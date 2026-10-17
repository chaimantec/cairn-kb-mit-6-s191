# Gradient descent, learning rates and mini-batches

Gradient descent is how a neural network is trained: repeatedly nudge the weights in the direction
that most reduces the loss. This page covers the algorithm, the learning rate, adaptive optimizers and
mini-batches, following MIT 6.S191 [lecture 1](01-introduction.md), sections 11, 13 and 14.

Notation: $\boldsymbol{W}$ is the collection of all the network's weights; $J(\boldsymbol{W})$ is the
empirical loss over the training data (see [loss functions](loss-functions.md));
$\frac{\partial J(\boldsymbol{W})}{\partial \boldsymbol{W}}$ is its gradient; $\eta$ is the learning
rate.

## Loss optimization

Training means finding the weights that achieve the lowest loss (lecture 1, slide 55, ≈35:33):

$$\boldsymbol{W}^{\ast} = \underset{\boldsymbol{W}}{\mathrm{argmin}} J(\boldsymbol{W})$$

The loss is a function of the weights, so for a network with two weights $w_0, w_1$ it can be drawn as
a surface: each point is a configuration of the weights, and its height is the loss (slide 57,
≈37:03).

## The algorithm

Start somewhere random on that surface, compute the gradient — which points uphill, the direction of
increasing loss, at that one location — and take a small step the opposite way; repeat until
convergence (slides 58–61, ≈37:03–38:34).

![Slide 61: Gradient Descent — repeat until convergence](../raw/images/01-introduction/slide-61.jpg)

*Lecture 1, slide 61 — repeated small steps against the gradient walk the weights down into a valley of the loss surface.*

As pseudocode (slide 62, ≈38:34):

1. Initialize the weights randomly, $\sim \mathcal{N}(0, \sigma^2)$.
2. Loop until convergence:
   1. compute the gradient $\frac{\partial J(\boldsymbol{W})}{\partial \boldsymbol{W}}$;
   2. update the weights: $\boldsymbol{W} \leftarrow \boldsymbol{W} - \eta \frac{\partial J(\boldsymbol{W})}{\partial \boldsymbol{W}}$.
3. Return the weights.

Lecture 1 says this is guaranteed to converge to *a* bottom, though not necessarily the lowest one,
since the result depends on where it starts (≈37:48–38:34). In TensorFlow the gradient comes from a
`tf.GradientTape` (slides 63–64). Computing the gradient itself is
[backpropagation](backpropagation.md).

## The learning rate

$\eta$ sets how big each step is: "the rate at which you follow the gradient" (≈43:12). Real loss
landscapes are highly non-convex (slide 72), so the choice matters (slides 75–77, ≈43:12–43:59):

- a **small** learning rate converges slowly and gets stuck in false local minima;
- a **large** one overshoots, becomes unstable and diverges — the loss can explode;
- a **stable** one is large enough to skip past false local minima but still settles in a global or
  near-global minimum.

![Slide 75: Setting the Learning Rate](../raw/images/01-introduction/slide-75.jpg)

*Lecture 1, slide 75 — a loss curve with a shallow false minimum and a deeper global one (star), and the initial guess.*

One remedy is to try many learning rates and see what works, which is "not as crazy of an option as
it sounds". The smarter one is an **adaptive learning rate** that is no longer fixed but grows or
shrinks with how large the gradient is, how fast learning is happening and the size of particular
weights (slides 78–80, ≈43:59–44:47).

## Optimizers

Lecture 1, slide 81, lists the standard optimizers with their TensorFlow and PyTorch classes:

| Optimizer | Reference given on the slide |
| --- | --- |
| SGD | Kiefer & Wolfowitz, 1952 |
| Adam | Kingma et al., 2014 |
| Adadelta | Zeiler et al., 2012 |
| Adagrad | Duchi et al., 2011 |
| RMSProp | — |

In practice you will "very rarely" use vanilla SGD, and would almost always use Adam or another
adaptive optimizer (≈45:34). In a training loop the optimizer is a single line that can be swapped for
any other (slide 82).

## Stochastic and mini-batch gradient descent

The full gradient sums over every data point, and backpropagating through every parameter for every
point on every step is expensive (slide 85, ≈46:19). Two cheaper estimates (slides 86–89,
≈46:19–47:51):

- **Stochastic gradient descent** uses one random data point $i$ per step, with gradient
  $\frac{\partial J_i(\boldsymbol{W})}{\partial \boldsymbol{W}}$: much faster, but very noisy.
- **Mini-batch gradient descent** averages over a batch of $B$ points,
  $\frac{\partial J(\boldsymbol{W})}{\partial \boldsymbol{W}} = \frac{1}{B} \sum_{k=1}^{B} \frac{\partial J_k(\boldsymbol{W})}{\partial \boldsymbol{W}}$:
  fast to compute and "a much better estimate of the true gradient".

Mini-batches give a more accurate gradient, smoother convergence and room for larger learning rates,
and because a batch is computed in parallel they bring large speed-ups on GPUs (slides 90–91). Batch
sizes are usually tens or hundreds — 32 is common — while large language models use millions; the
batch size is the dial between accuracy and cost (≈47:05–48:38).

## Where this comes up

- [Lecture 1 — Introduction to Deep Learning](01-introduction.md), sections 11, 13 and 14.
- [Lecture 2 — Recurrent Neural Networks, Transformers, and Attention](02-rnns-transformers-attention.md), sections 4 and 6: an RNN's three weight matrices are learned by gradient descent, with gradients from backpropagation through time; gradient clipping keeps exploding gradients in check.
