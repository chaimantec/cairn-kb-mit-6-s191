# Lecture 1 — Introduction to Deep Learning

**MIT 6.S191, 2026 edition. Lecturer: Alexander Amini. Delivered 5 January 2026.**
[Video](https://www.youtube.com/watch?v=II4giR4vOOo) ·
[Slides (PDF)](https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L1.pdf) ·
[Slide-by-slide transcription](../raw/slides/01-introduction.md) ·
[Transcript](../raw/transcripts/01-introduction.md) ·
[Verbatim captions](../raw/transcripts/original/01-introduction.md)

This lecture lays the foundation for the whole course. It defines deep learning as learning a task
directly from raw data with neural networks, builds the single neuron (the perceptron) from its three
steps (dot product, bias, non-linearity), stacks neurons into layers and layers into deep networks,
and then covers how such a network is trained: a loss that measures its errors, gradient descent
that lowers the loss, and backpropagation that computes the gradient. It closes with the practical
side of training — setting the learning rate, adaptive optimizers, mini-batches — and with two
regularization techniques against overfitting, dropout and early stopping.

Timestamps such as (≈15:37) point into the [transcript](../raw/transcripts/01-introduction.md);
"slide N" is page N of the PDF (the deck prints no slide numbers).

## 1. The pace of the field (0:05–7:47)

Amini opens with how fast the field moves, starting from the course's own history: the class was
created "exactly one decade ago" (≈0:53). Slide 2 shows generated faces from three moments: a blurry
grayscale face from 2015 (credited to Goodfellow et al.), a photorealistic synthetic face from 2018
(Karras, Laine, Aila), and a 2020 video still of a synthetic speaker made for the course's own
introduction video, which he says "went a bit viral" (≈1:38).

![Slide 2: "Seeing" the progress of deep learning throughout the years](../raw/images/01-introduction/slide-2.jpg)

*Slide 2 — generated faces in 2015 (Goodfellow et al.), 2018 (Karras, Laine, Aila) and the course's own 2020 synthetic-video introduction.*

The same revolution then reached natural language: slide 3 dates ChatGPT's launch (on GPT-3) to 2022
and "the GPT-4 'wow' moment" to 2023, and he describes the jump from GPT-3.5 to GPT-4 as one that
"even non-technical folks could really feel" (≈2:24). Behind those models sit GPU data centres
costing "hundreds of millions of dollars" (slide 4, ≈2:24–3:12), but the same capability has also
been moving onto small devices (slide 5), and the historical gap between large and small language
models has been large (≈3:12).

He then demonstrates this live on a phone in airplane mode (≈3:58–6:15), so that everything is
computed on the device: a chat model answers a question about finding zeros of an equation in Z7, the
integers modulo 7, and an end-to-end audio model answers a spoken request for a guide to giving a
compelling talk. He stresses that the audio model never converts speech to text, which is why its
latency is low and why it can "understand your emotion": converting to text loses it (≈6:15). The
model was developed by Liquid AI, released about a week before the lecture, and is multimodal across
text, audio and vision (≈7:01). Slide 6 shows the post he reads out: an open-source model "with only
2.6B parameters that can run locally on your phone" compared against the original GPT-4 on six
benchmarks, winning on five (IFEval, Multi-IF, IFBench, GPQA, AIME25) and losing on MMLU-Pro (53.87
against 63.7); the full table is in the [slide transcription](../raw/slides/01-introduction.md#slide-6--tweet-about-liquid-ai-model-beating-gpt-4-with-phone-photo).
Aloud he says "only 2 billion parameters" (≈7:47); the slide's figure is 2.6B.

## 2. What is deep learning? (7:47–9:22)

To define deep learning, Amini starts from intelligence, which he defines as processing information
in order to inform some future decision; **artificial intelligence** is a machine doing the same
(≈7:47–8:35). The three terms nest (slide 7):

- **Artificial intelligence**: "any technique that enables computers to mimic human behavior".
- **Machine learning**, a subset of AI: the "ability to learn without explicitly being programmed".
  Learning the processing from data, instead of being told the steps, is what separates ML from AI
  in general (≈8:35).
- **Deep learning**, a subset of ML: "extract patterns from data using neural networks", specifically
  deep neural networks.

![Slide 7: What is Deep Learning?](../raw/images/01-introduction/slide-7.jpg)

*Slide 7 — artificial intelligence ⊃ machine learning ⊃ deep learning, with each one's definition.*

The theme of the whole course is the slide's bottom line: "teaching computers how to learn a task
directly from raw data" (≈9:22). See [what is deep learning](what-is-deep-learning.md).

## 3. How the course runs (9:22–12:30)

The course is a one-week boot camp of technical lectures plus hands-on software labs, offered in both
TensorFlow and PyTorch (slides 8–9, ≈9:22–10:09). Each day has a lab mirroring that day's lectures
(slides 10–12, ≈10:57): lab 1 builds a music-generation model that learns a style of music (the slide
says Irish folk songs), lab 2 is computer vision and facial detection (the slide: detecting and
mitigating bias in facial recognition systems), and lab 3 fine-tunes, evaluates and deploys a large
language model (the slide: fine-tune Gemma in a mystery style and evaluate it with an AI judge). The
week ends with a project pitch competition, "very Shark Tank-like" (≈11:44): slide 13 sets five
minutes, strict, on Friday 9 January, with prizes, and Amini adds that "John" has offered the top
winners a TEDxMIT talk (≈10:09). Support runs through Piazza, the TAs, and the website, where all
slides are posted (slide 14, ≈11:44); staff and sponsors are on slides 15–16.

## 4. Why deep learning, and why now? (12:30–15:37)

Traditional machine learning depends on **hand-engineered features**, which slide 18 calls "time
consuming, brittle, and not scalable in practice". Deep learning's promise is to learn those features
directly from data, and to learn them **hierarchically** (≈12:30–13:16). For faces, he suggests how a
person might reason from first principles: detect lines, compose them into corners, compose corners
into eyes, noses and mouths, and take those as evidence of a face. Deep networks build features the
same way (≈13:16–14:03), from low-level lines and edges through mid-level parts to high-level facial
structure (slide 18).

![Slide 18: Why Deep Learning?](../raw/images/01-introduction/slide-18.jpg)

*Slide 18 — the feature hierarchy: lines and edges, then eyes, noses and ears, then whole facial structure.*

The core algorithms are old — slide 19's timeline runs from stochastic gradient descent (1952) and the
perceptron (1958) through backpropagation (1986) to deep convolutional networks for digit recognition
(1995) — so why the resurgence now? Amini gives three reasons (≈14:03–15:37):

1. **Big data.** Data has never been more prevalent, and these algorithms "live off of data".
2. **Hardware.** GPUs from companies like AMD and Nvidia accelerate massively parallel computation.
3. **Software.** Toolboxes such as TensorFlow and PyTorch, which the labs use, democratize creating,
   training and deploying models, even at large scale.

![Slide 19: Why Now?](../raw/images/01-introduction/slide-19.jpg)

*Slide 19 — the history timeline (1952–1995) and the three reasons: big data, hardware, software.*

## 5. The perceptron (15:37–18:40)

The most fundamental building block of every neural network is the single neuron, also called the
**perceptron** (≈14:50–15:37). See [the perceptron](perceptron.md).

Its forward propagation takes $m$ inputs $x_1, \dots, x_m$, multiplies each by its own weight
$w_1, \dots, w_m$, sums the products, and passes the sum through a **non-linear activation function**
$g$ to produce a single output $\hat{y}$ (slide 21, ≈15:37–17:08). One more term completes it: a
**bias** $w_0$, an extra weight on a constant input of 1, which lets the function shift (≈17:08):

$$\hat{y} = g\left(w_0 + \sum_{i=1}^{m} x_i w_i\right)$$

![Slide 22: The Perceptron: Forward Propagation](../raw/images/01-introduction/slide-22.jpg)

*Slide 22 — inputs, weights, sum, non-linearity, output; the green input of 1 carries the bias weight* $w_0$.

Since $\boldsymbol{X}$ and $\boldsymbol{W}$ are both lists of $m$ numbers, the sum is a dot product, and
the neuron is written compactly in vector form (slide 23, ≈17:53):

$$\hat{y} = g\left(w_0 + \boldsymbol{X}^T \boldsymbol{W}\right)$$

where $\boldsymbol{X} = [x_1, \dots, x_m]^T$ and $\boldsymbol{W} = [w_1, \dots, w_m]^T$.

![Slide 23: vector form of the perceptron](../raw/images/01-introduction/slide-23.jpg)

*Slide 23 — the same neuron, with the sum rewritten as the dot product* $\boldsymbol{X}^T \boldsymbol{W}$.

Amini singles this out as the one thing to remember from the class: a neuron is three steps, **dot
product, add a bias, apply a non-linearity**, and "that equation is the core to so many different
parts of deep learning" (≈24:02–24:48).

## 6. Activation functions (17:53–20:59)

A non-linear activation function maps any real number to a new real number — sometimes bounded,
sometimes not — by a transformation that is not linear (≈17:53–18:40). The example on slide 24 is the
**sigmoid**, which squashes any input into the range 0 to 1:

$$g(z) = \sigma(z) = \frac{1}{1 + e^{-z}}$$

![Slide 24: the sigmoid activation](../raw/images/01-introduction/slide-24.jpg)

*Slide 24 — the activation function* $g$ *highlighted in the perceptron equation, with the sigmoid as the example.*

Slide 25 shows three common choices, each with its derivative and its TensorFlow and PyTorch call:

| Function | $g(z)$ | $g'(z)$ | Range |
| --- | --- | --- | --- |
| Sigmoid | $\frac{1}{1 + e^{-z}}$ | $g(z)(1 - g(z))$ | 0 to 1 |
| Hyperbolic tangent | $\frac{e^{z} - e^{-z}}{e^{z} + e^{-z}}$ | $1 - g(z)^2$ | −1 to 1 |
| ReLU | $\max(0, z)$ | 1 for $z \gt 0$, 0 otherwise | 0 to ∞ |

![Slide 25: Common Activation Functions](../raw/images/01-introduction/slide-25.jpg)

*Slide 25 — sigmoid, tanh and ReLU (blue) with their derivatives (orange), and the one-line TensorFlow and PyTorch calls for each.*

The sigmoid is common wherever the output is a probability, because it always lands between 0 and 1,
"which is the space that probabilities live in"; ReLU outputs between zero and infinity, which is
useful for non-negativity constraints, and is "just two linear functions with a non-linearity between
them" (≈18:40–19:26). The slide's note: "all activation functions are non-linear". See
[activation functions](activation-functions.md).

**Why non-linearity at all?** Without it the neuron is just the dot product, and real data is
non-linear (≈19:26). Slides 26–28 show a two-dimensional dataset of red and green points that no
straight line can separate: a linear decision produces many errors, while a curved boundary separates
the classes easily (≈20:12). The slide's caption puts the general point: "linear activation functions
produce linear decisions no matter the network size", whereas "non-linearities allow us to approximate
arbitrarily complex functions".

![Slide 28: Importance of Activation Functions](../raw/images/01-introduction/slide-28.jpg)

*Slide 28 — the same red and green points under a linear decision boundary (left, many errors) and a non-linear one (right).*

## 7. A worked example: a neuron is a line (20:59–24:02)

Take a trained neuron with two inputs, bias $w_0 = 1$ and weights $w_1 = 3$, $w_2 = -2$ (slide 29,
≈20:59). Its output is

$$\hat{y} = g(1 + 3x_1 - 2x_2)$$

and what is inside $g$ "is just a line in 2D": $1 + 3x_1 - 2x_2 = 0$ is the neuron's **decision
boundary** in the plane of its two inputs (≈21:44). Feed in the new input $\boldsymbol{X} = [-1, 2]^T$:
it lies on one side of the line, and the arithmetic says which (slide 31, ≈22:30):

$$\hat{y} = g\big(1 + (3 \ast -1) - (2 \ast 2)\big) = g(-6) \approx 0.002$$

![Slide 31: The Perceptron: Example](../raw/images/01-introduction/slide-31.jpg)

*Slide 31 — the input* $[-1, 2]$ *plotted against the decision line* $1 + 3x_1 - 2x_2 = 0$*, and its output* $g(-6) \approx 0.002$.

A strongly negative pre-activation sends the sigmoid close to zero. In general the line splits the
plane in two (slide 32, ≈23:16): every input on one side has $z \lt 0$ before the activation and
$y \lt 0.5$ after a sigmoid, and every input on the other side has $z \gt 0$ and $y \gt 0.5$.

![Slide 32: the two half-planes of the decision boundary](../raw/images/01-introduction/slide-32.jpg)

*Slide 32 — the half-planes* $z \lt 0$, $y \lt 0.5$ *and* $z \gt 0$, $y \gt 0.5$ *on either side of the line.*

This picture works only because the neuron has two parameters; modern networks have billions, and a
billion-dimensional plot is impossible, so the rest of the lecture builds mathematical intuition
instead (≈23:16–24:02).

## 8. From one neuron to deep networks (24:02–30:55)

**Simplified notation.** With the three steps settled, the diagram drops its weight labels: every line
carries an input and an associated weight, and a single node $z$ stands for the dot product plus bias,
before the non-linearity (slide 35, ≈24:48–25:35):

$$z = w_0 + \sum_{j=1}^{m} x_j w_j, \qquad y = g(z)$$

![Slide 35: The Perceptron: Simplified](../raw/images/01-introduction/slide-35.jpg)

*Slide 35 — the simplified neuron: the inputs feed one node* $z$*, and the output is* $y = g(z)$.

**Multiple outputs.** Two neurons see the same inputs but have their own independent weights, so they
can produce two different answers (≈25:35). Because every input connects to every output, such layers
are called **dense** layers (slide 36):

$$z_i = w_{0,i} + \sum_{j=1}^{m} x_j w_{j,i}$$

To build one from scratch (slide 37, ≈25:35–27:06), initialize a weight matrix of size input dimension
× output dimension and a bias vector; the forward pass multiplies the inputs by the weights, adds the
bias, and applies the non-linearity. The TensorFlow and PyTorch versions differ mostly in names, and
both libraries already provide the layer: `tf.keras.layers.Dense(units=2)` in TensorFlow and
`nn.Linear(in_features=m, out_features=2)` in PyTorch (slide 38, ≈27:06–27:52). See
[neural network layers](neural-network-layers.md).

![Slide 38: Multi Output Perceptron](../raw/images/01-introduction/slide-38.jpg)

*Slide 38 — a dense layer with two outputs, and the one-line TensorFlow and PyTorch layer that implements it.*

**A hidden layer.** Adding a layer between inputs and outputs gives a single-hidden-layer network with
two weight matrices, $\boldsymbol{W}^{(1)}$ from the inputs to the hidden layer and
$\boldsymbol{W}^{(2)}$ from the hidden layer to the output, of different sizes because the layers have
different widths (slide 39, ≈27:52–28:38):

$$z_i = w_{0,i}^{(1)} + \sum_{j=1}^{m} x_j w_{j,i}^{(1)}, \qquad \hat{y}_ i = g\left(w_{0,i}^{(2)} + \sum_{j=1}^{d_1} g(z_j) w_{j,i}^{(2)}\right)$$

![Slide 39: Single Layer Neural Network](../raw/images/01-introduction/slide-39.jpg)

*Slide 39 — inputs, hidden layer and outputs, with weight matrices* $\boldsymbol{W}^{(1)}$ *and* $\boldsymbol{W}^{(2)}$.

Zooming in on one hidden unit, $z_2$, shows it is the same perceptron as before: a dot product of all
the inputs with that unit's own weights, plus its bias (slide 40, ≈28:38). Unit $z_3$ is computed the
same way with different weights (≈29:23).

![Slide 40: the weights into one hidden unit](../raw/images/01-introduction/slide-40.jpg)

*Slide 40 — only the weights into hidden unit* $z_2$ *are drawn, and its sum is written out term by term.*

Removing all the lines, a fully connected layer is drawn as a box with a "×" in it, and layers are
stacked with non-linearities between them using `Sequential` in both frameworks (slide 41,
≈29:23–30:10).

![Slide 41: layers as boxes, and Sequential code](../raw/images/01-introduction/slide-41.jpg)

*Slide 41 — each "×" box is a fully connected layer; `tf.keras.Sequential` and `nn.Sequential` stack them.*

**Deep networks.** A deep neural network is "nothing more than" many such layers stacked, so that the
output is computed by going "deeper and deeper" through them; Amini says people usually call a network
deep once it has more than about three layers (≈30:10). The $k$-th hidden layer computes (slide 42)

$$z_{k,i} = w_{0,i}^{(k)} + \sum_{j=1}^{n_{k-1}} g(z_{k-1,j}) w_{j,i}^{(k)}$$

and the code is the same `Sequential` block with more layers inside (slide 43).

![Slide 43: Deep Neural Network](../raw/images/01-introduction/slide-43.jpg)

*Slide 43 — hidden layer* $k$ *of a deep network, with the TensorFlow and PyTorch `Sequential` code.*

## 9. Applying a network: "Will I pass this class?" (30:55–33:16)

The running example has two features (slide 45): $x_1$, the number of lectures you attend, and
$x_2$, the hours spent on the final project. Past students are points in that plane, marked pass or
fail, and "you" are a new point at $(4, 5)$ (slide 47, ≈30:55–31:42).

![Slide 47: Example Problem: Will I pass this class?](../raw/images/01-introduction/slide-47.jpg)

*Slide 47 — past students as pass (green) and fail (red) points, and the new student at* $(4, 5)$.

Fed through a two-input network with one hidden layer of three units, the input $[4, 5]$ comes out as
0.1: a 10% chance of passing (slide 48, ≈31:42–32:30). The answer is wrong because the network is
**randomly initialized**: "effectively the same as a brand new baby", it has never seen any data, and
so far only a forward pass has been done (≈32:30). The ground truth for this example is 1, a pass
(slide 49), and the gap between 0.1 and 1 is what training has to close (≈32:30–33:16).

## 10. Quantifying loss (33:16–35:33)

The **loss** measures the cost incurred by an incorrect prediction: the deviation between the
prediction and the ground truth (slide 50, ≈33:16). Smaller loss means higher-quality output. For a
network $f$ with weights $\boldsymbol{W}$, the loss on example $i$ is

$$\mathcal{L}\left(f\left(x^{(i)}; \boldsymbol{W}\right), y^{(i)}\right)$$

where $f(x^{(i)}; \boldsymbol{W})$ is the prediction and $y^{(i)}$ the actual answer.

![Slide 50: Quantifying Loss](../raw/images/01-introduction/slide-50.jpg)

*Slide 50 — the network predicts 0.1 where the actual answer is 1; the loss compares the predicted and the actual value.*

Training minimizes not one example's loss but the average over the whole dataset of $n$ examples, the
**empirical loss** (slide 51, ≈34:01), also called the objective function, cost function or empirical
risk:

$$J(\boldsymbol{W}) = \frac{1}{n} \sum_{i=1}^{n} \mathcal{L}\left(f\left(x^{(i)}; \boldsymbol{W}\right), y^{(i)}\right)$$

![Slide 51: Empirical Loss](../raw/images/01-introduction/slide-51.jpg)

*Slide 51 — a dataset of inputs, the network's predictions* $f(x)$ *beside the true labels* $y$*, and their average loss* $J(\boldsymbol{W})$.

Which $\mathcal{L}$ to use depends on the output (≈34:01–35:33):

- For a **yes/no classification**, the network outputs a probability between 0 and 1 (which ties back
  to the sigmoid), and the **binary cross-entropy** loss compares the two probability distributions
  (slide 52):

  $$J(\boldsymbol{W}) = -\frac{1}{n} \sum_{i=1}^{n} y^{(i)} \log\left(f\left(x^{(i)}; \boldsymbol{W}\right)\right) + \left(1 - y^{(i)}\right) \log\left(1 - f\left(x^{(i)}; \boldsymbol{W}\right)\right)$$

- For a **continuous output**, such as tomorrow's temperature or your final grade, use a loss on the
  difference between the predicted and true values, such as the **mean squared error** (slide 53) or
  an L1 error:

  $$J(\boldsymbol{W}) = \frac{1}{n} \sum_{i=1}^{n} \left(y^{(i)} - f\left(x^{(i)}; \boldsymbol{W}\right)\right)^2$$

![Slide 52: Binary Cross Entropy Loss](../raw/images/01-introduction/slide-52.jpg)

*Slide 52 — binary cross-entropy for outputs that are probabilities, with its TensorFlow and PyTorch one-liners.*

![Slide 53: Mean Squared Error Loss](../raw/images/01-introduction/slide-53.jpg)

*Slide 53 — mean squared error for regression, on predicted against actual final grades.*

See [loss functions](loss-functions.md).

## 11. Training: loss optimization and gradient descent (35:33–39:22)

Training means finding the weights that achieve the lowest loss (slide 55, ≈35:33–36:18):

$$\boldsymbol{W}^{\ast} = \underset{\boldsymbol{W}}{\mathrm{argmin}} \frac{1}{n} \sum_{i=1}^{n} \mathcal{L}\left(f\left(x^{(i)}; \boldsymbol{W}\right), y^{(i)}\right) = \underset{\boldsymbol{W}}{\mathrm{argmin}} J(\boldsymbol{W})$$

Here $\boldsymbol{W} = \lbrace \boldsymbol{W}^{(0)}, \boldsymbol{W}^{(1)}, \dots \rbrace$ is the collection
of every weight in every layer, and the loss is a single number that is a function of all of them
(slide 56, ≈36:18). With just two weights $w_0$ and $w_1$, the loss is a surface whose height at each
point is the loss of that configuration (slide 57, ≈37:03).

![Slide 57: Loss Optimization](../raw/images/01-introduction/slide-57.jpg)

*Slide 57 — the loss* $J(w_0, w_1)$ *as a surface over two weights: peaks are bad weights, valleys good ones.*

**Gradient descent** walks down that surface (slides 58–61, ≈37:03–38:34). Start at a random point;
compute the **gradient**, which says which way is uphill at that one location; step a small amount in
the opposite direction; repeat until convergence.

![Slide 59: Compute gradient](../raw/images/01-introduction/slide-59.jpg)

*Slide 59 — at the random starting point, the gradient points uphill, the direction of increasing loss.*

![Slide 60: Take small step in opposite direction of gradient](../raw/images/01-introduction/slide-60.jpg)

*Slide 60 — one step of gradient descent: a small move downhill, against the gradient.*

![Slide 61: Repeat until convergence](../raw/images/01-introduction/slide-61.jpg)

*Slide 61 — repeated steps walk the weights down into a valley of the loss surface.*

Amini says this is guaranteed to converge to *a* bottom, but not necessarily the lowest one, since
where it ends up depends on where it starts (≈37:48–38:34). As an algorithm (slide 62, ≈38:34):

1. Initialize the weights randomly, $\sim \mathcal{N}(0, \sigma^2)$.
2. Loop until convergence:
   1. compute the gradient $\frac{\partial J(\boldsymbol{W})}{\partial \boldsymbol{W}}$;
   2. update the weights, $\boldsymbol{W} \leftarrow \boldsymbol{W} - \eta \frac{\partial J(\boldsymbol{W})}{\partial \boldsymbol{W}}$.
3. Return the weights.

In code (slides 63–64, ≈38:34–39:22) this is a loop that computes the loss inside a
`tf.GradientTape`, asks the tape for the gradient of the loss with respect to the weights, and applies
the same update. The gradient line is the key one, and computing it is the subject of the next
section. See [gradient descent](gradient-descent.md).

## 12. Computing gradients: backpropagation (39:22–42:27)

**Backpropagation** is how the gradient of a network is computed (≈39:22). Amini uses the simplest
possible network, a chain of one neuron per layer: input $x$, weight $w_1$, hidden unit $z_1$, weight
$w_2$, output $\hat{y}$, loss $J(\boldsymbol{W})$ (slide 65, ≈40:08). The question is how a small change
in one weight affects the final loss. For the last weight, the chain rule splits the derivative in two
(slide 67, ≈40:08–40:55):

$$\frac{\partial J(\boldsymbol{W})}{\partial w_2} = \frac{\partial J(\boldsymbol{W})}{\partial \hat{y}} \ast \frac{\partial \hat{y}}{\partial w_2}$$

![Slide 67: Computing Gradients: Backpropagation](../raw/images/01-introduction/slide-67.jpg)

*Slide 67 — the chain rule for the last weight* $w_2$*, each factor colour-matched to a link of the chain.*

For the earlier weight $w_1$, the second factor itself needs the chain rule again, through $z_1$
(slides 68–69, ≈40:55):

$$\frac{\partial J(\boldsymbol{W})}{\partial w_1} = \frac{\partial J(\boldsymbol{W})}{\partial \hat{y}} \ast \frac{\partial \hat{y}}{\partial z_1} \ast \frac{\partial z_1}{\partial w_1}$$

![Slide 70: repeat for every weight](../raw/images/01-introduction/slide-70.jpg)

*Slide 70 — the three-factor chain rule for* $w_1$*: "repeat this for every weight in the network using gradients from later layers".*

In a deeper network this repeats layer by layer, propagating gradients from the output back to the
input, which tells how every weight affects the final loss (slide 70, ≈41:41). In theory,
backpropagation is "nothing more than the chain rule". See [backpropagation](backpropagation.md).

## 13. Optimization in practice: learning rates and optimizers (42:27–46:19)

In practice it is much harder, because real loss landscapes are highly non-convex, with many minima,
and what training finds depends on the initialization and on the regularization applied (≈41:41–42:27).
Slide 72 shows a 2017 visualization of a real network's loss landscape ("Visualizing the loss landscape
of neural nets"), a two-dimensional projection of something with millions of dimensions, to be taken
"with a grain of salt", but still clearly rugged (≈42:27).

![Slide 72: Training Neural Networks is Difficult](../raw/images/01-introduction/slide-72.jpg)

*Slide 72 — a real network's loss landscape, rendered in 3D from "Visualizing the loss landscape of neural nets" (Dec 2017).*

**The learning rate.** The step size in the update, $\eta$, is the **learning rate**: the rate at
which you follow the gradient (slides 73–74, ≈43:12). It is just a number you set, and setting it is
hard (slides 75–77, ≈43:12–43:59):

- **too small** converges slowly and gets stuck in false local minima;
- **too large** overshoots, becomes unstable and diverges, so the loss can explode;
- **stable** rates are large enough to skip past the fake local minima but still settle in a global or
  near-global one.

![Slide 75: Setting the Learning Rate](../raw/images/01-introduction/slide-75.jpg)

*Slide 75 — a one-dimensional loss curve with a shallow false minimum and a deeper global one (star), starting from the initial guess.*

There are two ways to deal with this (slides 78–80, ≈43:59–44:47). One is to try many learning rates
and see what works, which "is not as crazy of an option as it sounds". The smarter one is an
**adaptive learning rate**: no longer fixed, made larger or smaller depending on how large the gradient
is, how fast learning is happening, the size of particular weights, and so on. Amini's intuition: take
a smaller step where the gradient is very large, and use something like momentum to carry through
small gradients and past local minima (≈44:47).

Slide 81 lists the main optimizers with their TensorFlow and PyTorch classes and references: SGD
(Kiefer & Wolfowitz, 1952), Adam (Kingma et al., 2014), Adadelta (Zeiler et al., 2012), Adagrad (Duchi
et al., 2011) and RMSProp. In practice you will "very rarely" use vanilla SGD; you would almost always
swap in Adam or another adaptive optimizer (≈45:34). Slide 82 puts it all together: a TensorFlow
training loop in which the optimizer line "can be replaced with any TensorFlow optimizer".

## 14. Mini-batches (46:19–48:38)

Computing the full gradient is expensive: backpropagation over every parameter, for every data point
in the dataset, on every step (slide 85, ≈46:19). Two alternatives trade cost against noise
(slides 86–89, ≈46:19–47:51):

- **Stochastic gradient descent (SGD)** picks a single random data point $i$ and steps against its
  gradient $\frac{\partial J_i(\boldsymbol{W})}{\partial \boldsymbol{W}}$: much faster, but "very
  noisy". (Slide 86's update line still prints the full gradient $\frac{\partial J(\boldsymbol{W})}{\partial \boldsymbol{W}}$;
  Amini's spoken description, ≈47:05, makes clear the step uses the one point's gradient.)
- **Mini-batch gradient descent** picks a batch of $B$ data points and averages their gradients:

  $$\frac{\partial J(\boldsymbol{W})}{\partial \boldsymbol{W}} = \frac{1}{B} \sum_{k=1}^{B} \frac{\partial J_k(\boldsymbol{W})}{\partial \boldsymbol{W}}$$

  which is fast and "a much better estimate of the true gradient".

Batch sizes range from a few points upward; 32 is very common, $B$ is usually on the order of tens or
hundreds, and large language models use batches in the millions; in every case it is much smaller than
the dataset (≈47:05–47:51). Mini-batches give a more accurate gradient estimate than single-point SGD,
smoother convergence, and allow larger learning rates; and because a batch can be computed in
parallel, they give significant speed-ups on GPUs (slides 90–91, ≈47:51–48:38). The batch size is how
you control the balance between accuracy and cost.

## 15. Overfitting and regularization (48:38–54:45)

**Overfitting** is learning too much into the training data: fitting details that do not generalize
beyond it. Its opposite is **underfitting**, a model not expressive enough to capture the data, such as
a straight line fitted to a non-linear relationship (slide 93, ≈48:38–49:24). The ideal sits in the
middle, generalizing to brand-new data in a test set or in deployment (≈49:24–50:10).

![Slide 93: The Problem of Overfitting](../raw/images/01-introduction/slide-93.jpg)

*Slide 93 — the same points under an underfitting line, an ideal fit, and an overfitting curve.*

**Regularization** is any technique that constrains the optimization problem to discourage complex
models, so as to improve generalization to unseen data (slides 94–95, ≈50:10). Amini notes this is how
models with billions of parameters can be trained without memorizing their datasets. See
[regularization](regularization.md).

**Dropout** (slides 96–98, ≈50:57–52:28): during training, randomly set some activations of the hidden
layers to zero, with a probability you choose, typically 50%. Each neuron must then cope with sometimes
receiving an input and sometimes not, so the network cannot rely on any single node or pathway and has
to find relationships that span many pathways (≈51:42).

![Slide 97: Regularization 1: Dropout](../raw/images/01-introduction/slide-97.jpg)

*Slide 97 — dropout: a random subset of hidden units (faded) is switched off for one training iteration.*

![Slide 98: a different dropout mask](../raw/images/01-introduction/slide-98.jpg)

*Slide 98 — on the next iteration a different random subset is dropped.*

A student asked whether the same activations are zeroed for the entire mini-batch. Amini's answer: yes
for the whole mini-batch, and a new random set is chosen for the next one (≈51:42–52:28).

**Early stopping** (slides 99–106, ≈52:28–54:45) works for any architecture, because it changes how long
you train, not the model. Keep a training set and a separate test set, and evaluate the loss on both
throughout training. At first both fall together, as the model moves from underfitting towards a good
fit; eventually the training loss keeps improving or plateaus while the test loss starts to rise, which
is overfitting (≈53:13–53:59). Save checkpoints along the way, and keep the one where the test loss was
lowest: after it, improvements on the training data no longer carry over to the test data (≈53:59).

![Slide 106: Regularization 2: Early Stopping](../raw/images/01-introduction/slide-106.jpg)

*Slide 106 — training and testing loss over iterations: stop where the testing loss bottoms out, between under-fitting and over-fitting.*

## 16. Summary, and what comes next (54:45–56:16)

Slide 107 reviews the lecture in three parts: the **perceptron** (the structural building block, with
non-linear activation functions), **neural networks** (stacking perceptrons, optimized through
backpropagation) and **training in practice** (adaptive learning, batching, regularization)
(≈54:45–55:31). Everything so far has handled non-sequential data. The next lecture, by Ava Amini,
covers sequence models — text as a sequence of words, audio as a sequence of waveforms, video as a
sequence of images — which power GPTs (≈55:31). Lab 1 (slide 108) is deep learning in Python and music
generation with RNNs, run in Google Colab.
