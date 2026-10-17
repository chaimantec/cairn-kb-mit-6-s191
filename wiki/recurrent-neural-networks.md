# Recurrent neural networks (RNNs)

A recurrent neural network processes a sequence one time step at a time while maintaining an
**internal state** $h_t$, a memory of what it has seen so far. At every step it updates that state
from the new input and the old state, and uses it to predict an output. It is one network applied at
every step with the same weights, not a new network per step. RNNs are the first sequence architecture
in MIT 6.S191, built from the ground up in [lecture 2](02-rnns-transformers-attention.md) (sections
3–9). See [sequence modeling](sequence-modeling.md) for the tasks they address.

## From feed-forward to recurrent

A feed-forward network applied separately at each time step computes $\hat{y}_ t = f(x_t)$, where $x_t$
is the input and $\hat{y}_ t$ the output at time $t$: each step is isolated, and the output at $t = 2$
cannot depend on $x_0$ or $x_1$ (slide 13, ≈8:27–9:14). Linking the steps through an internal state
$h$, passed from one step to the next, makes the output depend on the past (slide 14, ≈10:47–11:33):

$$\hat{y}_ t = f(x_t, h_{t-1})$$

## The recurrence relation

An RNN applies a recurrence relation at every time step (slide 17, ≈13:51–14:38):

$$h_t = f_W(x_t, h_{t-1})$$

where $h_t$ is the cell state, $f_W$ a function with weights $W$, $x_t$ the input and $h_{t-1}$ the old
state. **The same function and set of parameters are used at every time step.**

In lecture 2's version (slide 24, ≈16:56–17:43), the state update multiplies the previous state and
the input by their own weight matrices, sums them, and applies a hyperbolic tangent (see
[activation functions](activation-functions.md)); the output is a third weight matrix applied to the
new state:

$$h_t = \tanh(\boldsymbol{W}_ {hh}^T h_{t-1} + \boldsymbol{W}_ {xh}^T x_t)$$

$$\hat{y}_ t = \boldsymbol{W}_ {hy}^T h_t$$

The three weight matrices — $\boldsymbol{W}_ {hh}$ (state to state), $\boldsymbol{W}_ {xh}$ (input to
state) and $\boldsymbol{W}_ {hy}$ (state to output) — are learned by [gradient descent](gradient-descent.md)
(≈17:43). As pseudocode, an RNN predicting the next word initializes its hidden state to zeros, loops
over the words of the sentence calling `prediction, hidden_state = my_rnn(word, hidden_state)`, and
takes the prediction after the last word (slides 18–20, ≈15:23–16:56).

![Slide 24: RNN State Update and Output](../raw/images/02-rnns-transformers-attention/slide-24.jpg)

*Lecture 2, slide 24 — the input vector, the hidden-state update and the output vector.*

## Unrolled across time

Drawn as a loop, the state feeds back into the same cell; unrolled, the cell appears once per time step,
with $\boldsymbol{W}_ {xh}$, $\boldsymbol{W}_ {hh}$ and $\boldsymbol{W}_ {hy}$ re-used at every step
(slide 26, ≈18:28–19:15). Since there is a prediction at each step, there is a [loss](loss-functions.md)
at each step; these are summed into one total loss for the sequence.

![Slide 26: RNNs: Computational Graph Across Time](../raw/images/02-rnns-transformers-attention/slide-26.jpg)

*Lecture 2, slide 26 — the RNN unrolled, with shared weights and per-step losses summed into* $L$.

Slide 27 implements the cell from scratch as a TensorFlow `tf.keras.layers.Layer` (the code is in the
[lecture page](02-rnns-transformers-attention.md)); in practice you use the built-in layers, which slide
28 gives as `SimpleRNN(rnn_units)` in TensorFlow and `RNN(input_size, rnn_units)` from `torch.nn` in
PyTorch (≈20:46).

## Training: backpropagation through time

RNNs are trained with [backpropagation](backpropagation.md). Because the loss is summed over time steps,
errors are back-propagated through each step and then **across time steps**, from the current position
back to the beginning of the sequence: **backpropagation through time (BPTT)** (slides 43–44,
≈31:37–32:24).

Going back through the chain of states multiplies repeatedly by $\boldsymbol{W}_ {hh}$: the gradient
with respect to $h_0$ involves "many factors of $W_{hh}$ + repeated gradient computation" (slide 46,
≈32:24–33:10). This causes two problems:

- **Exploding gradients**, when many values are greater than 1: the gradient blows up. The usual remedy
  is **gradient clipping**, scaling large gradients back to a maximum (slide 47, ≈33:10).
- **Vanishing gradients**, when many values are less than 1: the gradient shrinks until there is very
  little signal to learn from (≈33:57). Slide 48 lists three places to address it: the activation
  function, weight initialization and the network architecture; the lecture does not go into them.

![Slide 48: Standard RNN Gradient Flow: Vanishing Gradients](../raw/images/02-rnns-transformers-attention/slide-48.jpg)

*Lecture 2, slide 48 — exploding gradients (values above 1, clip them) and vanishing gradients (values below 1).*

## Long-term dependencies and gated cells

Vanishing gradients mean errors from steps further back have smaller and smaller gradients, which biases
an RNN toward short-term dependencies (slide 49, ≈34:43–35:30). It handles "The clouds are in the ___"
but struggles with "I grew up in France, … and I speak fluent ___", where the clue lies far back (slides
50–53). Making the cell's internal computation more complex, to control the flow of information,
was the answer: the **long short-term memory (LSTM)**, from a group led by Jürgen Schmidhuber, uses
**gates** — a sigmoid layer followed by a pointwise multiplication — to selectively add or remove
information in each recurrent unit (slide 54, ≈35:30–36:15). The slide also names GRUs as gated cells;
the lecture does not give the LSTM's equations.

## Limitations

Lecture 2 names three limitations of RNNs (slides 59–61, ≈38:38–39:25):

- **An encoding bottleneck**: all information about the sequence must be packed into $h_t$.
- **Slow, with no parallelization**: the sequence is processed one step at a time.
- **No long memory**: they quickly run into limits on how long a dependency they can capture.

These motivate [attention and transformers](attention-and-transformers.md), which drop recurrence
entirely.

## Applications

Music generation, the subject of software lab 1: an RNN reads sheet music and predicts the next
character, each prediction fed back as the next input; Amini plays an AI-generated third movement for
Schubert's Unfinished Symphony made with a recurrent-based model (slide 56, ≈36:15–37:50). Sentiment
classification is the many-to-one example: read "I love this class!" and output the probability of
positive sentiment (slide 57).

## Where this comes up

- [Lecture 2 — Recurrent Neural Networks, Transformers, and Attention](02-rnns-transformers-attention.md),
  sections 3–9.
