# Loss functions

A loss function measures how wrong a network's prediction is. Training a network means finding the
weights that make the loss as small as possible. This page follows MIT 6.S191
[lecture 1](01-introduction.md), section 10 (≈33:16–35:33).

Notation: $f(x^{(i)}; \boldsymbol{W})$ is the network's prediction for the $i$-th example $x^{(i)}$
given weights $\boldsymbol{W}$; $y^{(i)}$ is that example's true answer; $n$ is the number of
examples.

## The loss of one prediction

"The loss of our network measures the cost incurred from incorrect predictions" (lecture 1,
slide 50). It is the deviation between prediction and ground truth, written

$$\mathcal{L}\left(f\left(x^{(i)}; \boldsymbol{W}\right), y^{(i)}\right)$$

Smaller loss means a higher-quality answer, larger loss a more erroneous one (≈33:16). In lecture 1's
running example, an untrained network predicts 0.1 for a student who actually passed (1), and that gap
is what the loss quantifies.

## The empirical loss

Training minimizes the loss not on one example but averaged over the whole dataset (slide 51,
≈34:01). This is the **empirical loss**, also called the objective function, cost function or
empirical risk:

$$J(\boldsymbol{W}) = \frac{1}{n} \sum_{i=1}^{n} \mathcal{L}\left(f\left(x^{(i)}; \boldsymbol{W}\right), y^{(i)}\right)$$

It is one number, and it is a function of the weights, which is what makes it something to minimize
(≈36:18). See [gradient descent](gradient-descent.md).

## Choosing the loss

The right $\mathcal{L}$ depends on what the network outputs (≈34:01–35:33).

**Binary cross-entropy, for probabilities.** For a yes/no question the network outputs a probability
between 0 and 1 — typically through a sigmoid (see [activation functions](activation-functions.md)) —
and cross-entropy compares the predicted and true distributions (slide 52):

$$J(\boldsymbol{W}) = -\frac{1}{n} \sum_{i=1}^{n} y^{(i)} \log\left(f\left(x^{(i)}; \boldsymbol{W}\right)\right) + \left(1 - y^{(i)}\right) \log\left(1 - f\left(x^{(i)}; \boldsymbol{W}\right)\right)$$

![Slide 52: Binary Cross Entropy Loss](../raw/images/01-introduction/slide-52.jpg)

*Lecture 1, slide 52 — predicted probabilities against true labels, and the binary cross-entropy formula.*

**Mean squared error, for continuous values.** To predict a real number — tomorrow's temperature, or
a final grade rather than pass/fail — use a loss on the difference between predicted and true values,
such as the mean squared error (slide 53) or an L1 error (≈34:47–35:33):

$$J(\boldsymbol{W}) = \frac{1}{n} \sum_{i=1}^{n} \left(y^{(i)} - f\left(x^{(i)}; \boldsymbol{W}\right)\right)^2$$

The slides give one-line implementations of each in TensorFlow and PyTorch; they are reproduced in
the [slide transcription](../raw/slides/01-introduction.md) under slides 52 and 53.

## Where this comes up

- [Lecture 1 — Introduction to Deep Learning](01-introduction.md), sections 9–11.
