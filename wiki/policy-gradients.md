# Policy gradients

**Policy gradient** methods are the policy-learning family of
[reinforcement learning](reinforcement-learning.md) algorithms: instead of learning the value of each
action and taking the best, as [Q-learning](q-learning.md) does, a network outputs a **probability
distribution over actions** for the current state, the action is **sampled** from it, and the network is
trained to make high-reward actions more likely. This page follows MIT 6.S191
[lecture 5](05-reinforcement-learning.md), sections 15–20 (≈34:39–51:35).

Notation, as on the lecture 5 slides: $s$ is a state and $a$ an action ($s_t$, $a_t$ at time $t$);
$\pi(s)$ is the policy; $P(a|s)$ is the probability of action $a$ in state $s$; $R_t$ is the total
discounted reward from time $t$; $\mu$ and $\sigma^2$ are a mean and a variance; $w$ are the network's
weights.

## Optimize the policy directly

Slides 36–37 set the two side by side. A deep Q network: "Approximate Q-function and use to infer the
optimal policy, $\pi(s)$". A policy gradient method: "Directly optimize the policy $\pi(s)$" (≈34:39–35:25). For a Breakout state the
policy network outputs one probability per action — $P(a_1|s) = 0.9$ for left, $P(a_2|s) = 0.1$ for
stay, $P(a_3|s) = 0$ for right — which sum to one, $\sum_{a_i \in A} P(a_i|s) = 1$. The action is sampled,
$\pi(s) \sim P(a|s)$, not taken as the argmax (≈36:12–36:58).

![Slide 37: the policy-gradient key idea](../raw/images/05-reinforcement-learning/slide-37.jpg)

*Lecture 5, slide 37 — a probability for each action, summing to one; the action is sampled.*

Sampling makes the policy **stochastic**: it can move left 90% of the time and stay still 10% of the
time, which Q-learning's argmax never does (≈36:58). Each probability is, in the lecturer's words, "the
probability that any given action results in the maximum return on future investment for that given
state" (≈41:35).

## Continuous action spaces

The subtler advantage is that the policy is no longer limited to a discrete set of actions (≈36:58–38:31).
A discrete action space asks "which direction should I move?" and puts a probability on each of left,
stay and right (slide 38); a continuous one asks "how fast should I move?" and needs a density over speed
(slide 39). The network then outputs the parameters of a distribution: on slide 40, a mean $\mu = -1$ and
a variance $\sigma^2 = 0.5$ defining

$$P(a|s) = N(\mu, \sigma^2)$$

from which the action is sampled — on the slide, $-0.8$ m/s, moving left (≈39:16). The mean is not the
action taken; it is only the centre of the distribution (≈40:03). The lecturer compares this to the
[VAE](autoencoders-and-vaes.md) encoder, which also outputs a mean and a spread rather than a point
(≈38:31). The Normal is an arbitrary choice — easy to learn, unimodal, a good approximator — and a
problem could need a multimodal or other parameterized distribution instead (≈40:03–40:50).

![Slide 40: a Gaussian policy over a continuous action](../raw/images/05-reinforcement-learning/slide-40.jpg)

*Lecture 5, slide 40 — the network outputs a mean and a variance, and the action is sampled from the Normal they define.*

## The training algorithm

Lecture 5 trains a self-driving car whose action is the steering angle and whose reward is the distance
travelled before a crash (slide 41, ≈41:35–42:21). The algorithm (slide 42, credited "Williams
*Reinforcement Learning* 1992."):

1. Initialize the agent.
2. Run a policy until termination.
3. Record all states, actions, rewards.
4. Decrease probability of actions that resulted in low reward.
5. Increase probability of actions that resulted in high reward.

The randomly initialized car crashes quickly, but every (state, action, reward) triplet on the way is
recorded. The actions closest to the crash — say the last 50% — are made less likely in those states,
and the earlier ones more likely; repeated, the car travels farther each time until it follows the lane
(slides 42–45, ≈43:08–44:41).

![Slide 42: a recorded trajectory ending in a crash](../raw/images/05-reinforcement-learning/slide-42.jpg)

*Lecture 5, slide 42 — each point of the run is a recorded (state, action, reward) triplet; red marks the actions near the crash.*

## The loss and the update

Steps 4 and 5 are a loss (slide 46, ≈45:26–46:58):

$$\mathbf{loss} = -\log P(a_t|s_t)\thinspace R_t$$

the negative of the action's log-likelihood times the total discounted reward. A likely action with a
large reward makes the loss very negative — a good loss — so it is reinforced; a likely action with a low
reward is discouraged; an unlikely action with a high reward is encouraged to happen again. Plugged into
gradient descent (slide 46 prints no learning rate):

$$w' = w - \nabla \mathbf{loss}$$

$$w' = w + \nabla \log P(a_t|s_t)\thinspace R_t$$

The boxed term $\nabla \log P(a_t|s_t)\thinspace R_t$ is the **policy gradient**, the gradient of the
policy itself, which gives the method its name (≈46:58). See [gradient descent](gradient-descent.md) and
[loss functions](loss-functions.md).

## Limits: exploration, and the real world

An action that is very unlikely may never be sampled, and so never learned, however good it is — "that's
a downside of the approach". Random initialization and extra randomness during training keep the model
exploring: the **exploration versus exploitation** trade-off (≈46:58–47:44).

The bigger problem is step 2: running until termination means crashing the car, which is why
reinforcement learning is rarely done directly in the real world (≈49:16–50:03). Lecture 5's answer is
training in simulation: a policy-gradient agent trained entirely in the VISTA data-driven simulator was
deployed directly on a real car (slides 48–49, ≈50:48–51:35; see
[reinforcement learning](reinforcement-learning.md)).

## Where this comes up

- [Lecture 5 — Reinforcement Learning](05-reinforcement-learning.md), sections 15–20.
