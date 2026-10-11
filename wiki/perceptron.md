# The perceptron (a single neuron)

The perceptron is a single artificial neuron, and MIT 6.S191 treats it as "the structural building
block of deep learning" (lecture 1, slide 20). Alexander Amini asks students to remember one thing from
the class if nothing else: a neuron does three steps — **a dot product, add a bias, apply a
non-linearity** ([lecture 1](01-introduction.md), ≈24:02–24:48).

## Forward propagation

A perceptron takes $m$ inputs $x_1, \dots, x_m$. Each input has its own weight $w_1, \dots, w_m$.
The neuron multiplies every input by its weight, adds up the products, adds a **bias** $w_0$, and
passes the result through a non-linear **activation function** $g$ to produce one output $\hat{y}$
(lecture 1, slides 21–22, ≈15:37–17:08):

$$\hat{y} = g\left(w_0 + \sum_{i=1}^{m} x_i w_i\right)$$

The bias is drawn as a weight on a constant input of 1; it lets the neuron shift its function up or
down (≈17:08).

![Slide 22: The Perceptron: Forward Propagation](../raw/images/01-introduction/slide-22.jpg)

*Lecture 1, slide 22 — inputs, weights, sum, non-linearity and output, with the bias weight* $w_0$ *on a constant input of 1.*

Writing the inputs and weights as vectors $\boldsymbol{X} = [x_1, \dots, x_m]^T$ and
$\boldsymbol{W} = [w_1, \dots, w_m]^T$ turns the sum into a dot product (slide 23, ≈17:53):

$$\hat{y} = g\left(w_0 + \boldsymbol{X}^T \boldsymbol{W}\right)$$

The course's simplified notation names the value before the non-linearity $z$, so that
$z = w_0 + \sum_{j=1}^{m} x_j w_j$ and the output is $y = g(z)$ (slide 35, ≈25:35).

## Why the non-linearity matters

Without $g$, a neuron is just a weighted sum, and stacking weighted sums only ever produces linear
decisions, "no matter the network size" (lecture 1, slide 27). Real data is non-linear, so the
activation function is what lets networks represent complex boundaries. See
[activation functions](activation-functions.md).

## A neuron is a line

Lecture 1 works an example with $w_0 = 1$, $w_1 = 3$, $w_2 = -2$ (slides 29–32, ≈20:59–24:02). The
neuron computes $\hat{y} = g(1 + 3x_1 - 2x_2)$, and the expression inside $g$ is a line in the plane of
the two inputs. That line, $1 + 3x_1 - 2x_2 = 0$, is the neuron's **decision boundary**:

- the input $[-1, 2]$ gives $1 + (3 \ast -1) - (2 \ast 2) = -6$, and $g(-6) \approx 0.002$ for a
  sigmoid $g$;
- every input on that side of the line has $z \lt 0$ and a sigmoid output below 0.5, and every input
  on the other side has $z \gt 0$ and an output above 0.5.

This visual intuition only works with two parameters; real networks have billions, which is why the
course moves on to building mathematical intuition instead (≈23:16–24:02).

## From neurons to networks

Several neurons sharing the same inputs form a layer, layers stack into networks, and many stacked
layers make a deep network. See [neural network layers](neural-network-layers.md).

## Where this comes up

- [Lecture 1 — Introduction to Deep Learning](01-introduction.md), sections 5, 7 and 8.
