# What is deep learning?

Deep learning is the part of machine learning that uses neural networks — specifically deep ones — to
learn a task directly from raw data. MIT 6.S191 frames the whole course around that one sentence:
"teaching computers how to learn a task directly from raw data"
([lecture 1](01-introduction.md), slide 7, ≈9:22).

## AI, machine learning, deep learning

The three terms nest inside one another ([lecture 1](01-introduction.md), slide 7, ≈7:47–9:22):

- **Intelligence**, as Alexander Amini defines it, is processing information in order to inform some
  future decision. **Artificial intelligence** is a machine doing the same; slide 7 puts it as "any
  technique that enables computers to mimic human behavior".
- **Machine learning** is the subset of AI that does this *without being explicitly programmed* with
  the steps: it learns how to process the information from data. That is the dividing line between ML
  and AI in general.
- **Deep learning** is the subset of ML that does the learning with neural networks — "extract
  patterns from data using neural networks".

![Slide 7: What is Deep Learning?](../raw/images/01-introduction/slide-7.jpg)

*Lecture 1, slide 7 — artificial intelligence ⊃ machine learning ⊃ deep learning.*

[Lecture 6](06-language-models-new-frontiers.md) adds a level inside deep learning: **large language
models**, "Very, very large neural networks trained on very, very large sets of text" (slide 69,
≈44:07). See [large language models](large-language-models.md).

## Why learn features instead of engineering them?

Traditional machine learning relies on features designed by hand, which lecture 1 calls "time
consuming, brittle, and not scalable in practice" (slide 18, ≈12:30). Deep learning instead learns the
features from data, and learns them as a **hierarchy**: low-level lines and edges are composed into
mid-level parts such as eyes, noses and ears, and those into high-level structure such as a whole face
(slide 18, ≈13:16–14:03). This mirrors how a person might reason from first principles about whether
an image contains a face.

[Lecture 3](03-convolutional-neural-networks.md) makes the same argument for vision (slides 14–18,
≈7:00–11:39). Classification is done by detecting lower-level features and composing them, but defining
those features by hand fails because images vary so much: in viewpoint, illumination, scale,
deformation, background clutter, occlusion, and within a class. Humans "are just not very good at
clearly defining what those lower-level features should be" (≈10:05). A network instead learns the
hierarchy through its depth. In a convolutional network the layers learn edges and dark spots, then eyes,
ears and noses, then facial structure (slide 50, ≈37:49; see
[convolutional neural networks](convolutional-neural-networks.md)).

## Supervised, unsupervised and reinforcement learning

The networks of lectures 1–3 learn by **supervised learning**: from pairs $(x, y)$ of data and label,
they learn a function mapping $x \rightarrow y$. In **unsupervised learning** there are only the data
$x$, and the goal is to learn their hidden or underlying structure ([lecture 4](04-deep-generative-modeling.md),
slides 3–4, ≈2:25–3:57). [Generative modeling](generative-modeling.md) is the course's way into it.

**Reinforcement learning** has neither labels nor a pre-collected dataset: an agent acts in an
environment, its data — states, actions and rewards — are collected while it learns, and the goal is to
"Maximize future rewards over many time steps" ([lecture 5](05-reinforcement-learning.md), slides 4–6,
≈0:52 and ≈2:24–4:42). Lecture 5's apple example puts the three side by side: "This thing is an apple",
"This thing is like the other thing", and "Eat this thing because it will keep you alive". See
[reinforcement learning](reinforcement-learning.md).

## Why now?

The building blocks are decades old. Lecture 1's timeline (slide 19) dates stochastic gradient descent
to 1952, the perceptron to 1958, backpropagation to 1986 and deep convolutional networks for digit
recognition to 1995. Their recent dominance comes from three things (≈14:03–15:37):

1. **Big data**: larger datasets that are easier to collect and store, and these algorithms "live off
   of data".
2. **Hardware**: GPUs, which make the computation massively parallel.
3. **Software**: improved techniques, new models, and toolboxes such as TensorFlow and PyTorch that
   democratize building, training and deploying models.

It was not always so. Lecture 6's slide 14 draws AI's popularity as waves: "Birth" in 1956, "Inflated
Hype" in 1974, "AI winter I" in 1980, "New Hopes" in 1987, "AI winter II" in 1993, then "Explosive
Growth". There were times when these models were under heavy scrutiny from the scientific community, and
like any technology, deep learning goes through waves of growth and of criticism (≈10:58–12:33).

Lecture 7's guest lecturer, Douglas Blank, tells the same history as a sequence of ideas (lecture 7,
≈7:09–11:47; slides 11–16). After the term "artificial intelligence" was coined in 1956, the first
decades were dominated by symbolic reasoning, rules of the form "if this, then that". From the 1970s
came expert systems, symbolic systems made domain-specific. Then the field moved "away from symbols and
into numbers", toward machine learning and statistics (slide 11 tables the dominant funded areas by
decade).

He lived through the second AI winter as a neural-network researcher. He finished his PhD in 1997, sent
out a hundred job applications and got very few responses, in a field that did not yet accept neural
networks as AI. His 2005 talk "A Tale of Two AIs" set formal, discrete, rule-based systems against
informal, real-valued, distributed ones (slides 13–14).

His reasons for the 2010–2017 breakthrough overlap lecture 1's (slide 15). Data got huge, GPUs got fast,
networks got deeper, and algorithms got better (automatic differentiation). Industry invested heavily,
and breakthroughs arrived in every major domain at once. Since 2017 the big impact rests on the
transformer (≈11:47; slide 16).

## Where this comes up

- [Lecture 1 — Introduction to Deep Learning](01-introduction.md), sections 1, 2 and 4: the pace of
  the field, the definitions, and why deep learning works now.
- [Lecture 3 — Convolutional Neural Networks](03-convolutional-neural-networks.md), sections 3 and 15:
  hand-engineered versus learned visual features, and the hierarchy a CNN learns.
- [Lecture 4 — Deep Generative Modeling](04-deep-generative-modeling.md), section 2: supervised versus
  unsupervised learning.
- [Lecture 5 — Reinforcement Learning](05-reinforcement-learning.md), section 2: reinforcement
  learning as the third class of learning problems.
- [Lecture 6 — Language Models and New Frontiers](06-language-models-new-frontiers.md), sections 2, 4 and 21:
  data to decision and back, AI's waves of hype, and LLMs as a class of deep learning.
- [Lecture 7 — The Three Laws of AI](07-three-laws-of-ai.md), sections 4–7: AI history from symbolic
  reasoning to deep learning, and the AI winter as a neural-network researcher saw it.
- The building block every later idea rests on is the [perceptron](perceptron.md).
