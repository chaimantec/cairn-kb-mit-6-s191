# Q-learning and deep Q networks

**Q-learning** is the value-learning family of [reinforcement learning](reinforcement-learning.md)
algorithms: learn the **Q-function**, which gives the expected return of each action in each state,
and act by picking the action with the highest value. A **deep Q network (DQN)** learns the Q-function
with a neural network. This page follows MIT 6.S191 [lecture 5](05-reinforcement-learning.md),
sections 6–14 (≈13:07–34:39).

Notation, as on the lecture 5 slides: $s$ is a state and $a$ an action ($s_t$, $a_t$ at time $t$);
$r$ is a reward and $R_t$ the discounted return from time $t$; $\gamma$ is the discount factor;
$Q(s, a)$ is the Q-function; $\pi(s)$ is the policy. Slides 28–30 also use $s'$ and $a'$, which they do
not define; read with the lecturer's explanation, they are the future state and the action taken there.

## The Q-function

The Q-function is the expected total future reward of taking action $a_t$ in state $s_t$ (slide 18,
≈13:07–13:53):

$$Q(s_t, a_t) = \mathbb{E}[R_t | s_t, a_t]$$

Given it, the optimal policy plugs in every possible action and takes the best (slide 19, ≈14:40):

$$\pi^{\ast}(s) = \underset{a}{\operatorname{argmax}}\thinspace Q(s, a)$$

So once the Q-function is known the problem is trivial; the work is in learning it (≈18:31).

## Guessing Q-values is hard

Lecture 5 shows why with Atari Breakout (slides 22–24, ≈20:03–24:40). Pair A has the ball falling
straight onto a paddle that stays still; pair B has the paddle chasing a ball coming in from the side.
Most of the room picked B, but trained policies show the real reason it wins: the B policy "learns a hack
in the system", breaking through the corner to unlock free blocks along the top. Reinforcement learning
plays millions of games and finds strategies people would not forecast.

## Two architectures

A deep Q network can be set up in two ways (slides 25–26, ≈24:40–25:26): take the state and an action as
input and output one value $Q(s, a)$; or take only the state and output a Q-value for every action,
$Q(s, a_1), \ldots, Q(s, a_n)$. The second needs one forward pass instead of one per action, and is
usually the one used in practice.

![Slide 26: two deep Q network architectures](../raw/images/05-reinforcement-learning/slide-26.jpg)

*Lecture 5, slide 26 — one Q-value per state-action pair (left), or one pass giving a Q-value for each action (right).*

## Training: target, prediction and the Q-loss

If the agent took all the best actions, its return would be maximized, and that maximum can serve as the
ground truth (slide 27, ≈26:12). The **target** is the reward now plus the discounted best Q-value in the
future (slide 28):

$$\left( r + \gamma \max_{a'} Q(s', a') \right)$$

the **prediction** is the network's own $Q(s, a)$ (slide 29), and the **Q-loss** trains the prediction to
match the target (slide 30):

$$\mathcal{L} = \mathbb{E}\left[ \left\Vert \left(r + \gamma \max_{a'} Q(s', a')\right) - Q(s,a) \right\Vert^2 \right]$$

Aloud, the loss subtracts the two and takes the absolute value (≈26:58). Targets come from playing each
game to the end and rewinding it: "the network does not learn the reward, the network observes the
reward from the game", and no human labels anything (≈29:14–30:47). Asked whether the target depends on
the network itself, given the $Q$ inside it, the lecturer said it is "the actual reward" and the notation
"probably … a misnomer": the Q there is "the true Q that's actually observed as the function of the
rollout" (≈33:52–34:39).

## Acting

At run time the network outputs a Q-value per action — on slide 31, 20 for left, 3 for stay and 0 for
right — and the policy takes the argmax, $\pi(s) = \operatorname{argmax}_ {a} Q(s, a) = a_1$. The action
goes to the environment, the next state comes back, and the loop continues (≈27:44–28:29).

![Slide 31: the DQN end to end](../raw/images/05-reinforcement-learning/slide-31.jpg)

*Lecture 5, slide 31 — Q-values of 20, 3 and 0 for left, stay and right; the argmax, left, is executed.*

## DQN on Atari

DeepMind's 2015 deep Q network (credited "Mnih+ *Nature* 2015.") was a
[convolutional neural network](convolutional-neural-networks.md) reading the screen's pixels: two
convolution layers and two fully connected layers ending in one output per joystick action, 18 in all
(slide 32, ≈31:35). With no labels and no prior knowledge of the games, it surpassed human-level
performance on many of the 49 Atari games charted on slide 33 — from Video Pinball at 2539% of human level
down to Montezuma's Revenge at 0% — an algorithm the lecturer says fits in "a few dozen lines of code"
(≈31:35–32:20). See [lecture 5](05-reinforcement-learning.md), section 13, for the chart.

## Downsides

Slide 34 lists two (≈32:20–33:52). **Complexity**: Q-learning "can model scenarios where the action space
is discrete and small" and "cannot handle continuous action spaces". **Flexibility**: because the policy
is computed deterministically by maximizing, it "cannot learn stochastic policies". Both motivate
[policy gradients](policy-gradients.md).

## Where this comes up

- [Lecture 5 — Reinforcement Learning](05-reinforcement-learning.md), sections 6–14.
