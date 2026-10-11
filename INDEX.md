# MIT 6.S191 — Introduction to Deep Learning

MIT's one-week introductory boot camp on deep learning, taught by Alexander Amini and Ava Amini, with
lectures, hands-on software labs in TensorFlow and PyTorch, and a project pitch competition. It runs
from the foundations of neural networks — the single neuron, training by gradient descent and
backpropagation — up to recent advances in large language models. Course site:
<https://introtodeeplearning.com/>.

**Coverage: lecture 1 only.** This knowledge base covers **lecture 1 of the 2026 edition**
("Introduction to Deep Learning", Alexander Amini, 5 January 2026). The Cairn catalog for this course
lists 90 recordings — the 2026 edition's lectures (positions 1–9) followed by the 2018–2025 editions —
and none of the others is in this KB yet. Do not cite it as the whole course: for any other lecture,
say it is not covered.

## How to use this knowledge base

- Start from the lecture page or the topic page below. Lecture pages follow the lecture in order, with
  timestamps such as (≈24:10) into the transcript and slide citations.
- **"Slide N" means page N of the PDF.** The decks print no slide numbers.
- For exact wording, numbers, code and equations as printed, read the slide transcription in
  `raw/slides/`. For what was said, read the copy-edited transcript in `raw/transcripts/` (not the
  verbatim captions in `raw/transcripts/original/`, which are kept only as a reference).

## Images

Lecture 1 has **34 slide images**, embedded where they are used: in [the lecture page](wiki/01-introduction.md)
beside the passage that cites each slide, in the topic pages, and under the matching `## Slide N`
heading of [the slide transcription](raw/slides/01-introduction.md). They are whole slides, every one
that carries a distinct figure; slides without an image are text, code or tables the transcription
reproduces exactly, logistics, logos, or build steps contained in a later rendered slide.

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

### Topics

- [What is deep learning?](wiki/what-is-deep-learning.md) — AI, machine learning and deep learning
  defined and nested; learned hierarchical features versus hand-engineered ones; why now (big data,
  hardware, software) and the 1952–1995 timeline.
- [The perceptron](wiki/perceptron.md) — the single neuron: weighted sum, bias, non-linearity, the
  vector form $\hat{y} = g(w_0 + \boldsymbol{X}^T \boldsymbol{W})$, and the worked example showing a
  neuron's decision boundary is a line.
- [Activation functions](wiki/activation-functions.md) — why networks need non-linearity; sigmoid, tanh
  and ReLU with their derivatives, ranges and TensorFlow/PyTorch calls.
- [Neural network layers and deep networks](wiki/neural-network-layers.md) — dense (fully connected)
  layers, weight matrices, a hidden layer, stacking into deep networks, and `Dense`/`Linear` and
  `Sequential` code.
- [Loss functions](wiki/loss-functions.md) — the loss of a prediction, the empirical loss
  $J(\boldsymbol{W})$, binary cross-entropy for probabilities and mean squared error for continuous
  outputs.
- [Gradient descent, learning rates and mini-batches](wiki/gradient-descent.md) — loss optimization,
  the gradient descent algorithm, choosing the learning rate, adaptive optimizers (SGD, Adam, Adadelta,
  Adagrad, RMSProp), stochastic and mini-batch gradient descent.
- [Backpropagation](wiki/backpropagation.md) — computing the gradient with the chain rule, worked on a
  one-neuron-per-layer network, and why it propagates backwards.
- [Overfitting and regularization](wiki/regularization.md) — underfitting versus overfitting,
  regularization, dropout (including the per-mini-batch question from class) and early stopping.

## Raw materials

- [`raw/slides/`](raw/slides/) — every slide of each transcribed deck, with its text, equations, code
  and a prose description of every figure: [lecture 1](raw/slides/01-introduction.md) (108 slides).
- [`raw/transcripts/`](raw/transcripts/) — the lecture transcripts, copy-edited from YouTube captions,
  with `[MM:SS]` paragraph marks and `[Ed: …]` notes where the captions are unclear or differ from a
  slide: [lecture 1](raw/transcripts/01-introduction.md). The verbatim captions are in
  `raw/transcripts/original/`.
- [`raw/images/`](raw/images/) — the slide images described above.
- [`sources.md`](sources.md) — every document the course site links, with its canonical URL. The PDFs
  are **not** committed; cite those URLs.
- [`SEE_ALSO.md`](SEE_ALSO.md) — sibling knowledge bases for neighbouring courses.
- [`LICENSE.md`](LICENSE.md) — licence and attribution, including third-party figures on the slides.
