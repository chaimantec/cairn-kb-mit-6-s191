# Backpropagation

Backpropagation is how the gradient of a neural network's loss is computed: it tells, for every
weight, how a small change in that weight would change the loss. [Gradient descent](gradient-descent.md)
needs exactly this gradient on every step. In MIT 6.S191 [lecture 1](01-introduction.md) (section 12,
≈39:22–42:27), Alexander Amini puts it plainly: in theory it is "nothing more than the chain rule".

## The chain rule on the simplest network

Lecture 1 uses a network with one neuron per layer (slide 65, ≈40:08): an input $x$, a weight $w_1$
into a hidden unit $z_1$, a weight $w_2$ into the output $\hat{y}$, and the loss $J(\boldsymbol{W})$
computed from $\hat{y}$.

**The last weight.** To find how $w_2$ affects the loss, split the derivative at $\hat{y}$ (slide 67,
≈40:08–40:55):

$$\frac{\partial J(\boldsymbol{W})}{\partial w_2} = \frac{\partial J(\boldsymbol{W})}{\partial \hat{y}} \ast \frac{\partial \hat{y}}{\partial w_2}$$

**An earlier weight.** For $w_1$, the factor $\frac{\partial \hat{y}}{\partial w_1}$ needs the chain
rule again, through $z_1$ (slides 68–69, ≈40:55):

$$\frac{\partial J(\boldsymbol{W})}{\partial w_1} = \frac{\partial J(\boldsymbol{W})}{\partial \hat{y}} \ast \frac{\partial \hat{y}}{\partial z_1} \ast \frac{\partial z_1}{\partial w_1}$$

![Slide 70: Computing Gradients: Backpropagation](../raw/images/01-introduction/slide-70.jpg)

*Lecture 1, slide 70 — each factor of the chain rule matches one link of the chain from* $w_1$ *to the loss.*

## Why "back" propagation

The first factor, $\frac{\partial J(\boldsymbol{W})}{\partial \hat{y}}$, is shared by both weights. In a
deeper network the same expansion repeats layer by layer: the gradients computed at the output are
propagated backwards through the network, all the way to the input, reusing the gradients of later
layers to get those of earlier ones (slide 70: "repeat this for every weight in the network using
gradients from later layers"; ≈41:41). The result tells how every single weight affects the final
loss — whether moving it in some direction makes the loss go up or down.

## In practice

The chain rule is clean; real networks are not. Their loss landscapes are highly non-convex, with many
minima, and what training finds depends on the initialization and on regularization (≈42:27; slide 72).
Backpropagation is also the expensive part of training, since it computes a derivative for every
parameter for every data point, which is the motivation for mini-batches (slide 85, ≈46:19; see
[gradient descent](gradient-descent.md)). In TensorFlow the framework computes it: a
`tf.GradientTape` records the forward pass and returns the gradient of the loss with respect to the
weights (slides 63–64).

## Through time: training recurrent networks

[Lecture 2](02-rnns-transformers-attention.md) (section 6, ≈30:04–33:57) applies the same algorithm to
[recurrent neural networks](recurrent-neural-networks.md). An RNN makes a prediction, and so has a
loss, at every time step, and the total loss is their sum. Errors are back-propagated through each
time step and then across time steps, from the current position back to the beginning of the sequence:
**backpropagation through time (BPTT)** (slides 43–44). Because each step back multiplies by the same
state-to-state weight matrix $\boldsymbol{W}_ {hh}$ again, the gradient can explode (many values above
1; the remedy is gradient clipping) or vanish (many values below 1), which makes long-term dependencies
hard to learn (slides 46–49).

![Slide 44: RNNs: Backpropagation Through Time](../raw/images/02-rnns-transformers-attention/slide-44.jpg)

*Lecture 2, slide 44 — backpropagation through time: the backward pass (red) runs from each loss back through the chain of states.*

## Through a sampling step: the reparametrization trick

A variational autoencoder ([lecture 4](04-deep-generative-modeling.md); see
[autoencoders and VAEs](autoencoders-and-vaes.md)) samples its latent variables $z$ in the middle of the
network, and "we cannot backpropagate gradients through sampling layers!" (lecture 4, slide 34, ≈28:47).
The fix rewrites the sample as a deterministic function of the encoder's outputs, a mean vector $\mu$
and a standard deviation vector $\sigma$, plus noise $\varepsilon$ that is not learned (slide 35,
≈28:47–29:34):

$$z = \mu + \sigma \odot \varepsilon, \quad \varepsilon \sim \mathcal{N}(0, 1)$$

In the computation graph, $z$ becomes a deterministic node and the randomness a separate input, so the
gradients $\frac{\partial f}{\partial z}$ and $\frac{\partial f}{\partial \phi}$ flow back to the
encoder's weights $\phi$ (slides 36–37, ≈29:34–30:20).

## Where this comes up

- [Lecture 1 — Introduction to Deep Learning](01-introduction.md), sections 11–14.
- [Lecture 2 — Recurrent Neural Networks, Transformers, and Attention](02-rnns-transformers-attention.md), section 6.
- [Lecture 4 — Deep Generative Modeling](04-deep-generative-modeling.md), section 11: backpropagating
  through a sampled latent variable.
