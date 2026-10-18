# Distributed training at scale

How a neural network is trained across many GPUs at once: why it has to be, how much memory training
really takes, and the strategies that split the memory and the work across a cluster. All of it comes from
[lecture 9](09-massively-parallel-training.md), Mathias Lechner's guest lecture on how Liquid AI trains its
models on thousands of GPUs. Section numbers below refer to that page.

## Why one GPU is not enough

Training is mostly matrix multiplication, and GPUs do it far faster than CPUs. Lecture 9's slide 3 times
one multiplication of a $256 \times 4096$ input by a $4096 \times 4096$ weight matrix, 8.6 billion
floating-point operations: about 86 ms on a 2011 CPU, 5.4 ms on a 2011 gaming GPU and 8.7 µs on a 2022
NVIDIA H100 (lecture 9, section 3). That is why deep learning trains on GPUs at all (see also
[what is deep learning?](what-is-deep-learning.md), "Why now?").

Scaling laws then push toward more of everything. On Meta's Llama 2 curves, more training tokens lower the
loss, and at every token count a larger model has the lower loss (slides 4–5); the slides credit the
power-law form to Kaplan et al. (2020) (lecture 9, section 4). Training a large model on a large dataset in
reasonable time takes many GPUs, and a large model's training state does not fit on one GPU anyway.

## The memory of training

Training needs far more memory than the weights. Lecture 9's slide 8 works it out for a model of 1 billion
parameters (batch size 16, 256 layers, hidden size 1024) (lecture 9, section 7):

- **parameters**, at 16 bits: 2 GB;
- **gradients**, the same size: 2 GB;
- **optimizer states**: Adam keeps two values per parameter at 32 bits, 8 GB;
- **activations**, kept from the forward pass because backpropagation multiplies each layer's backward
  signal by them (see [backpropagation](backpropagation.md)): about 16 GB.

That is about 28 GB for a small model, and about 2 TB for a 70-billion-parameter one, against single GPUs
of a few hundred gigabytes. Three families of technique reduce the memory each device holds:

- **Activation checkpointing** keeps the activations of only some layers (say every fourth) and recomputes
  the rest during the backward pass. In slide 9's example it cuts activation memory fourfold for about 30%
  more compute — one extra forward pass. It is used heavily, because memory is typically more precious than
  compute (section 8).
- **Offloading** moves rarely used data — optimizer states, inactive layers, activations — to CPU memory.
  Its limit is bandwidth: an H100's HBM moves 3.35 TB/s, the PCIe bus 64 GB/s, so offloading suits niche
  cases such as fine-tuning a large model on one GPU (section 9).
- **Sharding** partitions the training state across devices, so that each holds only a part and they
  communicate to gather the rest when needed (section 11). Sharding only the optimizer states, which are
  used once per step, is the simplest case; sharding gradients and then parameters saves more and costs
  more communication.

**Mixed precision** — lower precision where the network tolerates it — also saves memory (section 19).

## The cluster, and why bandwidth decides everything

A cluster node holds a CPU and, in NVIDIA's case, eight GPUs joined by NVLink: **scale up**. Nodes are
joined by an InfiniBand network: **scale out**. Remote direct memory access lets a GPU send data straight
from its memory to the network card without passing through either CPU (lecture 9, section 10). Every link
is slower than the one inside it; slide 11's figures are about 20 TB/s for cache, 3.35 TB/s for HBM,
900 GB/s for NVLink, 200 GB/s per InfiniBand link and 64 GB/s for PCIe.

Lecture 9's key principle follows: **match the parallelism strategy to the bandwidth hierarchy** (slide 22).
The strategies differ in how much they communicate, so the most communication-hungry one goes on the
fastest link, and the least on the slowest (section 20).

## The parallelism strategies

Each splits a different thing (lecture 9, sections 6 and 11–15):

| Strategy | What is split | Communication | Notes |
| --- | --- | --- | --- |
| Data parallel (DP) | the batch; every GPU holds the whole model | one all-reduce of the gradients per step | scales linearly, but a very large batch hurts generalization |
| Pipeline parallel (PP) | the layers, by depth | activations passed between stages | idle "bubbles", filled by micro-batching |
| Tensor parallel (TP) | each weight matrix, within a layer | an all-reduce per column–row pair | very communication-intensive; kept inside a node |
| Sequence / context parallel (SP/CP) | the sequence positions | none for time-independent layers; key–value exchange for attention | for long-context training |
| Expert parallel (EP) | a mixture of experts' experts, across devices | an all-to-all that routes tokens to experts | needs the router to balance the load |

**Data parallelism** is the default of distributed training: every other method assumes it (section 11).
It works because the samples of a mini-batch are independent and only their gradients are averaged (see
[gradient descent](gradient-descent.md)). In lecture 9's example, a batch of 256 is split over four GPUs,
64 each, and the four gradients are averaged:

$$\nabla W = \frac{\nabla W_0 + \nabla W_1 + \nabla W_2 + \nabla W_3}{4}$$

**Pipeline parallelism** gives each GPU a stretch of layers. Run naively, only one GPU works at a time; cutting
the batch into micro-batches lets the stages work on different micro-batches at once (section 12).

**Tensor parallelism** splits a matrix multiplication $XW = Y$. Splitting $W$ by columns needs the whole input
and gives a partitioned output; splitting by rows takes a partitioned input and needs an all-reduce to sum the
partial outputs. A transformer's MLP pairs them, column then row with the non-linearity between, so two layers
cost one all-reduce (section 13; see [attention and transformers](attention-and-transformers.md)).

**Sequence and context parallelism** split the sequence. Layers that do not mix across time, such as MLPs and
layer norms, need no communication; attention does, and context parallelism partitions its keys and values
(the KV cache) across GPUs (section 14).

**Expert parallelism** places the experts of a mixture-of-experts layer on different devices. A router sends
each token to a few experts, so a model like Liquid AI's LFM2-8B-A1B has 8.3 billion parameters but only 1.5
billion active. If the router sends most tokens to a few experts, their GPUs carry the load while the others
idle (section 15).

## Combining them: 5D parallelism

The strategies stack, each along its own axis of the cluster, which is why the combination is called 4D or
5D parallelism (lecture 9, section 19). Slide 21's example runs on 2048 GPUs as data parallel 8 $\times$ tensor
parallel 8 $\times$ pipeline parallel 4 $\times$ expert parallel 8: tensor parallelism within a node over NVLink, pipeline
stages across nodes, data parallelism for throughput, and expert parallelism for the MoE layers. Fused
kernels and FlashAttention are further optimizations on top. There is no single recipe: how a model is split
depends on its size and on the cluster, and Liquid AI trains an 8B model differently from a 1B model
(section 20).

Small models are the hard case: past a good batch size there are few layers to pipeline and small matrices to
split, so their training is sped up mostly by algorithms such as distillation (section 21).

## Frameworks

Three PyTorch frameworks implement these strategies (lecture 9, sections 16–18):

- **DeepSpeed ZeRO** (Microsoft), the "Zero Redundancy Optimizer", shards memory in three stages: optimizer
  states (ZeRO-1), then gradients (ZeRO-2), then parameters (ZeRO-3). In slide 18's example the per-GPU
  memory falls from 12 GB to 6, 4.5 and 3 GB. ZeRO-3 lets a model that fits on no single GPU be trained
  across several. It is used by wrapping the model in one call, with the strategy in a config file.
- **FSDP**, fully sharded data parallel (Meta), is PyTorch's native ZeRO-3-style sharding. Each wrapped
  module gathers its parameters just before it computes and discards them afterwards.
- **Megatron-LM** (NVIDIA) focuses on parallelism and throughput, with pipeline and tensor parallelism built
  in, at the price of more custom code.

Lechner's advice for a first project is DeepSpeed, the easiest to adopt, which also offers offloading for a
single GPU. Liquid AI's large pre-training runs use FSDP with its own fork of Megatron (section 21).

## Where this comes up

- [Lecture 9 — Secrets of Massively Parallel Training](09-massively-parallel-training.md): the whole lecture.
- [Lecture 1 — Introduction to Deep Learning](01-introduction.md): Adam, the optimizer whose states
  lecture 9 counts (section 13), and mini-batches and GPUs (section 14).
- [Lecture 6 — Language Models and New Frontiers](06-language-models-new-frontiers.md): emergent abilities
  with scale, the other side of the scaling laws.
- [Large language models](large-language-models.md): what these training runs produce.
