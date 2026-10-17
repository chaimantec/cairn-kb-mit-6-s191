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

## Losses over sequences

A [recurrent neural network](recurrent-neural-networks.md) makes a prediction at every time step, so it
has a loss at every time step, $L_0, L_1, L_2, \dots$; these are summed into a single total loss $L$ for
the whole sequence ([lecture 2](02-rnns-transformers-attention.md), slide 26, ≈19:15). That summed loss is
what backpropagation through time differentiates.

## Many classes: softmax

When the output is one of several classes, the network gives a probability for each, through a
**softmax** over its final outputs $y_i$ ([lecture 3](03-convolutional-neural-networks.md), slide 52,
≈38:35):

$$\text{softmax}(y_i) = \frac{e^{y_i}}{\sum_j e^{y_j}}$$

and is trained with a classification loss, "just like we saw yesterday" (≈38:35). Lecture 3 does not
write that loss out. Its one written loss is for the self-driving model of slide 65, which outputs a
probability distribution $P(\theta \mid I, M)$ over the control $\theta$, given camera image $I$ and map
$M$. It is trained to minimize $L = -\log(P(\theta \mid I, M))$, the negative log of the probability it
assigns (slide 65; the slide prints the formula with one closing parenthesis).

## Losses without labels: generative models

[Lecture 4](04-deep-generative-modeling.md) trains networks with no labels at all. An
[autoencoder](autoencoders-and-vaes.md) compares its input $x$ with its own reconstruction $\hat{x}$,
for images pixel by pixel (lecture 4, slide 15, ≈13:59–14:46):

$$\mathcal{L}(x, \hat{x}) = \Vert x - \hat{x} \Vert^2$$

A variational autoencoder, whose encoder (weights $\phi$) and decoder (weights $\theta$) are both
trained, adds a second term (slide 24, ≈20:13–20:59):

$$\mathcal{L}(\phi, \theta, x) = (\text{reconstruction loss}) + (\text{regularization term})$$

The regularization term is a distance between the distribution the encoder infers over the latent
variables and a fixed Normal prior, which slide 29 names the KL-divergence (≈21:47–24:08).

A [generative adversarial network](generative-adversarial-networks.md) has no single loss to minimize.
Its generator $G$ and discriminator $D$ share one objective that $D$ maximizes and $G$ minimizes, so
training is a min-max game (slides 70–72, ≈40:23–41:58):

$$\arg\min_{G} \max_{D} \mathbb{E}_ {\mathbf{z},\mathbf{x}}\left[\log D(G(\mathbf{z})) + \log\left(1 - D(\mathbf{x})\right)\right]$$

The formula is reproduced as slide 72 prints it; the lecture 4 page discusses how its terms are read
(section 18).

## Losses for reinforcement learning

In [reinforcement learning](reinforcement-learning.md) there are no labels either; the targets come from
rewards the agent observes by acting. A [deep Q network](q-learning.md) is trained to match a target
built from the reward $r$, the discount factor $\gamma$ and the best Q-value in the next state, with the
**Q-loss** ([lecture 5](05-reinforcement-learning.md), slide 30, ≈26:12–27:44):

$$\mathcal{L} = \mathbb{E}\left[ \left\Vert \left(r + \gamma \max_{a'} Q(s', a')\right) - Q(s,a) \right\Vert^2 \right]$$

Aloud, the lecture describes it as the absolute value of the difference between target and prediction.
A [policy-gradient](policy-gradients.md) network is trained instead with the negative log-likelihood of
the action $a_t$ it took in state $s_t$, weighted by the total discounted reward $R_t$ that followed
(slide 46, ≈45:26–46:58):

$$\mathbf{loss} = -\log P(a_t|s_t)\thinspace R_t$$

so that actions followed by high rewards become more likely and those followed by low rewards less so.

## Next-token prediction and denoising

Two losses in [lecture 6](06-language-models-new-frontiers.md) reuse the earlier ones. A
[large language model](large-language-models.md) predicts a probability for every token in its
vocabulary; since the vocabulary is a discrete set, next-token prediction is a classification problem,
trained with a **cross-entropy loss** between the predicted probabilities and the true next token, "just as
we saw in lecture one with losses that define classification" (slide 71, ≈47:54). The text provides its own
labels. A [diffusion model](diffusion-models.md) is trained on pairs of images one noising step apart with
"a mean squared error style loss" on their pixel differences; predicting that difference, which is the
noise, is a very effective way to train it (≈35:43). Lecture 6 writes out neither loss.

## Where this comes up

- [Lecture 1 — Introduction to Deep Learning](01-introduction.md), sections 9–11.
- [Lecture 2 — Recurrent Neural Networks, Transformers, and Attention](02-rnns-transformers-attention.md), sections 4 and 6.
- [Lecture 3 — Convolutional Neural Networks](03-convolutional-neural-networks.md), sections 15 and 20:
  softmax outputs for classification, and a likelihood loss for probabilistic control.
- [Lecture 4 — Deep Generative Modeling](04-deep-generative-modeling.md), sections 6, 8–9 and 18:
  the reconstruction loss, the VAE's regularization term, and the GAN's min-max objective.
- [Lecture 5 — Reinforcement Learning](05-reinforcement-learning.md), sections 11 and 19: the
  Q-loss and the policy-gradient loss.
- [Lecture 6 — Language Models and New Frontiers](06-language-models-new-frontiers.md), sections 16 and 23:
  the denoising loss of diffusion models and the cross-entropy loss of next-token prediction.
