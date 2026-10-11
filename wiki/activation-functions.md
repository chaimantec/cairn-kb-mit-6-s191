# Activation functions

An activation function $g$ is the non-linear function a neuron applies after its weighted sum:
$\hat{y} = g(z)$, where $z = w_0 + \boldsymbol{X}^T \boldsymbol{W}$ is the dot product of the inputs
$\boldsymbol{X}$ with the weights $\boldsymbol{W}$ plus the bias $w_0$ (see
[the perceptron](perceptron.md)). It maps any real number to a new real number, sometimes bounded and
sometimes not, by a transformation that is not linear ([lecture 1](01-introduction.md), ≈17:53–18:40).

## Why networks need them

"The purpose of activation functions is to introduce non-linearities into the network" (lecture 1,
slides 26–28, ≈19:26–20:59). Real-world data is non-linear: lecture 1's example is a two-dimensional set
of red and green points that no straight line can separate. A network whose activations are linear
can only ever draw a straight decision boundary, "no matter the network size"; with non-linear
activations it can draw curves, and "non-linearities allow us to approximate arbitrarily complex
functions".

![Slide 28: Importance of Activation Functions](../raw/images/01-introduction/slide-28.jpg)

*Lecture 1, slide 28 — a linear decision boundary (left) against a non-linear one (right) on the same points.*

## Common choices

Lecture 1, slide 25, shows three, each with its derivative $g'(z)$, which training needs (see
[backpropagation](backpropagation.md)):

| Function | $g(z)$ | $g'(z)$ | Output range | TensorFlow / PyTorch (as on the slide) |
| --- | --- | --- | --- | --- |
| Sigmoid | $\frac{1}{1 + e^{-z}}$ | $g(z)(1 - g(z))$ | 0 to 1 | `tf.math.sigmoid(z)` / `torch.sigmoid(z)` |
| Hyperbolic tangent | $\frac{e^{z} - e^{-z}}{e^{z} + e^{-z}}$ | $1 - g(z)^2$ | −1 to 1 | `tf.math.tanh(z)` / `torch.tanh(z)` |
| ReLU (rectified linear unit) | $\max(0, z)$ | 1 if $z \gt 0$, else 0 | 0 to ∞ | `tf.nn.relu(z)` / `torch.nn.ReLU(z)` |

![Slide 25: Common Activation Functions](../raw/images/01-introduction/slide-25.jpg)

*Lecture 1, slide 25 — sigmoid, tanh and ReLU (blue) with their derivatives (orange).*

What each is good for, as lecture 1 puts it (≈18:40–19:26):

- The **sigmoid** is "very commonly used for things like probabilities", because its output always
  lies between 0 and 1. It is why a yes/no classifier can output the probability of "yes" (see
  [loss functions](loss-functions.md)).
- **ReLU** outputs between zero and infinity, useful for non-negativity constraints, and is simple:
  "just two linear functions with a non-linearity between them".

The note at the bottom of slide 25 is the unifying point: all activation functions are non-linear.

## Where this comes up

- [Lecture 1 — Introduction to Deep Learning](01-introduction.md), section 6.
