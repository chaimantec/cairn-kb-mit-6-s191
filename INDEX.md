# MIT 6.S191 — Introduction to Deep Learning

MIT's one-week introductory boot camp on deep learning, taught by Alexander Amini and Ava Amini, with
lectures, hands-on software labs in TensorFlow and PyTorch, and a project pitch competition. It runs
from the foundations of neural networks — the single neuron, training by gradient descent and
backpropagation — up to recent advances in large language models. Course site:
<https://introtodeeplearning.com/>.

**Coverage: lectures 1–8 only.** This knowledge base covers **lectures 1–8 of the 2026 edition**:
"Introduction to Deep Learning" (Alexander Amini) and "Recurrent Neural Networks, Transformers, and
Attention" (Ava Amini), both delivered 5 January 2026, and "Convolutional Neural Networks" (Alexander
Amini; the deck's title is "Deep Computer Vision") and "Deep Generative Modeling" (Ava Amini), both
delivered 6 January 2026, and "Reinforcement Learning" (Alexander Amini; the deck's title is "Deep
Reinforcement Learning") and "Language Models and New Frontiers" (Ava Amini; the deck's title is "Deep
Learning Limitations and New Frontiers"), both delivered 7 January 2026, and two guest lectures: "AI for
Science" (Chris Bishop, Microsoft Research AI for Science), delivered 8 January 2026, and "The Three Laws
of AI" (Douglas Blank, Comet ML), delivered 9 January 2026. The Cairn catalog for this course lists 90
recordings — the 2026 edition's lectures (positions 1–9) followed by the 2018–2025 editions — and none
of the others is in this KB yet.
Do not cite it as the whole course: for any other lecture — the 2026 guest lecture at position 9 or any
earlier edition — say it is not covered. Vision transformers, which lecture 2 says
lecture 3 will cover, are not discussed in lecture 3.

## How to use this knowledge base

- Start from the lecture page or the topic page below. Lecture pages follow the lecture in order, with
  timestamps such as (≈24:10) into the transcript and slide citations.
- **"Slide N" means page N of the PDF.** The decks of lectures 1–6 and 8 print no slide numbers; lecture
  7's deck prints them, and they equal the page numbers.
- For exact wording, numbers, code and equations as printed, read the slide transcription in
  `raw/slides/`. For what was said, read the copy-edited transcript in `raw/transcripts/` (not the
  verbatim captions in `raw/transcripts/original/`, which are kept only as a reference).

## Images

All eight lectures have slide images: **34 for lecture 1**, **33 for lecture 2**, **33 for lecture
3**, **39 for lecture 4**, **19 for lecture 5**, **24 for lecture 6**, **4 for lecture 7** and **18 for
lecture 8**. Each is embedded where it is used: in the lecture page
([lecture 1](wiki/01-introduction.md), [lecture 2](wiki/02-rnns-transformers-attention.md),
[lecture 3](wiki/03-convolutional-neural-networks.md), [lecture 4](wiki/04-deep-generative-modeling.md),
[lecture 5](wiki/05-reinforcement-learning.md), [lecture 6](wiki/06-language-models-new-frontiers.md),
[lecture 7](wiki/07-three-laws-of-ai.md), [lecture 8](wiki/08-ai-for-science.md))
beside the passage that cites the slide, in some topic pages, and under the matching `## Slide N`
heading of the slide transcription ([lecture 1](raw/slides/01-introduction.md),
[lecture 2](raw/slides/02-rnns-transformers-attention.md),
[lecture 3](raw/slides/03-convolutional-neural-networks.md),
[lecture 4](raw/slides/04-deep-generative-modeling.md),
[lecture 5](raw/slides/05-reinforcement-learning.md),
[lecture 6](raw/slides/06-language-models-new-frontiers.md),
[lecture 7](raw/slides/07-three-laws-of-ai.md),
[lecture 8](raw/slides/08-ai-for-science.md)).
They are whole slides, every one that carries a distinct figure; slides without an image are text, code
or tables the transcription reproduces exactly, logistics, logos, portraits, stock photographs, video
stills, screenshots of text, journal and book covers, repeats of a rendered figure, or build steps
contained in a rendered slide. Lecture 7's deck is mostly text, so it has four images: a timeline, a
chart and two screenshots of the Opik platform. No other lecture is in this KB, so no other lecture has
images.

- **Use an image path you have actually read in a file. Never construct one from the pattern**, and
  never assume a slide has an image because a neighbouring slide does. Reading an image path returns
  its displayable URL.
- Prefer the slide transcription for numbers and code; the images are 1280×720 (lectures 7 and 8,
  1400×788).
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
- [Lecture 5 — Reinforcement Learning](wiki/05-reinforcement-learning.md) — the whole lecture in order:
  learning in dynamic environments; supervised, unsupervised and reinforcement learning (the apple
  example); agent, environment, actions and action space, states, rewards, the return and discounting;
  the Q-function and the policy; value versus policy learning; the Atari Breakout A-or-B puzzle; deep Q
  networks, the training target and the Q-loss; DQN on 49 Atari games; downsides of Q-learning; policy
  gradients, discrete and continuous action spaces and a Gaussian policy; the self-driving training
  algorithm, the policy-gradient loss and update, exploration versus exploitation; why real-world
  training needs simulation (VISTA); AlphaGo; preference alignment of language models.
- [Lecture 6 — Language Models and New Frontiers](wiki/06-language-models-new-frontiers.md) — the whole
  lecture in order: the universal approximation theorem and its caveats; AI's waves of hype; networks that
  fit randomly labelled data; function approximation away from the training data; "garbage in, garbage
  out", colorization and autopilot failures, uncertainty; adversarial attacks and the adversarial-image
  update; algorithmic bias and the list of limitations; diffusion models: one-shot versus iterative
  generation, forward noising, reverse denoising and its loss, sampling, text conditioning, molecular
  design; large language models: tokens, next-token prediction and cross-entropy, from base model to
  chatbot, capabilities, limitations and emergent abilities with scale.
- [Lecture 7 — The Three Laws of AI](wiki/07-three-laws-of-ai.md) — Douglas Blank's guest lecture, in
  order: Asimov's Three Laws of Robotics restated for AI, and the 1956 hope of writing them as code; AI
  history from symbolic reasoning and expert systems to statistics and deep learning, and the AI winter
  ("A Tale of Two AIs"); the Opik platform; a live jailbreak challenge (a system prompt hiding a password);
  messages, chat prompts, traces, spans and projects; datasets, metrics, experiments and LLM-as-a-judge;
  four models compared on a 123-item jailbreak dataset; prompt optimization; safety drift in long
  conversations (the Sam Nelson case) and eight recommendations; agents, and building one from tools in 90
  seconds; modern laws of AI, version 1 (from regulations) and version 2 (practices), with law 0 and law −1.
- [Lecture 8 — AI for Science](wiki/08-ai-for-science.md) — Chris Bishop's guest lecture, in order: the
  world described by simple, precise equations (the electron's magnetic moment) that Dirac said cannot be
  solved; the scientific discovery loop and AI emulators as a third oracle; the no free lunch theorem,
  inductive bias (invariance, equivariance, conservation laws) and the bitter lesson; deep learning
  emulators and their benefits; weather and pollution with Aurora; MatterGen, conditional diffusion for
  crystals; the accuracy–speed–generality trilemma and chemical accuracy; the wave function's curse of
  dimensionality; density functional theory, the exchange-correlation functional, the DFT zoo and the
  learned Skala functional; sequence, structure and function; molecular dynamics, the curse of
  sequentiality and protein emulators; his book; questions on protein dynamics, data augmentation and
  simulated versus real data.

### Topics

- [What is deep learning?](wiki/what-is-deep-learning.md) — AI, machine learning and deep learning
  defined and nested; learned hierarchical features versus hand-engineered ones, including lecture 3's
  case for vision; supervised, unsupervised and reinforcement learning; why now (big data, hardware, software),
  the 1952–1995 timeline and lecture 6's waves of AI hype; lecture 7's history from symbolic AI and expert
  systems to statistics and deep learning, and the AI winter; LLMs as a class of deep learning.
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
  reconstruction loss, the VAE's two terms and the GAN's min-max objective; the Q-loss and the
  policy-gradient loss of reinforcement learning; the cross-entropy of next-token prediction and the
  denoising loss of diffusion models.
- [Gradient descent, learning rates and mini-batches](wiki/gradient-descent.md) — loss optimization,
  the gradient descent algorithm, choosing the learning rate, adaptive optimizers (SGD, Adam, Adadelta,
  Adagrad, RMSProp), stochastic and mini-batch gradient descent; the policy-gradient update; the same
  update turned on the input to make adversarial examples.
- [Backpropagation](wiki/backpropagation.md) — computing the gradient with the chain rule, worked on a
  one-neuron-per-layer network, why it propagates backwards, backpropagation through time for RNNs, and
  the reparametrization trick for backpropagating through a VAE's sampling step.
- [Sequence modeling](wiki/sequence-modeling.md) — sequential data, the four input/output shapes of
  sequence tasks, the design criteria a sequence model must meet (worked through next-word prediction),
  and embeddings: vocabulary, indexing, one-hot versus learned; convolutions over sequences; next-token
  prediction in large language models.
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
  object detection, semantic segmentation and continuous control; colorization failures and adversarial
  examples.
- [Overfitting and regularization](wiki/regularization.md) — underfitting versus overfitting,
  regularization, dropout (including the per-mini-batch question from class) and early stopping; the
  different sense of regularizing a VAE's latent space; networks that perfectly fit random labels.
- [Generative modeling](wiki/generative-modeling.md) — learning a data distribution: supervised versus
  unsupervised learning, density estimation and sample generation, why it is useful (debiasing, outlier
  detection, generative AI), latent variables, and choosing between autoencoders, GANs and diffusion
  models.
- [Autoencoders and VAEs](wiki/autoencoders-and-vaes.md) — the encoder, decoder and reconstruction
  loss; the latent bottleneck; VAEs' mean and standard deviation vectors, $q_{\phi}(z \mid x)$ and
  $p_{\theta}(x \mid z)$, the regularization term and Normal prior, continuity and completeness, the
  reparametrization trick, latent perturbation and β-VAEs.
- [Generative adversarial networks](wiki/generative-adversarial-networks.md) — generator against
  discriminator, the number-line intuition, the min-max objective as printed, training instability,
  GANs as distribution transformers, and CycleGAN.
- [Reinforcement learning](wiki/reinforcement-learning.md) — the third learning paradigm: agent,
  environment, actions, states and rewards; the return and the discount factor; the Q-function and the
  policy; value versus policy learning; exploration versus exploitation; simulation and VISTA; Atari,
  self-driving, Go and AlphaGo, and the preference alignment of language models.
- [Q-learning and deep Q networks](wiki/q-learning.md) — the Q-function and the argmax policy, the
  Breakout puzzle, the two DQN architectures, the target, prediction and Q-loss, acting, DQN on Atari,
  and Q-learning's downsides (discrete actions only, no stochastic policies).
- [Policy gradients](wiki/policy-gradients.md) — a network that outputs a distribution over actions
  and samples from it; continuous actions with a Gaussian policy; the five-step training algorithm; the
  loss $-\log P(a_t|s_t)\thinspace R_t$ and the policy-gradient update; exploration; training in simulation.
- [Limitations of deep learning](wiki/limitations-of-deep-learning.md) — the universal approximation theorem
  and its two caveats; fitting random labels; behaviour away from the training data; garbage in, garbage
  out; over-represented and out-of-distribution data; uncertainty; adversarial examples and the update
  that makes them; algorithmic bias; the slide's list of limitations, and those of LLMs.
- [Diffusion models](wiki/diffusion-models.md) — why move beyond VAEs and GANs; one-shot versus iterative
  generation; forward noising and reverse denoising; training by predicting the noise; sampling new data;
  whether the noise is really noise; conditioning on text; molecules and proteins; MatterGen's conditional
  diffusion for crystals.
- [Large language models](wiki/large-language-models.md) — LLMs as very large networks trained on very
  large text; data and tokens; next-token prediction and its cross-entropy loss; base model to chatbot;
  capabilities and limitations (hallucination, jailbreaks, confidence, planning); system and user prompts,
  a live jailbreak and four models compared, and tools; emergent abilities with scale; foundation models.

- [AI safety](wiki/ai-safety.md) — Asimov's laws and why they could not be coded; what goes wrong
  (adversarial examples, bias, jailbreaks, safety drift in long conversations, agents acting on mistakes);
  preference alignment; the eight recommendations against safety drift; lecture 7's modern laws of AI,
  versions 1 and 2, with law 0 ("If you can't guarantee safety and security, don't deploy it") and law −1.
- [Evaluating LLMs](wiki/llm-evaluation.md) — messages, chat prompts, traces, spans and projects;
  turning informal testing into experiments with a dataset and a metric; the password-jailbreak worked
  example; LLM-as-a-judge; comparing models (GPT-4o Mini 78%, GPT-4o 94%, GPT-5 100%); prompt
  optimization; testing long conversations.
- [AI agents](wiki/ai-agents.md) — an AI agent as "a software system that can do things on behalf of the
  user"; why an LLM needs tools; building one from Python functions in 90 seconds; why agents must be
  tested and traced; how this differs from the agent of reinforcement learning.
- [AI for science](wiki/ai-for-science.md) — deep learning emulators: why known equations cannot be
  solved, the no free lunch theorem and inductive bias in science, the bitter lesson, training on
  simulator data and its benefits, the accuracy–speed–generality trilemma, and lecture 8's examples:
  Aurora, MatterGen, density functional theory with the Skala functional, and protein dynamics.

## Raw materials

- [`raw/slides/`](raw/slides/) — every slide of each transcribed deck, with its text, equations, code
  and a prose description of every figure: [lecture 1](raw/slides/01-introduction.md) (108 slides),
  [lecture 2](raw/slides/02-rnns-transformers-attention.md) (83 slides),
  [lecture 3](raw/slides/03-convolutional-neural-networks.md) (70 slides),
  [lecture 4](raw/slides/04-deep-generative-modeling.md) (84 slides),
  [lecture 5](raw/slides/05-reinforcement-learning.md) (58 slides),
  [lecture 6](raw/slides/06-language-models-new-frontiers.md) (81 slides),
  [lecture 7](raw/slides/07-three-laws-of-ai.md) (44 slides),
  [lecture 8](raw/slides/08-ai-for-science.md) (31 slides).
- [`raw/transcripts/`](raw/transcripts/) — the lecture transcripts, copy-edited from YouTube captions,
  with `[MM:SS]` paragraph marks and `[Ed: …]` notes where the captions are unclear or differ from a
  slide: [lecture 1](raw/transcripts/01-introduction.md),
  [lecture 2](raw/transcripts/02-rnns-transformers-attention.md),
  [lecture 3](raw/transcripts/03-convolutional-neural-networks.md),
  [lecture 4](raw/transcripts/04-deep-generative-modeling.md),
  [lecture 5](raw/transcripts/05-reinforcement-learning.md),
  [lecture 6](raw/transcripts/06-language-models-new-frontiers.md),
  [lecture 7](raw/transcripts/07-three-laws-of-ai.md),
  [lecture 8](raw/transcripts/08-ai-for-science.md). The verbatim captions are in
  `raw/transcripts/original/`.
- [`raw/images/`](raw/images/) — the slide images described above.
- [`sources.md`](sources.md) — every document the course site links, with its canonical URL. The PDFs
  are **not** committed; cite those URLs.
- [`SEE_ALSO.md`](SEE_ALSO.md) — sibling knowledge bases for neighbouring courses.
- [`LICENSE.md`](LICENSE.md) — licence and attribution, including third-party figures on the slides.
