# Lecture 9 — Secrets of Massively Parallel Training

**MIT 6.S191, 2026 edition. Guest lecturer: Mathias Lechner, co-founder and CTO of Liquid AI.**
[Video](https://www.youtube.com/watch?v=UZZD9d9YqnQ) ·
[Slides (PDF)](https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L9.pdf) ·
[Slide-by-slide transcription](../raw/slides/09-massively-parallel-training.md) ·
[Transcript](../raw/transcripts/09-massively-parallel-training.md) ·
[Verbatim captions](../raw/transcripts/original/09-massively-parallel-training.md)

A guest lecture on how a model is trained across thousands of GPUs, from the company that trains Liquid
AI's LFM2 models. Mathias Lechner answers three questions in turn. **Why we scale**: training is mostly
matrix multiplication, which GPUs do far faster than CPUs, and scaling laws say a larger model trained on
more data fits the data better. **What we scale**: the memory a training run needs and how to cut it
(activation checkpointing, offloading, sharding), and the ways to split the work across devices — data,
pipeline, tensor, sequence and context, and expert parallelism. **How we scale**: three PyTorch
frameworks that implement these strategies, DeepSpeed ZeRO, FSDP and Megatron-LM. A real run combines
several strategies at once ("5D parallelism"), and the principle that decides which goes where is the
bandwidth of each link in the cluster: the most communication-hungry strategy gets the fastest link.

The deck is 22 slides. Its agenda (slide 2) ends with a case study, "Training LFM2", that has no slide of
its own and is not given as a separate part of the talk; LFM2 models come up as examples along the way
(slides 6 and 17) and in the questions. Six questions from students close the lecture.

## 1. Introduction (0:05–0:51)

Alexander Amini introduces Lechner as co-founder and CTO of Liquid AI. Before co-founding it, Lechner was
a researcher at MIT CSAIL, where he co-invented liquid neural networks. Amini, also a co-founder of Liquid
AI, has worked with him for nine years (≈0:05).

## 2. The talk, and Liquid AI (0:51–2:22)

Lechner's subject is how Liquid AI scales training runs up to thousands of GPUs (≈0:51). Liquid AI is an
MIT spin-off, about three years old, that builds efficient foundation models; about half a year before
the talk it released the LFM2 series of language models optimized to run on devices (slide 2,
≈0:51–1:37). The talk follows the agenda of slide 2: why we scale machine learning models at all, what we
scale (the strategies that shard and partition a workload across a cluster), how we scale (the PyTorch
training frameworks that implement them), and a case study of what the company's own training runs use
(≈1:37–2:22).

## 3. Why train on GPUs? (2:22–4:40)

Lechner starts in 2011 with AlexNet, an image-recognition network that was one of the first trained fully
end to end on a GPU and that "really sparked the deep learning revolution". It was trained on two NVIDIA
GTX 580 GPUs for about two weeks (slide 3, ≈2:22).

Training a neural network is essentially a series of matrix multiplications; there are other operations,
but the multiplications are the heavy part (≈3:07). Slide 3's example multiplies an input of 256 rows by
4096 features by a $4096 \times 4096$ weight matrix:

$$[256 \times 4096] \times [4096 \times 4096] = 8.6 \text{ GFLOP}$$

about 8.6 billion floating-point operations, "additions and multiplications" (≈3:07). The slide then
times that one multiplication on three devices:

| Device | Peak rate | Precision | Time for 8.6 GFLOP |
| --- | --- | --- | --- |
| CPU (2011): Intel i7-3960X | 0.1 TFLOPS | FP32 | ≈ 86 ms |
| GPU (2011): GTX 580 | 1.58 TFLOPS | FP32 | ≈ 5.4 ms |
| GPU (2022): NVIDIA H100 | 989 TFLOPS | BF16 | ≈ 8.7 µs |

A 2011 CPU managed about 0.1 teraflops (trillion floating-point operations per second); the gaming GPU
did 16 times more (≈3:07–3:54). AlexNet's two weeks on two GPUs would therefore have taken "basically a
year" on a CPU. The takeaway: training is compute-intensive, and the kind of computation it needs fits
what GPUs accelerate (≈3:54). Since then hardware has kept improving: the H100, still widely used for
training and inference, does "right around 1000x more" than the gaming GPU (slide 3, "~1000× since
2011"; ≈3:54–4:40). See "Spoken versus printed" below for the arithmetic on these figures.

## 4. Why larger datasets, and larger models? (4:40–6:57)

**More data.** Meta's Llama 2 7B, an open-source large language model from 2023, came with its training
curve (slide 4, ≈4:40). The horizontal axis is the number of training tokens processed, in billions (0
to 2,000); the vertical axis is the training perplexity, "kind of how well the model fits to the training
data". The curve falls steadily, from above 2.2 at the start to about 1.75 at 2 trillion tokens: more
training data gives a lower loss, a better fit (≈5:26). That assumes the data is fresh and high quality.
This is not just eyeballing a plot: **scaling laws** capture the loss's dependence on dataset size as a
power law (≈5:26). The slide credits that to Kaplan et al. (2020): "Loss decreases as a **power law**
with dataset size."

**Larger models.** Meta trained four sizes of the same architecture — 7B, 13B, 34B and 70B parameters —
and shared all four curves (slide 5, ≈6:12). At any point on the token axis the loss falls monotonically
with model size: a larger model on the same data fits better and is more capable. The curves never cross;
at 2 trillion tokens they end at about 1.75, 1.67, 1.57 and 1.50 (approximate readings in the slide
transcription). Again, this has been analysed systematically (≈6:12); slide 5 states that loss also
falls as a power law with model size.

![Slide 5 — Llama 2 training perplexity against processed tokens for the 7B, 13B, 34B and 70B models](../raw/images/09-massively-parallel-training/slide-5.jpg)

*Slide 5: four Llama 2 sizes; at every token count the larger model sits lower.*

## 5. The scaling imperative, and why the examples got smaller (6:57–8:29)

The "scaling imperative" is to train larger models, with more parameters, on more tokens, because the
scaling laws promise a better model (slide 6, ≈6:57). Slide 6 cites "Scaling Laws (Kaplan et al., 2020)
+ Chinchilla (Hoffmann et al., 2022)" and three models:

- **GPT-3** (2020): 175B parameters, 300B tokens.
- **LLaMA 2** (2023): 70B parameters, 2T tokens — roughly 10 times the data.
- **LFM2.5-1.2B** (2026): 1.2B parameters, 28T tokens, released by Liquid AI the week of the talk — more
  than another 10 times the data (≈6:57–7:43).

Dataset sizes clearly grow. But the models in these examples get *smaller*, the opposite of what Lechner
has just argued (≈7:43). The reason is that the scaling laws concern only training. After training, a
model is run, and a service like ChatGPT is trained once and then used by millions of people, so over a
model's lifetime inference dominates the compute and training is a small portion of it. Hence the big
push for efficient models (≈7:43–8:29). GPT-3's weights would not even fit on Lechner's laptop, while
LFM2.5 runs on a phone, much faster, and even on a Raspberry Pi, with quality "much better" than GPT-3's
(≈8:29).

## 6. Data parallelism (8:29–11:34)

The easiest way to scale the amount of data processed exploits a property of stochastic gradient descent:
the samples in a batch are independent of one another, and only at the end are their gradients averaged
(≈8:29–9:16). **Data parallelism** uses this in three steps (slide 7):

1. **Replicate**: put a full copy of the model, with its optimizer states, on every GPU.
2. **Distribute**: give each GPU a different part of the batch; each computes its gradients on its own.
3. **Synchronize**: average the gradients across GPUs in one communication step at the end.

The heavy computation — the forward and backward passes — runs independently on every device, and very
little communication is needed (≈9:16–10:02). In slide 7's example a batch of 256 samples is split over
four GPUs, 64 each; each computes a local gradient $\nabla W_i$, and an **all-reduce** averages them:

$$\nabla W = \frac{\nabla W_0 + \nabla W_1 + \nabla W_2 + \nabla W_3}{4}$$

![Slide 7 — a 256-sample batch split into four 64-sample shards on four GPUs, with an all-reduce averaging the gradients](../raw/images/09-massively-parallel-training/slide-7.jpg)

*Slide 7: each GPU holds the full model and a quarter of the batch; only the gradient average crosses between them.*

Throughput scales linearly: add GPUs and the effective batch size grows with them (≈10:02). That is also
the method's limit. Past some point the batch is so large that generalization suffers: train one model
with a small batch and one with a gigantic batch on the same data, and the small-batch model does better
on the test set — a matter of the loss landscape, on which many papers have been written (≈10:48; slide
7, "Large batches can hurt generalization"). So batch-size scaling is the most naive way to scale, up to
a threshold, and scaling throughput *without* growing the batch is much harder (≈10:48). For the
mini-batches being split here, see [gradient descent](gradient-descent.md).

## 7. How much memory does training need? (11:34–13:05)

Slide 8 asks what the largest model is that fits on one GPU, and works an example: a 1-billion-parameter
model with batch size 16, 256 layers and hidden size 1024 (≈11:34).

| Item | Size | Slide 8's working |
| --- | --- | --- |
| Parameters (bf16) | 2 GB | 1B × 2 bytes |
| Gradients (bf16) | 2 GB | same size as the parameters |
| Adam optimizer states (fp32) | 8 GB | 2 moments × 4 bytes × 1B parameters |
| Activations (all layers) | ~16 GB | 256 layers $\times$ batch 16 $\times$ hidden 1024 $\times$ 2 bytes |
| **Total** | **~28 GB** | |

Each line has a reason (≈11:34–12:19). The parameters are usually stored at 16-bit precision. A gradient
buffer of the same size holds the gradient. The optimizer states exist because training does not apply
plain gradient descent but preconditions each update — different parameters learn at different speeds —
and Adam keeps extra values that are "a multiplier on the parameters", here stored at 32 bits (they can be
quantized to some extent). The activations are needed by backpropagation: the backward signal arriving at
a layer is multiplied by that layer's activations from the forward pass, so they must be remembered (see
[backpropagation](backpropagation.md)).

![Slide 8 — memory breakdown for training a 1B-parameter model: parameters, gradients, optimizer states and activations](../raw/images/09-massively-parallel-training/slide-8.jpg)

*Slide 8: the stack's heights follow the sizes — activations and optimizer states dwarf the weights themselves.*

So even a small model needs about 28 GB to train, and a 70-billion-parameter model would need about 2 TB,
while the largest single GPUs hold "200, 300, 400 GB" (slide 8, ≈12:19–13:05). Training needs better
strategies to reduce memory. (Slide 8's activation working multiplies out to about 8.4 million bytes, not
16 GB; the slide does not show what else enters the figure.)

## 8. Activation checkpointing (13:05–14:37)

**Activation checkpointing** is used heavily in industry. It is not a free lunch but a trade of compute
for memory (slide 9, ≈13:05). Without it, the activations of every layer are stored for the backward
pass. With it, only some are kept: say every fourth layer, so layers 1 and 5 keep their activations and
the layers in between discard theirs during the forward pass. When the backward pass reaches layer 5,
the activations of layers 2, 3 and 4 are recomputed from the checkpoint, and backpropagation finishes
that stretch (≈13:51). In this scenario memory falls fourfold (slide 9: from "~8 GB activations" to "~2 GB
activations", "4x Memory reduction").

![Slide 9 — activation checkpointing: all layer activations stored versus only checkpoints stored](../raw/images/09-massively-parallel-training/slide-9.jpg)

*Slide 9: green layers keep their activations; brown ones are discarded and recomputed during the backward pass.*

The extra compute sounds expensive, but it is not (≈14:37). The first forward pass and the backward pass
happen anyway, and the backward pass already does two jobs, propagating back to the inputs and computing
the weight gradients; checkpointing adds one more forward pass, a small portion of the whole. Slide 9
puts it at "~30%" extra compute, "FWD + 2×BWD → FWD + 2×BWD + FWD". A second reason it is used so much
is that on typical GPUs compute tends to be cheaper than memory — "In practice, memory is more precious
than compute" (slide 9, ≈14:37).

## 9. Offloading to CPU memory (14:37–16:55)

**Offloading** applies a general idea of computer science, the memory hierarchy, in which infrequently
used data is pushed to a slower but larger tier, as a laptop moves data from cache to main memory to disk
(slide 10, ≈14:37–15:23). In training, three things are candidates: the optimizer states, used only at
the very end to precondition the weight update; the parameters of inactive layers, since layer 100 is
not needed while layers 1 to 10 compute; and the activations. Because the data is not needed all the
time, the transfer cost may amortize over a training step (≈15:23).

The catch is bandwidth (≈16:09). Data in the host's memory must cross the PCIe bus and another bus to
reach the GPU, which from the GPU's point of view is slow. Slide 10 gives the numbers: 3.35 TB/s for an
H100's HBM against 64 GB/s for PCIe 5.0, "52× slower to fetch from CPU memory". So offloading is used for
niche applications: fine-tuning a large language model — fine-tuning a 70-billion-parameter model on one
GPU leaves no other option — and long context, where for very long sequences part of the sequence is
offloaded to CPU memory (Lechner names DeepSpeed Ulysses here; the slide does not). In general it suits
scenarios that need only a little training; to really use a cluster there are better strategies
(≈16:09–16:55).

## 10. Inside a GPU cluster: scale up and scale out (16:55–19:12)

To see those strategies, look inside the clusters being built now, "these gigawatt clusters" (slide 11,
≈16:55). A **node** has a CPU connected to several GPUs, in NVIDIA's case eight per host. Each GPU has its
own cache and its own HBM (high-bandwidth memory), and the CPU has its own memory pool (≈16:55–17:40).
The GPUs of a node are joined by a very fast interconnect, NVLink in NVIDIA's terminology; putting as
many GPUs as fit in one node, typically eight, is **scale up**. The GPUs reach the CPU over a slower bus.
**Scale out** adds more replicas of the machine and joins them by a network, InfiniBand in NVIDIA's case
(≈17:40–18:26).

InfiniBand is much like everyday networking, except that it must support **remote direct memory access
(RDMA)**: when two GPUs on different nodes exchange data, they should not go through the CPU on each
machine, as a normal network stack would, but pipe the data straight from HBM into the network interface
(slide 11, ≈18:26; the slide's two paths are "GPU → CPU → NIC → net → NIC → CPU → GPU" against "GPU →
RDMA NIC → net → RDMA NIC → GPU", which "Bypasses CPU + OS"). The interconnect within a node is much faster
than the scale-out fabric (≈18:26–19:12). Slide 11's legend gives each tier's bandwidth:

| Link | Bandwidth |
| --- | --- |
| Cache | ~20 TB/s |
| HBM | 3.35 TB/s |
| DDR5 | ~400 GB/s |
| NVLink | 900 GB/s |
| InfiniBand (IB) | 200 GB/s per link |
| PCIe | 64 GB/s |

![Slide 11 — two GPU nodes with NVLink, PCIe and InfiniBand links, and a traditional versus RDMA transfer path](../raw/images/09-massively-parallel-training/slide-11.jpg)

*Slide 11: NVLink joins the GPUs inside a node (scale up); an InfiniBand switch joins the nodes (scale out).*

## 11. Sharding (19:12–21:30)

**Sharding** is another generic idea: partition data across several locations, as large databases are
partitioned across the globe (slide 12, ≈19:12). In training, almost anything can be sharded: the model
weights, the optimizer states, the activations, the data and the gradients. The trade-off is always the
same: each device holds less memory, but the devices must communicate to gather what they need, and that
communication looks different for each thing sharded (≈19:12–19:58). Every method from here on assumes
data parallelism as the default setting of distributed training (≈19:58).

The simplest case is **optimizer state sharding**, because the optimizer is used only at the end, to
precondition the weight update (slide 13, ≈19:58). In slide 13's example, plain data parallelism on two
GPUs keeps a full replica on each: 8 GB of optimizer states, 2 GB of parameters and 2 GB of gradients,
12 GB per GPU and 24 GB in all. Splitting the optimizer states into two shards, one per GPU, cuts each to
8 GB, 16 GB in all, a saving the slide puts at 33% (≈20:44).

![Slide 13 — per-GPU memory with and without optimizer state sharding across two GPUs](../raw/images/09-massively-parallel-training/slide-13.jpg)

*Slide 13: only the optimizer states are split; parameters and gradients stay whole on both GPUs.*

The price is a changed update, in four steps (slide 13, ≈20:44–21:30):

1. **Forward and backward**: each GPU computes its local gradients, with no communication.
2. **Reduce-scatter**: the GPUs exchange gradients so that each receives the gradients for its own shard.
3. **Local update**: each GPU updates the parameters of its shard.
4. **All-gather**: the updated parameters are exchanged across the whole sharding group.

The savings are large because Adam keeps two values per parameter (≈21:30).

## 12. Pipeline parallelism (21:30–24:33)

**Pipeline parallelism** both reduces memory and raises throughput (≈21:30). A deep network is deep
because it has many layers, so split it by depth: layers 0 to 31 on GPU 0, the next layers on GPU 1, and
so on (slide 14, ≈22:16; the slide's four stages hold layers 0–31, 32–63, 64–95 and 96–127).

The major issue is the **pipeline bubble** (≈22:16). During the forward pass, while GPU 0 computes the
first layers it runs at 100% and the others sit idle, waiting for work; the backward pass is the same in
reverse order. The fix is **micro-batching**: split the batch into smaller units, so that GPU 0 computes
the first micro-batch and hands it to GPU 1, then starts the second while GPU 1 works on the first, and
likewise for the backward pass (≈23:02). Slide 14 prints the bubble's size as "O((p-1)/m)", without
defining the symbols; the talk does not read it out.

![Slide 14 — pipeline schedules on four GPUs: a naive pipeline with idle bubbles, and micro-batching](../raw/images/09-massively-parallel-training/slide-14.jpg)

*Slide 14: in the naive schedule each GPU waits for the one before it; micro-batches fill most of the idle time.*

Industry uses pipeline parallelism heavily, with more sophisticated schedules than plain micro-batching
(slide 14, ≈23:02–24:33). Llama 3 schedules forward and backward passes bidirectionally, interleaving
them much more — the last GPU in the pipeline, for instance, prioritizes backward passes early so the
earlier GPUs can start backpropagating. DeepSeek's DualPipe, used in DeepSeek-V3, splits the work more
finely still, separating the backward pass to the input from the backward pass to the weights into
smaller units that can be scheduled separately.

## 13. Tensor parallelism (24:33–26:04)

Pipeline parallelism splits the network by depth; **tensor parallelism** splits within a layer (slide
15, ≈24:33). A layer computes a matrix multiplication $XW = Y$, and the weight matrix $W$ can be split in
half across two GPUs in two ways:

- **Column parallelism**: split $W$ by columns into $W_1$ (GPU 0) and $W_2$ (GPU 1). The input $X$ must be
  replicated on both devices, and the output comes out partitioned, $Y_1$ and $Y_2$, with no collective
  communication.
- **Row parallelism**: split $W$ by rows. The input can arrive partitioned, $X_1$ and $X_2$, and each GPU
  produces a partial output; an all-reduce sums $Y_1 + Y_2$ into $Y$.

The two sound the same, and the difference is nuanced (≈24:33–25:18). It pays off in a transformer's MLP,
which stacks two layers with a non-linearity between them (GeLU here; without it the stack would be
pointless). Start from a replicated input, make the first layer column-parallel, so the intermediate
states come out partitioned; apply the non-linearity to each part with no communication; make the second
layer row-parallel, which accepts partitioned inputs; and finish with one all-reduce that makes the output
replicated again (slide 15, ≈25:18–26:04). Two sharded layers cost one communication step, which is why
tensor parallelism is used in this form. The slide adds that it "Requires high-bandwidth interconnect
(NVLink)".

![Slide 15 — column-parallel and row-parallel splits of a weight matrix, and their pairing in a transformer MLP](../raw/images/09-massively-parallel-training/slide-15.jpg)

*Slide 15: column-split W1, then row-split W2 — the GeLU between them needs no communication, and one all-reduce ends the block.*

For self-attention and the transformer, see [attention and transformers](attention-and-transformers.md).

## 14. Sequence and context parallelism (26:04–27:36)

The sequence is another dimension to split (slide 16, ≈26:04). With a training context of 8K tokens,
tokens 0 to 2000 can go to GPU 0, the next 2000 to GPU 1, and so on. Many layers — MLPs, layer norms —
do not mix information across time, so in them the GPUs need not communicate at all: this is **sequence
parallelism**. Attention does mix across the sequence and needs more care. **Context parallelism**
partitions the KV cache, and there are many algorithms for doing it efficiently, such as ring attention
(≈26:50). So: sequence parallelism for the time-independent layers, context parallelism for attention.
Slide 16 shows a query block for the current tokens against key–value blocks of past tokens (0–2K, 2K–4K,
4K+) on different GPUs, exchanged by an all-to-all, and claims 100K+ token contexts for context
parallelism and 1M+ for the two combined.

![Slide 16 — sequence parallelism over an 8K-token sequence on four GPUs, and context parallelism over key-value chunks](../raw/images/09-massively-parallel-training/slide-16.jpg)

*Slide 16: sequence parallelism shards activations by position; context parallelism shards attention's keys and values.*

In practice these are used for long-context training (≈26:50–27:36). A large model is mostly trained on a
short context such as 8K; after the main training phase the context is extended by training on further
tokens at a longer length (the captions garble how many, somewhere between hundreds of billions and
trillions), so the model need not be trained from scratch with a million-token context.

## 15. Mixture of experts and expert parallelism (27:36–30:41)

The last parallelism strategy comes with an architecture (slide 17, ≈27:36). A **mixture of experts
(MoE)** layer tries to scale model capacity without adding compute. Normally a bigger weight matrix makes
inference and training more expensive. An MoE layer instead slices the weight matrix into parts called
**experts**, and a **router** decides which to activate for each token; the rest are treated as zero.
It is a form of structured sparsity (≈28:22). Slide 17 contrasts a dense FFN ("All params used for every
token") with an MoE FFN in which a softmax router picks the top 2 of 8 experts and sums their outputs,
weighted ("Only top-K experts compute → sparse activation").

That suggests a natural way to partition: **expert parallelism** puts different experts on different
devices — experts 0 and 1 on device 0, experts 2 and 3 on device 1, and so on — with communication to
route each token to its experts and aggregate the results (slide 17, "All-to-All: route tokens to the
correct experts"; ≈28:22–29:08).

![Slide 17 — a dense FFN against a top-2 MoE FFN, and eight experts placed two per GPU across four GPUs](../raw/images/09-massively-parallel-training/slide-17.jpg)

*Slide 17: only the two selected experts compute for a token, and expert parallelism spreads the eight experts over four GPUs.*

Liquid AI's own example is LFM2-8B-A1B, a model of 8.3 billion parameters of which only 1.5 billion are
active: it runs at the speed of a 1.5-billion-parameter model with the capacity of an 8-billion one
(slide 17, ≈29:08). The parameters scale; the compute scales much less.

The major challenge is **load balancing**, for two reasons (≈29:08–30:41). The first is training
stability: if the router overfits and sends every token to one expert, the rest are never activated and
you are in effect training a small network. Methods to balance the load during training are still being
developed. The second is expert parallelism itself: if all the tokens go to experts 0 and 1, one GPU
carries all the load while the rest idle, which slows training a lot. Research on doing this properly is
ongoing.

## 16. DeepSpeed ZeRO (30:41–32:13)

The rest of the talk turns to frameworks that implement these strategies (≈30:41). The first is
**DeepSpeed ZeRO**, the "Zero Redundancy Optimizer", which is about sharding memory on top of the
baseline of data parallelism (slide 18). It has three stages:

- **ZeRO-1** shards the optimizer states, exactly as in section 11. Its communication is the
  reduce-scatter of gradients to their shards and the all-gather of the updated parameters (≈31:26).
- **ZeRO-2** also shards the gradients, adding a further reduce-scatter that sends gradients to the
  shard that holds them.
- **ZeRO-3** shards everything: optimizer states, gradients and parameters. It needs much more
  communication, because parameters are used far more often than optimizer states — in every forward and
  backward pass. In practice it still works, because parameters are moved in blocks rather than weight by
  weight (≈31:26).

Slide 18's example shows the per-GPU memory falling stage by stage:

| Stage | Optimizer | Gradients | Parameters | Per GPU |
| --- | --- | --- | --- | --- |
| Baseline (DDP) | 8 GB | 2 GB | 2 GB | 12 GB |
| ZeRO-1 | 2 GB shard | 2 GB | 2 GB | 6 GB |
| ZeRO-2 | 2 GB shard | 0.5 GB shard | 2 GB | 4.5 GB |
| ZeRO-3 | 2 GB shard | 0.5 GB shard | 0.5 GB shard | 3 GB |

![Slide 18 — per-GPU memory for baseline data parallelism and ZeRO stages 1 to 3, with their communication patterns](../raw/images/09-massively-parallel-training/slide-18.jpg)

*Slide 18: each ZeRO stage shards one more kind of state, trading communication for memory.*

ZeRO-3 is what lets a model too big for one device's memory be trained across several GPUs (slide 18,
≈32:13). DeepSpeed is not to be confused with DeepSeek (≈32:13).

## 17. Fully sharded data parallel (32:13–33:44)

**Fully sharded data parallel (FSDP)** is PyTorch's native implementation of ZeRO-3-style sharding
(slide 19, ≈32:13). Being PyTorch-native, it is used by wrapping an `nn.Module` in an FSDP block, which
handles the sharding. By default all the data is sharded fully — hence the name. When the Python program
enters a layer in the forward pass, FSDP all-gathers its parameters, so the code sees all the layer's
weights; when execution leaves the layer, the gathered copy is discarded and only the shard remains
(≈32:58; slide 19, "gather → compute → discard"). The backward pass is similar, with gradients
communicated as well (slide 19: "All-Gather params → Compute grads → Reduce-Scatter").

![Slide 19 — FSDP unit wrapping, the forward gather-compute-discard flow, and the three sharding strategies](../raw/images/09-massively-parallel-training/slide-19.jpg)

*Slide 19: each wrapped block gathers its parameters just in time and drops them again afterwards.*

FSDP has several settings, so it can also implement ZeRO stages one and two (≈33:44). Slide 19 lists
three: FULL_SHARD (parameters, gradients and optimizer; maximum savings, most communication),
SHARD_GRAD_OP (gradients and optimizer only; parameters replicated) and NO_SHARD (plain data-parallel
behaviour, least communication). FSDP is used heavily together with activation checkpointing to train
large models (≈33:44).

## 18. Megatron-LM, and how the frameworks differ (33:44–36:01)

The third framework is **Megatron-LM**, NVIDIA's framework for distributed training of large
transformers (slide 20, ≈33:44). If DeepSpeed and FSDP offer the same features, how do they differ? The
biggest difference is who made them: DeepSpeed comes from Microsoft, FSDP from Meta and Megatron from
NVIDIA. Google is missing because it uses JAX rather than PyTorch (≈34:29). Conceptually they are very
similar, with different focuses and design philosophies (slide 20):

| Aspect | DeepSpeed ZeRO | FSDP | Megatron |
| --- | --- | --- | --- |
| Focus | Memory | Memory | Parallelism |
| PP / TP | Limited | No | Native |
| Philosophy | Wrap model | nn.Module | "MPU" |
| Ease of use | config.yaml | PyTorch native | Custom code |

DeepSpeed ZeRO and FSDP are mostly about memory; Megatron also focuses on parallelization and throughput,
so pipeline and tensor parallelism, which must be added to FSDP and DeepSpeed from outside, come as
ready-made layers in Megatron (≈34:29–35:15). DeepSpeed's philosophy is not to change your code: define
the model, optimizer and data loader, wrap them in one DeepSpeed call — a one-line change — and choose
the sharding methods in a YAML config file, separating code from configuration (≈35:15–36:01). FSDP feels
native to PyTorch: you define your own `nn.Module`. Megatron is more complex, with a "model parallel
unit" that tracks what is sharded where (the communication groups), and needs much more custom code, in
exchange for more features.

## 19. Putting it all together (36:01–39:04)

Suppose you have a cluster of about 2,000 GPUs and want to train a big model as fast as possible (slide
21, ≈36:01). First, memory:

- **Activation checkpointing**, heavily, because memory is typically more precious than compute.
- **Mixed precision**: not every part of the network needs the same precision. The activations are much
  more sensitive, while the weights can be quantized to very low precision (≈36:46; slide 21, "bf16/fp8
  for activations").
- **FSDP or ZeRO sharding** of parameters, gradients and optimizer states, exchanged only when needed.
- **Offloading**, for niche applications (slide 21, "CPU / NVMe for cold data").

Then throughput. The parallelization strategies are often called **4D or, more recently, 5D
parallelism**, because they can be used at the same time, each along its own axis of the cluster
(≈36:46–37:32): data parallel, tensor parallel, pipeline parallel, sequence and context parallel, and
expert parallel, which is like tensor parallelism but for mixtures of experts. Further optimizations
include fused kernels, which keep the overhead of communication between CPU and GPU from adding up, and
FlashAttention, a cache-aware algorithm that uses the device's cache very efficiently (≈37:32).

Slide 21's example is a 2048-GPU run:

$$\text{DP} = 8 \times \text{TP} = 8 \times \text{PP} = 4 \times \text{EP} = 8 = 2048 \text{ GPUs}$$

with "TP within node (NVLink) • PP across nodes • DP for throughput • EP for MoE layers". Lechner walks
through it (≈38:18–39:04). Tensor parallelism is very communication-intensive, so it goes on a single
node, where eight GPUs share NVLink: tensor parallel 8. Pipeline parallelism splits the network's depth
across four nodes. Data parallelism processes different portions of the training batch on separate groups,
which exchange only gradient information at the end; expert and sequence parallelism are further
dimensions to add. In practice the strategies are stacked together. The captions of this passage are
muddled: Lechner first describes "TP8" as splitting the cluster into eight partitions that each have their
own mini-batch and exchange only gradients, which is how he described data parallelism (≈38:18), and then
as tensor parallelism within a node of eight GPUs.

## 20. Summary: match the strategy to the bandwidth hierarchy (39:04–41:23)

Lechner's summary follows slide 22 (≈39:04–40:36). Why scale: bigger models and more data fit the data
better; GPUs suit training far better than CPUs; and the models to be trained do not fit on one GPU,
since training needs much more memory than the weights. Memory solutions: activation checkpointing,
offloading, sharding and mixed precision. Parallelization strategies, which both reduce memory and raise
throughput: data parallelism, the naive one, limited by batch size; tensor parallelism, splitting weight
matrices; pipeline parallelism, splitting by depth; expert parallelism, tensor parallelism for MoE; and
context and sequence parallelism.

The key principle is to remember the cluster's network topology — which device is connected to which,
with what bandwidth and latency — and match the communication to that hierarchy (slide 22, "Match
parallelism strategy to your bandwidth hierarchy"; ≈39:50–40:36). A kernel developer thinks about cache,
not even HBM; above that come HBM, NVLink within a machine, and the scale-out InfiniBand network (slide 22:
"Cache > HBM (GPU memory) > NVLink (within node) > InfiniBand (within cluster) > ..."). No single strategy
suffices; in practice several are combined, and how depends on model size and cluster: Liquid AI trains an
8B model very differently from a 1B model, and both differently from how a 1-trillion-parameter model
would be trained (≈40:36–41:23).

## 21. Questions (41:23–52:50)

**What does the 2048-GPU example save in memory, against what it costs in compute?** (≈41:23–42:55).
The example is illustrative, chosen for a model of about 70 billion parameters in the style of Llama. Such
a model does not fit on one device; with FSDP or ZeRO it might fit on four nodes, but training would then
take years, and competition demands speed. So GPUs are added, and with them pipeline parallelism and the
rest. Data parallelism alone would be simplest, but the batch is already very large — language models use
batches of things like 8 billion tokens, and beyond that people start to see performance degrade
(≈42:55).

**How does the picture change for decentralized training, with unreliable workers that can drop out?**
(≈43:40–45:11). Data parallelism is well suited to it, because it needs the least communication of any
strategy. Lechner believes Google already runs data parallelism across different data centres, and he has
seen smaller distributed runs that try it. There is also research on asynchronous training, for workers
of very different speeds; it was used heavily in the past, but he has not seen many bigger runs with it
recently. It is an active research area (≈44:25–45:11).

**If a bigger batch harms generalization, how do you speed up training a small model?**
(≈45:11–46:43). Scaling is easy while data parallelism is within a good batch size, and very hard beyond
it. Pipeline parallelism is probably the first thing people add, but a small model has few layers — 32 or
16 — and small matrices, leaving little room to shard. So much of the gain comes from algorithms instead,
such as **distillation**, which accelerates training not by running more tokens but by giving a richer
training signal: instead of predicting the next token, the model predicts a teacher model's distribution
over it (≈46:43). The captions go on to say that "we" scaled "Llama 2" this way, with "a previous
generation Llama 1 7B model" as the teacher giving a distribution over "like 16" tokens; which models are
meant, and what the 16 counts, is unclear in the captions (see the transcript's note at 46:43).

**How much quality checking is possible on 28 trillion tokens, and could one train only on the data that
matters?** (≈46:43–49:00). The first trillion or so tokens of high-quality data — scientific papers,
Wikipedia and the like, available in open datasets on Hugging Face — are easy to get; the further along
the token axis, the harder high-quality data is to find. Liquid AI filters Common Crawl, trains smaller
filter models to detect which data could be useful for training the large ones, and runs many ablations on
data. Synthetic data is another direction, but a careful one: models trained fully on synthetic data
collapse much of the training dynamics — "people call it like the model has no soul" (≈48:14). Finding
the last 30 trillion or more tokens of high-quality data is very challenging (≈49:00).

**Will Liquid AI's models, as they compete with bigger ones, outgrow a phone's memory?** (≈49:00–51:18).
The company is still doing active research and believes much more is possible algorithmically and
architecturally; even LFM2 is "boring in a sense". There are challenges, including the current chip and
memory shortage. But Liquid AI works with hardware partners such as AMD and Qualcomm, and expects to
co-evolve with them: more low-precision flops on devices, perhaps different tiers of memory for
mixture-of-experts models. Phones have limits today, but he expects hardware over the next five years to
be much better designed for running generative AI (≈50:32).

**Which framework for training a domain-specific model?** (≈51:18–52:50). The easiest is DeepSpeed: a
one-line change brings much of the memory benefit, and it implements offloading, so even with one GPU,
where FSDP is no use, you can offload. It is the entry point; the more you customize, the further you go.
Liquid AI used DeepSpeed for early experiments on multimodality, but its bigger pre-training runs use FSDP
plus its own fork of Megatron, taking some of Megatron's sharding strategies and combining them with FSDP
for memory savings (≈52:04).

## Spoken versus printed

- **"~1000× since 2011"** (slide 3, and "right around 1000x" aloud, ≈3:54): the slide's own figures give
  989 ÷ 1.58 ≈ 626 for the H100 against the GTX 580. Its "16× faster" for the GTX 580 against the CPU
  matches 1.58 ÷ 0.1 ≈ 16. The H100's figure is printed for BF16 and the other two for FP32.
- **Slide 22's "GPUs: ~600× faster than CPUs"**: by slide 3's figures, the H100 does 989 ÷ 0.1 ≈ 9,890
  times the 2011 CPU's rate; about 600 is the ratio of the two GPUs.
- **Slide 9 against slide 8**: slide 9 prints "(128 layers total)" and "~8 GB activations" for the case
  without checkpointing, where slide 8's example has 256 layers and ~16 GB of activations. Slide 14's four
  pipeline stages hold layers 0–127, matching slide 9.
- **Slide 8's activation working**, $256 \times 16 \times 1024 \times 2$ bytes, multiplies out to about 8.4 million bytes,
  not the ~16 GB beside it.
- **"2,000 GPUs"** aloud (≈36:01) for slide 21's 2048-GPU example.
- **DeepSpeed Ulysses** (≈16:09) is named aloud but not on the slides; the agenda's case study on training
  LFM2 (slide 2) has no slide and no separate part in the talk.
- **Slide 18's "Memory" column** gives "4x reduction" for ZeRO-1 and "8x reduction" for ZeRO-2, while the
  same slide's columns take the per-GPU total from 12 GB to 6 GB ($2\times$) and 4.5 GB (about $2.7\times$); ZeRO-3's
  3 GB is $4\times$. Slide 13 (two GPUs) and slide 18 (four, by its shard sizes) are different set-ups, so
  their 8 GB and 6 GB per GPU for optimizer sharding are not in conflict.
- **Mixed precision**: aloud, the activations are "much more sensitive" and the weights can be quantized
  to very low precision (≈36:46); slide 21's card reads "bf16/fp8 for activations".

## Where this connects

- [Distributed training at scale](distributed-training.md) — the topic page for this lecture's ideas: the
  memory of training, the parallelism strategies and the frameworks.
- [Gradient descent](gradient-descent.md) — mini-batches, which data parallelism splits across GPUs, and
  Adam, whose optimizer states take most of the memory in slide 8's example.
- [Backpropagation](backpropagation.md) — why training must keep the forward pass's activations, the
  memory that activation checkpointing trades for compute.
- [Attention and transformers](attention-and-transformers.md) — the transformer's MLP and attention, which
  tensor and context parallelism split.
- [Large language models](large-language-models.md) — scaling laws, the training-versus-inference trade
  that pushes toward small models, data quality and distillation.
- [What is deep learning?](what-is-deep-learning.md) — GPUs as one of the reasons deep learning works now.
- [Lecture 6](06-language-models-new-frontiers.md), section 1, announces this guest lecture.
