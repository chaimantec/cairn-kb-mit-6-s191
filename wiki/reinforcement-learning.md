# Reinforcement learning

**Reinforcement learning** is the third paradigm of machine learning in MIT 6.S191, after supervised
and unsupervised learning. An **agent** acts in an **environment**, receives **rewards** for its
actions, and learns to maximize the rewards it collects over time — with no pre-collected dataset, since
the data are gathered while the agent learns. **Deep** reinforcement learning trains such agents with
deep neural networks. This page follows [lecture 5](05-reinforcement-learning.md), sections 1–8 and
18–22; the two families of algorithms have their own pages,
[Q-learning and deep Q networks](q-learning.md) and [policy gradients](policy-gradients.md).

Notation, as on the lecture 5 slides: $t$ is the time step; $s_t$ the state, $a_t$ the action and $r_t$
the reward at time $t$; $A$ the action space; $R_t$ the return; $\gamma$ the discount factor;
$Q(s, a)$ the Q-function; $\pi(s)$ the policy.

## How it differs from supervised and unsupervised learning

Lecture 5 sets the three side by side (slides 4–6, ≈2:24–4:42). **Supervised learning** has pairs
$(x, y)$ of data and label and learns a function mapping $x \rightarrow y$: "This thing is an apple."
**Unsupervised learning** has data $x$ alone and learns its underlying structure: "This thing is like
the other thing." **Reinforcement learning** has, as slide 6 prints it, state-action pairs — aloud,
triplets of states, actions and rewards — and its goal is to "Maximize future rewards over many time
steps": "Eat this thing because it will keep you alive." No label says apples are good to eat; eating
apples and other food, you could observe that apples make you live longer (≈4:42).

So reinforcement learning has "neither" labels nor a fixed dataset: data are actively collected while
the model learns, in a dynamic environment, much as humans learn by interacting with the world (≈0:52).
It is naturally temporal, maximizing rewards over the horizon of a sequence (≈4:42). See
[what is deep learning?](what-is-deep-learning.md) for the other two paradigms.

## The vocabulary

Lecture 5 builds the terms around one loop diagram (slides 8–17, ≈5:28–10:04):

- The **agent** "takes actions": a delivery drone, Super Mario in his game, or a person in the world.
  (Lecture 7 uses "agent" in a different sense, for a language model that calls tools on a user's behalf;
  see [AI agents](ai-agents.md).)
- The **environment** is "the world in which the agent exists and operates".
- An **action** is "a move the agent can make in the environment"; the **action space** $A$ is "the set
  of possible actions an agent can make in the environment" — for simplicity, a finite set, such as
  forwards, backwards, left and right in a two-dimensional world.
- **Observations** come back from the environment after each action. The new **state**, "a situation
  which the agent perceives", is $s_{t+1}$ after action $a_t$.
- The **reward** $r_t$ is "feedback that measures the success or failure of the agent's action" — a coin
  collected, or $+1$ for winning a game of chess and $-1$ for losing it. Rewards may be **sparse** or
  delayed, as in chess, where nothing arrives until the end; that is one of the big challenges. They can
  be negative, which can act as a penalty (≈8:31–10:50).

A state and a reward are different things: the state is a snapshot of the environment (where all the
chess pieces are) and does not depend on how good the action was; the reward depends directly on it
(≈11:35–12:22).

![Slide 17: the reinforcement learning loop and the discounted return](../raw/images/05-reinforcement-learning/slide-17.jpg)

*Lecture 5, slide 17 — the agent sends actions; the environment returns observations: the new state and the reward.*

## The return and discounting

The **return** (total reward) is the sum of all rewards from time $t$ on, $R_t = \sum_{i=t}^{\infty} r_i$
(slide 14). Future rewards are usually **discounted**: five dollars today is worth more to you than five
dollars a year from now (≈9:18). With a discount factor $0 \lt \gamma \lt 1$ that compounds over time,
slide 17 writes

$$R_t = \sum_{i=t}^{\infty} \gamma^{i} r_i$$

and slide 18 writes the same idea counted from the present, $R_t = r_t + \gamma r_{t+1} + \gamma^{2} r_{t+2} + \cdots$
(the two forms differ by the constant factor $\gamma^{t}$). A reward that arrives only at the end of a
game is discounted back in the same way; the hard part is learning what to do now from it (≈10:50–11:35).

## The Q-function and the policy

The **Q-function** gives the expected return of taking action $a_t$ in state $s_t$ (slide 18, ≈13:07):

$$Q(s_t, a_t) = \mathbb{E}[R_t | s_t, a_t]$$

It is an expected value: it does not capture the spread of possible returns (≈16:12). What an agent
ultimately needs is a **policy** $\pi(s)$, which gives the best action to take in a state. Given a
Q-function, the policy simply picks the action with the highest Q-value (slide 19, ≈14:40–15:27):

$$\pi^{\ast}(s) = \underset{a}{\operatorname{argmax}}\thinspace Q(s, a)$$

## Two families of algorithms

Deep reinforcement learning algorithms come in two families (slide 20, ≈19:17):

- **Value learning** finds $Q(s, a)$ and acts with $a = \operatorname{argmax}_ {a} Q(s, a)$. Its main
  algorithm in the course is the deep Q network: see [Q-learning and deep Q networks](q-learning.md).
- **Policy learning** finds $\pi(s)$ directly and samples $a \sim \pi(s)$. This handles stochastic
  policies and continuous action spaces, which Q-learning cannot: see [policy gradients](policy-gradients.md).

Lecture 5's summary slide (57) lists the foundations as "Agents acting in environment", "State-action
pairs → maximize future rewards" and "Discounting".

## Exploration versus exploitation

A policy that never tries an action never learns about it, even if that action would earn a large
reward. Lecture 5 calls this a downside of policy learning and answers it with randomness: random
initialization so that many actions are seen at first, and encouraging randomness during training so the
model explores other states. "Even though you think you're in a good path, you don't just want to
exploit that. You always want to have some exploration around as well" (≈46:58–47:44).

## Learning in the real world: simulation

Training as lecture 5 describes it requires running the policy until termination — for a self-driving
car, crashing it — so it cannot be done on real roads (slide 47, ≈49:16–50:03). Simulation is therefore
a very big field for reinforcement learning, and games are central because "it's very safe to die in
games" (≈50:03). Most simulators are model-based and game-like, which makes transferring a policy to
reality hard; MIT's **VISTA** is a data-driven, photorealistic simulator built from real driving data, in
which a policy-gradient agent was trained and then deployed directly on a real car (slides 48–49,
≈50:48–51:35; see [lecture 5](05-reinforcement-learning.md), section 20).

## Applications in the course

- **Atari games**: DeepMind's deep Q network learned from screen pixels and surpassed human-level play on
  many games (lecture 5, slides 32–33; see [Q-learning](q-learning.md)).
- **Autonomous driving**: the VISTA-trained car above.
- **Go**: AlphaGo first imitated human expert positions by supervised learning, then improved by
  self-play reinforcement learning to super-human performance, and learned a value network for
  "intuition" about board states (slides 53–56, ≈52:21–53:53). Lecture 5 also showed, in answer to a
  question, a slide not in the published deck on training from scratch with no human data, across Go,
  chess and other games (≈54:39–55:25).
- **Language models**: after imitation by next-word prediction, LLMs face a preference-alignment problem;
  the thumbs up and thumbs down users give a chatbot train "a reward model" that a reinforcement learning
  algorithm then maximizes (≈53:53–54:39). Lecture 5 says this is covered later in the course;
  [lecture 6](06-language-models-new-frontiers.md) covers training by next-token prediction and says only
  that base models are then tuned and refined to act as chatbots (≈49:25; see
  [large language models](large-language-models.md)).

## Where this comes up

- [Lecture 5 — Reinforcement Learning](05-reinforcement-learning.md), sections 1–8 and 18–23.
