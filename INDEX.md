# MIT 6.S191 — Introduction to Deep Learning

MIT's one-week introductory boot camp on deep learning, taught by Alexander Amini and Ava Amini, with
lectures, hands-on software labs in TensorFlow and PyTorch, and a project pitch competition. It runs
from the foundations of neural networks — the single neuron, training by gradient descent and
backpropagation — up to recent advances in large language models. Course site:
<https://introtodeeplearning.com/>.

**Coverage: lectures 1–4 only.** This knowledge base covers **lectures 1–4 of the 2026 edition**:
"Introduction to Deep Learning" (Alexander Amini) and "Recurrent Neural Networks, Transformers, and
Attention" (Ava Amini), both delivered 5 January 2026, and "Convolutional Neural Networks" (Alexander
Amini; the deck's title is "Deep Computer Vision") and "Deep Generative Modeling" (Ava Amini), both
delivered 6 January 2026. The Cairn catalog for this course lists 90 recordings — the 2026 edition's
lectures (positions 1–9) followed by the 2018–2025 editions — and none of the others is in this KB yet.
Do not cite it as the whole course: for any other lecture (reinforcement learning, language models,
diffusion models and the rest), say it is not covered. Vision transformers, which lecture 2 says
lecture 3 will cover, are not discussed in lecture 3.

## How to use this knowledge base

- Start from the lecture page or the topic page below. Lecture pages follow the lecture in order, with
  timestamps such as (≈24:10) into the transcript and slide citations.
- **"Slide N" means page N of the PDF.** The decks print no slide numbers.
- For exact wording, numbers, code and equations as printed, read the slide transcription in
  `raw/slides/`. For what was said, read the copy-edited transcript in `raw/transcripts/` (not the
  verbatim captions in `raw/transcripts/original/`, which are kept only as a reference).

## Images

All four lectures have slide images: **34 for lecture 1**, **33 for lecture 2**, **33 for lecture
3** and **39 for lecture 4**. Each is embedded where it is used: in the lecture page
([lecture 1](wiki/01-introduction.md), [lecture 2](wiki/02-rnns-transformers-attention.md),
[lecture 3](wiki/03-convolutional-neural-networks.md), [lecture 4](wiki/04-deep-generative-modeling.md))
beside the passage that cites the slide, in some topic pages, and under the matching `## Slide N`
heading of the slide transcription ([lecture 1](raw/slides/01-introduction.md),
[lecture 2](raw/slides/02-rnns-transformers-attention.md),
[lecture 3](raw/slides/03-convolutional-neural-networks.md),
[lecture 4](raw/slides/04-deep-generative-modeling.md)).
They are whole slides, every one that carries a distinct figure; slides without an image are text, code
or tables the transcription reproduces exactly, logistics, logos, stock photographs, video stills,
repeats of a rendered figure, or build steps contained in a rendered slide. No other lecture is in this KB, so no other lecture has images.

- **Use an image path you have actually read in a file. Never construct one from the pattern**, and
  never assume a slide has an image because a neighbouring slide does. Reading an image path returns
  its displayable URL.
- Prefer the slide transcription for numbers and code; the images are 1280×720.
- Show one image at a time, and keep its slide citation.

## Contents

### Lectures

- [Lecture 1 — Introduction to Deep Learning](wiki/01-introduction.md) — the whole lecture in order:
  the pace of the field (generated faces, GPT-4, an on-phone model demo); AI ⊃ ML ⊃ DL; why deep
  learning and why now; the perceptron and activation functions with a worked decision-boundary
  example; dense layers to deep networks in TensorFlow and PyTorch; "Will I pass this class?";
  loss, empirical loss, cross-entropy and MSE; gradient descent; backpropagation; learning rates and
  optimizers; mini-batches; overfitting, dropout and early stopping.
- [Lecture 2 — Recurrent Neural Networks, Transformers, and Attention](wiki/02-rnns-transformers-attention.md)
  — the whole lecture in order: why sequences (the ball example); one-to-one, many-to-one, one-to-many
  and many-to-many tasks; building recurrence from the perceptron; the RNN recurrence relation, state
  update and output equations, unrolling, and TensorFlow/PyTorch code; next-word prediction and the
  design criteria (embeddings, variable length, long-term dependencies, order); backpropagation through
  time, exploding and vanishing gradients, LSTMs; music generation; the limitations of RNNs;
  self-attention with query, key and value; attention heads and transformers.
- [Lecture 3 — Convolutional Neural Networks](wiki/03-convolutional-neural-networks.md) — the whole
  lecture in order: what vision is and where it is used (facial detection, the MIT self-driving car,
  medicine); images as matrices of numbers; regression and classification; hand-engineered versus
  learned features; why flattening into a fully connected network fails; patches, sliding windows and
  the convolution, with the "X or X?" case study and a worked 5×5 example; hand-written filters
  (sharpen, edge detect); CNN layers, the output volume, stride and receptive field; ReLU; max pooling;
  the learned feature hierarchy; softmax classification; TensorFlow and PyTorch code; applications:
  breast cancer screening, object detection (R-CNN, Faster R-CNN), semantic segmentation (FCN) and
  end-to-end navigation; lab 2.
- [Lecture 4 — Deep Generative Modeling](wiki/04-deep-generative-modeling.md) — the whole lecture in
  order: "which face is real?"; supervised versus unsupervised learning; density estimation and sample
  generation; debiasing, outlier detection and generative AI; latent variables and the Myth of the Cave;
  autoencoders, the reconstruction loss and the latent bottleneck; VAEs: mean and standard deviation
  vectors, the reconstruction and regularization terms, the Normal prior and KL-divergence, continuity
  and completeness, the reparametrization trick, latent perturbation, disentanglement and β-VAEs; GANs:
  generator and discriminator, the number-line intuition, the min-max objective, distribution
  transformers and latent interpolation; CycleGAN for images and speech; diffusion models deferred.

### Topics

- [What is deep learning?](wiki/what-is-deep-learning.md) — AI, machine learning and deep learning
  defined and nested; learned hierarchical features versus hand-engineered ones, including lecture 3's
  case for vision; supervised versus unsupervised learning; why now (big data, hardware, software) and
  the 1952–1995 timeline.
- [The perceptron](wiki/perceptron.md) — the single neuron: weighted sum, bias, non-linearity, the
  vector form $\hat{y} = g(w_0 + \boldsymbol{X}^T \boldsymbol{W})$, and the worked example showing a
  neuron's decision boundary is a line.
- [Activation functions](wiki/activation-functions.md) — why networks need non-linearity; sigmoid, tanh
  and ReLU with their derivatives, ranges and TensorFlow/PyTorch calls; tanh in the RNN state update and
  sigmoid gates; ReLU after every convolution in a CNN.
- [Neural network layers and deep networks](wiki/neural-network-layers.md) — dense (fully connected)
  layers, weight matrices, a hidden layer, stacking into deep networks, and `Dense`/`Linear` and
  `Sequential` code; why flattening an image into dense layers fails.
- [Loss functions](wiki/loss-functions.md) — the loss of a prediction, the empirical loss
  $J(\boldsymbol{W})$, binary cross-entropy for probabilities and mean squared error for continuous
  outputs; per-time-step losses summed over a sequence; softmax over many classes, and the
  negative-log-likelihood loss of lecture 3's driving model; losses without labels: the autoencoder's
  reconstruction loss, the VAE's two terms and the GAN's min-max objective.
- [Gradient descent, learning rates and mini-batches](wiki/gradient-descent.md) — loss optimization,
  the gradient descent algorithm, choosing the learning rate, adaptive optimizers (SGD, Adam, Adadelta,
  Adagrad, RMSProp), stochastic and mini-batch gradient descent.
- [Backpropagation](wiki/backpropagation.md) — computing the gradient with the chain rule, worked on a
  one-neuron-per-layer network, why it propagates backwards, backpropagation through time for RNNs, and
  the reparametrization trick for backpropagating through a VAE's sampling step.
- [Sequence modeling](wiki/sequence-modeling.md) — sequential data, the four input/output shapes of
  sequence tasks, the design criteria a sequence model must meet (worked through next-word prediction),
  and embeddings: vocabulary, indexing, one-hot versus learned; convolutions over sequences.
- [Recurrent neural networks](wiki/recurrent-neural-networks.md) — the internal state and recurrence
  relation $h_t = f_W(x_t, h_{t-1})$, the state-update and output equations, unrolling across time,
  backpropagation through time, exploding and vanishing gradients, gradient clipping, LSTMs and gates,
  and the three limitations of RNNs.
- [Attention and transformers](wiki/attention-and-transformers.md) — why drop recurrence; attention as
  search (query, key, value); self-attention in four steps (positional encoding, Q/K/V, scaled
  dot-product and softmax, weighting the values); attention heads, multiple heads and transformers.
- [Convolutional neural networks](wiki/convolutional-neural-networks.md) — the convolution (filters,
  feature maps, a worked example, hand-written versus learned filters), convolutional layers (depth,
  stride, receptive field), ReLU, max pooling, the learned feature hierarchy, and a CNN for
  classification in code.
- [Computer vision](wiki/computer-vision.md) — what vision is, images as numbers, regression and
  classification, why features must be learned, and the tasks one CNN body serves: classification,
  object detection, semantic segmentation and continuous control.
- [Overfitting and regularization](wiki/regularization.md) — underfitting versus overfitting,
  regularization, dropout (including the per-mini-batch question from class) and early stopping; the
  different sense of regularizing a VAE's latent space.
- [Generative modeling](wiki/generative-modeling.md) — learning a data distribution: supervised versus
  unsupervised learning, density estimation and sample generation, why it is useful (debiasing, outlier
  detection, generative AI), latent variables, and choosing between autoencoders, GANs and diffusion.
- [Autoencoders and VAEs](wiki/autoencoders-and-vaes.md) — the encoder, decoder and reconstruction
  loss; the latent bottleneck; VAEs' mean and standard deviation vectors, $q_{\phi}(z \mid x)$ and
  $p_{\theta}(x \mid z)$, the regularization term and Normal prior, continuity and completeness, the
  reparametrization trick, latent perturbation and β-VAEs.
- [Generative adversarial networks](wiki/generative-adversarial-networks.md) — generator against
  discriminator, the number-line intuition, the min-max objective as printed, training instability,
  GANs as distribution transformers, and CycleGAN.

## Raw materials

- [`raw/slides/`](raw/slides/) — every slide of each transcribed deck, with its text, equations, code
  and a prose description of every figure: [lecture 1](raw/slides/01-introduction.md) (108 slides),
  [lecture 2](raw/slides/02-rnns-transformers-attention.md) (83 slides),
  [lecture 3](raw/slides/03-convolutional-neural-networks.md) (70 slides),
  [lecture 4](raw/slides/04-deep-generative-modeling.md) (84 slides).
- [`raw/transcripts/`](raw/transcripts/) — the lecture transcripts, copy-edited from YouTube captions,
  with `[MM:SS]` paragraph marks and `[Ed: …]` notes where the captions are unclear or differ from a
  slide: [lecture 1](raw/transcripts/01-introduction.md),
  [lecture 2](raw/transcripts/02-rnns-transformers-attention.md),
  [lecture 3](raw/transcripts/03-convolutional-neural-networks.md),
  [lecture 4](raw/transcripts/04-deep-generative-modeling.md). The verbatim captions are in
  `raw/transcripts/original/`.
- [`raw/images/`](raw/images/) — the slide images described above.
- [`sources.md`](sources.md) — every document the course site links, with its canonical URL. The PDFs
  are **not** committed; cite those URLs.
- [`SEE_ALSO.md`](SEE_ALSO.md) — sibling knowledge bases for neighbouring courses.
- [`LICENSE.md`](LICENSE.md) — licence and attribution, including third-party figures on the slides.
