# Overfitting and regularization

A model **overfits** when it learns the details of its training data so closely that it no longer
generalizes to new data. **Regularization** is the family of techniques that counter this. This page
follows MIT 6.S191 [lecture 1](01-introduction.md), section 15 (≈48:38–54:45).

## Underfitting, overfitting, and the ideal fit

Overfitting is "learning too much into your data": fitting details of the training set that do not
generalize outside it. **Underfitting** is the opposite: a model not expressive enough to capture the
data, such as a straight line fitted to a non-linear relationship (lecture 1, slide 93,
≈48:38–49:24). The ideal sits in between, so that on brand-new data — a test set, or deployment — the
model still predicts accurately (≈49:24–50:10).

![Slide 93: The Problem of Overfitting](../raw/images/01-introduction/slide-93.jpg)

*Lecture 1, slide 93 — the same points under an underfitting line, an ideal fit, and an overfitting curve.*

## Regularization

Regularization is a "technique that constrains our optimization problem to discourage complex models",
and we need it to "improve generalization of our model on unseen data" (slides 94–95, ≈50:10). Lecture
1 notes this is how models with billions of parameters avoid simply memorizing their datasets. It
presents two techniques.

## Dropout

During training, randomly set some activations of the hidden layers to zero, with a probability you
choose — typically 50% of a layer (slides 96–98, ≈50:57–52:28). Each neuron then has to cope with
inputs that are sometimes there and sometimes not, so the network is forced not to rely on any single
node or pathway, and has to learn relationships that span many pathways (≈51:42). The slide gives the
layer in both frameworks: `tf.keras.layers.Dropout(p=0.5)` and `torch.nn.Dropout(p=0.5)` (as printed).

![Slide 97: Regularization 1: Dropout](../raw/images/01-introduction/slide-97.jpg)

*Lecture 1, slide 97 — a random subset of hidden units (faded) is dropped for one training iteration; slide 98 drops a different subset.*

A student asked whether the same activations are zeroed across a whole mini-batch. The answer in
lecture 1: yes, the same units are dropped for the entire mini-batch, and a new random set is drawn
for the next one (≈51:42–52:28).

## Early stopping

Early stopping works for any model, because it changes how long you train rather than the
architecture (slides 99–106, ≈52:28–54:45). Hold out a test set separate from the training set, and
evaluate the loss on both throughout training:

- at first both losses fall together, as the model moves from underfitting towards a good fit;
- eventually the training loss keeps improving or plateaus while the test loss starts to rise — the
  model is now overfitting.

Save checkpoints as you go, and keep the one where the test loss was lowest ("stop training here!"):
beyond it, gains on the training data no longer carry over to the test data (≈53:13–54:45).

![Slide 106: Regularization 2: Early Stopping](../raw/images/01-introduction/slide-106.jpg)

*Lecture 1, slide 106 — training (green) and testing (blue) loss: stop at the testing minimum, between under-fitting and over-fitting.*

## Regularizing a latent space

[Lecture 4](04-deep-generative-modeling.md) uses "regularization" for something related but different:
a term in a variational autoencoder's loss that keeps the distribution of its latent variables close to
a Normal prior. Without it the network is unregularized, free to give each input a pointed distribution
or a far-off mean, and to "cheat" by memorizing the data in clustered regions; with it the latent space
stays continuous and complete, so that it can be sampled (lecture 4, slides 27–32, ≈21:47–27:14). See
[autoencoders and VAEs](autoencoders-and-vaes.md).

## Where this comes up

- [Lecture 1 — Introduction to Deep Learning](01-introduction.md), section 15.
- [Lecture 4 — Deep Generative Modeling](04-deep-generative-modeling.md), sections 9–10: the
  regularization term of a VAE.
