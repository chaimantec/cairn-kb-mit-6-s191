# Limitations of deep learning

Neural networks are very powerful function approximators, and that power is exactly where their main
limitations come from: they can fit almost anything they are trained on, with no guarantee about what
they do on data unlike their training data. Lecture 6 spends its first half on these limitations — what
the universal approximation theorem does not promise, networks that memorize random labels, behaviour
away from the training data, failures inherited from the data, uncertainty, adversarial attacks and
algorithmic bias — and presents them "from the lens of opportunity": places where new methods are still
needed (lecture 6, ≈27:18). Citations are to [lecture 6](06-language-models-new-frontiers.md) unless
another lecture is named; "slide N" is page N of that lecture's PDF.

## The universal approximation theorem, and what it does not promise

The **universal approximation theorem** (slide 12, credited "Hornik+ *Neural Networks* 1989.") states: "A
feedforward network with a single layer is sufficient to approximate, to an arbitrary precision, any
continuous function." Aloud, Amini puts it as a network with "a single hidden layer" (≈8:40–9:26). It
does not even require depth: if a problem reduces to a mapping from inputs to outputs, one fully
connected layer suffices to approximate it to some precision.

Slide 13 prints the two caveats (≈10:12):

- "The number of hidden units may be infeasibly large." The theorem puts no limit on the size of the
  layer.
- "The resulting model may not generalize." It places no guarantee on generalization — the overfitting
  problem of lecture 1, where low training error coexists with poor test performance (see
  [overfitting and regularization](regularization.md)).

These are the two questions that dominate deep learning today: how large models must be to have
general-purpose capabilities, and whether they generalize to new situations (≈10:58).

## Capacity: fitting random labels

"Understanding Deep Neural Networks Requires Rethinking Generalization" (slides 16–22, credited "Zhang+
*ICLR* 2017.") made the point concrete (≈12:33–15:40). For every ImageNet image — each image, not each
class — the authors rolled a K-sided die, K being the number of classes, and replaced the image's label
with the outcome, so that labels became arbitrary. A deep network trained at increasing degrees of this
randomization did worse and worse on a held-out test set, as expected. But on the training set it made
no difference: trained long enough, the network fit the training examples however random their labels.
Slide 22's red annotation: "Modern deep networks can perfectly fit to random data".

![Slide 22: training accuracy stays at 100% while test accuracy falls](../raw/images/06-language-models-new-frontiers/slide-22.jpg)

*Lecture 6, slide 22 — training accuracy (blue) at 100% at every degree of label randomization; test accuracy (green) falls.*

Amini reads this as the universal approximation principle in practice — with the difference that this is
a deep network and the theorem is about one layer: these models can fit training data to arbitrary
precision, and that by itself says nothing about generalization (≈15:40).

## Away from the training data

Neural networks are "excellent function approximators … when they have training data" (slides 23–28).
Within the distribution of the training data, a network's prediction for a new point is reasonable
(slide 26); Amini describes the network as learning a maximum-likelihood, most likely estimate of the
data within this distribution (≈16:26). Outside it there are no solid theoretical guarantees: slide 27
extends the fitted curve where there is no data and it swings wildly, and slide 28 asks "How do we know
when our network doesn't know?" (≈16:26–17:11).

![Slide 28: the fitted curve away from the data](../raw/images/06-language-models-new-frontiers/slide-28.jpg)

*Lecture 6, slide 28 — where there is no training data (purple arrows), nothing constrains the fitted curve.*

## Garbage in, garbage out

Deep learning is not alchemy (slide 29: "Deep Learning = Alchemy?" "NO!"): there is no machine into which
training data and a random architecture go, a learning algorithm is cranked, and excellent results come
out (≈17:58). The opposite maxim holds — "garbage in, garbage out". A model trained on too little data, on
a problem it does not suit, or mismatched in size to the task may learn its training data and still fail
on test scenarios. Amini's advice: think about the task, its inputs and outputs, the quality of data you
can curate or generate, and whether deep learning is the right approach at all (≈18:44).

The data need not be garbage for this to bite; their distribution is enough (≈19:29):

- **Over-represented examples.** A CNN trained to colorize black-and-white images gives a dog a green ear
  and a reddish tongue (slide 30). The likely reason is that the training set holds many photographs of
  dogs with their tongues out (slide 31), and the model reproduces what the data over-represent
  (≈20:17).
- **Out-of-distribution inputs.** In the fatal autopilot crash of slide 32, the driver had reported the car
  swivelling towards a construction barrier; the barrier was absent from earlier street-view images of the
  location, so it was an out-of-distribution outlier the training data did not contain (≈21:03–21:49).

## Uncertainty

Both lead to **uncertainty**: knowing when a model is confident and when it lacks information and needs a
human (≈21:49–22:37). That matters most in safety-critical applications — autonomous vehicles, medicine,
facial recognition (slide 33) — and in "sparse and/or noisy datasets", where imbalance or noise in the
data creates regions of greater uncertainty in a network's outputs (≈22:37). The course's second software
lab works with these issues, which have algorithmic and data-side remedies (≈23:24). The same question
returns for language models: a generation can be very probable without being high-confidence, and
quantifying the uncertainty of LLMs is an open research problem (≈50:57; see
[large language models](large-language-models.md)).

## Adversarial attacks

An **adversarial example** is an input built to fool a network (≈23:24). On vision models: add to a
natural image a perturbation imperceptible to humans, and the network misclassifies it with high
confidence — slide 34's temple, classified "Temple (97%)", becomes "Ostrich (98%)" (credited "Despois
'Adversarial examples' 2017.").

![Slide 34: temple plus perturbation equals ostrich](../raw/images/06-language-models-new-frontiers/slide-34.jpg)

*Lecture 6, slide 34 — an imperceptible perturbation changes the class from temple to ostrich.*

The construction inverts training (slides 36–41, ≈24:58–25:45). [Gradient descent](gradient-descent.md)
holds the image $x$ and its true label $y$ fixed and changes the weights $W$ to *decrease* the loss $J$,
with learning rate $\eta$:

$$W \leftarrow W - \eta \frac{\partial J(W, x, y)}{\partial W}$$

An adversarial image holds the weights and the label fixed and changes the input to *increase* the loss
(slide 39, credited "Goodfellow+ *NIPS* 2014."):

$$x \leftarrow x + \eta \frac{\partial J(W, x, y)}{\partial x}$$

The slides pair the two with "How does a small change in weights decrease our loss" and "How does a small
change in the input increase our loss". (Slide 41's callout names the fixed weights $\boldsymbol{\theta}$,
though its formula writes $W$.) The attack also works on physical objects: slide 42 (credited "Athalye+
*ICML* 2018.") shows a 3D-printed turtle, photographed from 24 viewpoints, classified as a rifle in 17 of
them (≈25:45–26:31). For language models the equivalent is the **jailbreak**, which probes a model to
expose these adversarial failure modes (≈23:24, ≈51:43).

## Algorithmic bias

**Algorithmic bias** is "a very real and severe limitation" for safety, fairness and ethics (slide 43, a
wall of news headlines on racial and gender bias in AI systems; ≈26:31). The course's facial detection lab
deals with it hands-on; lecture 4 describes how a generative model of the data can help build fairer
datasets and models (see [generative modeling](generative-modeling.md)).

## The list, and the opportunities

Slide 44 collects the limitations of neural networks: very data hungry (often millions of examples);
computationally intensive to train and deploy; easily fooled by adversarial examples; subject to
algorithmic bias; poor at representing uncertainty ("how do you know what the model knows?");
uninterpretable black boxes, difficult to trust; often requiring expert knowledge to design and fine-tune
architectures; difficult to encode structure and prior knowledge during learning; and poor at
extrapolation, struggling "to go beyond the data". The list is "not comprehensive at all", and each item
is an opportunity for new methods (≈27:18).

The second half of lecture 6 turns to advances that push past some of these, especially generalization:
scaling data and models has produced **emergent capabilities** that generalize far better than before
(≈28:04–28:50). See [diffusion models](diffusion-models.md) and
[large language models](large-language-models.md), whose own limitations — robustness and confidence,
hallucination, jailbreaks, long-term planning and logic — are listed on slide 74 (≈50:10–51:43).

## Where this comes up

- [Lecture 6 — Language Models and New Frontiers](06-language-models-new-frontiers.md), sections 3–11 and 25.
- [Lecture 1 — Introduction to Deep Learning](01-introduction.md): overfitting, which the theorem's second
  caveat recalls.
- [Lecture 4 — Deep Generative Modeling](04-deep-generative-modeling.md): debiasing and outlier detection
  with generative models.
