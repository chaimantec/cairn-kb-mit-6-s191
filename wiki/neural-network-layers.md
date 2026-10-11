# Neural network layers and deep networks

A neural network is built by putting [perceptrons](perceptron.md) side by side into **layers** and
stacking layers one after another. A **deep** neural network is simply one with many stacked layers.
This page follows the build-up in MIT 6.S191 [lecture 1](01-introduction.md), section 8
(≈24:02–30:55).

Notation, as in the course: $x_j$ are the inputs, $z_i$ the value of unit $i$ before its activation
function $g$, $w_{j,i}$ the weight from input $j$ to unit $i$, $w_{0,i}$ unit $i$'s bias, and a
superscript $(k)$ marks the layer a weight belongs to.

## Dense (fully connected) layers

Two neurons can see the same inputs while having their own independent weights, and so produce two
different outputs (lecture 1, ≈25:35). Because every input connects to every output, such a layer is
called **dense** (slide 36):

$$z_i = w_{0,i} + \sum_{j=1}^{m} x_j w_{j,i}, \qquad y_i = g(z_i)$$

Implementing one from scratch (slide 37, ≈25:35–27:06) means initializing a weight matrix of size
(input dimension × output dimension) and a bias, then, in the forward pass, multiplying the inputs by
the weights, adding the bias and applying the non-linearity. Both frameworks already provide it: a
`Dense` layer in TensorFlow and a `Linear` layer in PyTorch, which "do the exact same thing"
(slide 38, ≈27:06–27:52):

```python
layer = tf.keras.layers.Dense(units=2)                 # TensorFlow
layer = nn.Linear(in_features=m, out_features=2)       # PyTorch
```

![Slide 38: Multi Output Perceptron](../raw/images/01-introduction/slide-38.jpg)

*Lecture 1, slide 38 — a dense layer with two outputs, and its TensorFlow and PyTorch one-liners.*

## A hidden layer

Inserting a layer between inputs and outputs gives a single-hidden-layer network with two weight
matrices, $\boldsymbol{W}^{(1)}$ (inputs to hidden) and $\boldsymbol{W}^{(2)}$ (hidden to output), of
different sizes because the layers differ in width (slide 39, ≈27:52–28:38). With $d_1$ hidden units:

$$z_i = w_{0,i}^{(1)} + \sum_{j=1}^{m} x_j w_{j,i}^{(1)}, \qquad \hat{y}_ i = g\left(w_{0,i}^{(2)} + \sum_{j=1}^{d_1} g(z_j) w_{j,i}^{(2)}\right)$$

Each hidden unit is the same perceptron as before, with its own weights over the same inputs
(slide 40, ≈28:38–29:23).

## Deep networks

A deep neural network is "nothing more than" many such layers stacked, with non-linearities between
them (≈29:23–30:10); Amini says a network is usually called deep once it has more than about three
layers. Layer $k$, with $n_k$ units, computes from the activated outputs of layer $k-1$ (slide 42):

$$z_{k,i} = w_{0,i}^{(k)} + \sum_{j=1}^{n_{k-1}} g(z_{k-1,j}) w_{j,i}^{(k)}$$

In code the layers go inside a `Sequential` block (slides 41 and 43): `tf.keras.Sequential([...])`
with `Dense` layers in TensorFlow, or `nn.Sequential(...)` with `nn.Linear` layers separated by
`nn.ReLU()` in PyTorch.

![Slide 43: Deep Neural Network](../raw/images/01-introduction/slide-43.jpg)

*Lecture 1, slide 43 — hidden layer* $k$ *of a deep network, and the `Sequential` code that stacks layers.*

A network built this way only computes a forward pass; until it is trained its weights are random and
its outputs meaningless (lecture 1, ≈32:30). Training needs a [loss function](loss-functions.md),
[gradient descent](gradient-descent.md) and [backpropagation](backpropagation.md).

## Where this comes up

- [Lecture 1 — Introduction to Deep Learning](01-introduction.md), sections 8 and 9.
