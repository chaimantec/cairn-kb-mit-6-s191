# AI for science and deep learning emulators

**AI for science** here means using deep learning to accelerate scientific discovery, as Chris Bishop
presents it in the guest [lecture 8](08-ai-for-science.md). Its central tool is the **deep learning
emulator**. A conventional simulator solves the equations of physics many times; its output becomes
training data for a neural network; and the trained network then gives the simulator's answers thousands
of times faster. This page collects the ideas behind emulators and the examples the lecture gives.
Citations are to [lecture 8](08-ai-for-science.md) unless another lecture is named; "slide N" is page N of
that lecture's PDF.

## The problem: known equations that cannot be solved

The world is described by simple equations of extraordinary precision. Slide 3's theoretical and
experimental values of the electron's magnetic moment agree, in Bishop's words, to 13 significant figures
(≈2:31). But the equations are extremely hard to solve. Paul Dirac said so in 1929: the laws needed for
"a large part of physics and the whole of chemistry are thus completely known", but their exact
application "leads to equations much too complicated to be soluble" (slide 4, ≈3:17).

The reason is dimension. Schrödinger's equation is an equation for the wave function
$\Psi(\mathbf{x}_ 1, \ldots, \mathbf{x}_ N)$, a function of the positions of all $N$ electrons at once.
For caffeine's roughly 100 electrons that is a 300-dimensional space. A grid of 1,000 points per
dimension needs 1,000 points in one dimension, a million in two and a billion in three, so the cost grows
exponentially with the number of electrons (slide 19, ≈29:24–30:09). Nobody has computed caffeine's
properties by solving Schrödinger's equation directly (≈30:09).

## Data and inductive bias: the no free lunch theorem

The **no free lunch theorem**, as the lecture states it, says "you cannot learn purely from data". A
prediction always combines data with assumptions, called prior knowledge or **inductive bias** (≈7:54).
Slide 6 draws the two regimes as balance scales:

- **Large language models** are data-heavy, trained at internet scale, with a "fairly lightweight"
  inductive bias: attention, a very general assumption (≈7:54–8:40; see
  [large language models](large-language-models.md) and
  [attention and transformers](attention-and-transformers.md)).
- **Scientific AI models** have scarce, expensive data (a student can spend a year finding the 3D
  structure of one protein, which is one data point) and a uniquely rich inductive bias: the equations
  (≈8:40–9:26).

Science's inductive biases include Schrödinger's equation itself, **invariance** and **equivariance** under
rotation, and **conservation laws** of energy, mass, momentum and charge (slide 7, ≈9:26–10:59). An
isolated molecule's energy must not change when it is rotated, though every coordinate fed to the network
changes: that is invariance. Its magnetic moment must rotate with it: that is equivariance. That idea
underlies **geometrical deep learning** (≈10:13–10:59). Such knowledge can be built into a model in several
ways (≈10:59–11:45; ≈50:51–51:36):

- by structuring the architecture so that every setting of the weights satisfies the property;
- by writing an equation as "something equals zero" and adding the something squared to the loss;
- by **data augmentation**: rotate each molecule into, say, a hundred orientations with the same energy
  label, and let a general architecture learn the invariance, though not exactly.

## The bitter lesson

Rich Sutton's 2019 essay "The Bitter Lesson" (slide 8) says that general methods that leverage computation
win in the end. In Bishop's summary, people who baked in more prior knowledge have always lost out to
someone who simply had more data, "provided data is available, an important caveat" (≈11:45–12:31). That
poses the dilemma: science has beautiful equations it will not ignore, yet data eventually wins (≈13:18).

## Emulators: turning the equations into data

The emulator reconciles the two (slide 9, ≈13:18–15:38). The steps:

1. **Generate data.** Solve the equations ahead of time, many times, for many systems: expensive, but done
   once.
2. **Train.** Train a network on that synthetic data. The data is expensive to compute, so the datasets
   and models are far smaller than a frontier LLM's.
3. **Use.** Use the network in place of the **simulator**, the conventional software that solves the
   equations iteratively. A trained feedforward network is just a function, evaluated very quickly.

The cost is **amortized** over thousands or millions of uses (≈15:38). The prior knowledge enters as data,
which is how the approach "takes on board the idea of the bitter lesson" (≈56:13).

Slide 10 lists the benefits (≈15:38–18:41). The data is **synthetic** and **perfectly labelled**, since
any property can be computed from a solution. There are **no privacy issues**. Its quantity is limited
"only" by compute, so "we'll never run out of data". It can be generated on **under-utilized** single GPUs
or CPUs, in massively parallel jobs. And the payoff is **acceleration**, printed as "≈ $10^3 - 10^{4+}$":
usually "a few thousand times faster than the original simulator" at the first attempt (≈18:41).

Experiments remain fundamental: "If it doesn't agree with experiment, we're wrong", and experimental data
also complements the computational data, for instance by fine-tuning a model trained on simulations
(≈55:27–56:13).

## Examples in the lecture

- **Weather and the Earth system: Aurora** (slides 11–13, ≈18:41–22:30). Numerical weather prediction
  solves partial differential equations on supercomputers, and decades of simulated atmospheric data
  exist. Aurora, named on the slides, is a **foundation model** trained on diverse data from many
  simulators and then fine-tuned. Fine-tuned for air pollution, it is the state of the art. It produces the
  UK 8-day forecast "in 1 minute on a single A100 GPU".
- **Materials: MatterGen** (slides 14–17, ≈22:30–26:21). A **conditional diffusion model** for crystals
  that denoises the unit cell, atom types and atom positions, conditioned on desired electronic, magnetic
  or mechanical properties. It focuses the search on promising regions of chemical space, and an emulator
  then screens the candidates. See [diffusion models](diffusion-models.md).
- **Quantum chemistry: Skala** (slides 18–25, ≈26:21–40:08). **Density functional theory** (DFT; Walter
  Kohn, 1965) replaces the wave function by the electron density $\rho(\mathbf{x})$, a function of three
  dimensions. That is an exact transformation from exponential to cubic cost, except for the
  **exchange-correlation functional**, which Kohn proved universal but nobody can write down. About 800
  handcrafted approximations are in use, and they trade cost against error. Skala learns the functional
  with message passing over a point cloud of the density. It reaches chemical accuracy, about 1 kcal/mol,
  on atomization energies in slide 25's chart, at cubic complexity.
- **Proteins: molecular dynamics emulators** (slides 26–30, ≈40:08–45:29). Molecular dynamics integrates
  Newton's second law with femtosecond steps, $10^6$ to $10^{15}$ of them in sequence, with
  quantum-mechanical forces at every step: the **curse of sequentiality**. An emulator trained on DFT
  forces between chunks of a protein runs MD for proteins of about 10,000 atoms (AI²BMD, named on slide
  29). A biomolecular emulator, on the cover of Science (slide 30), samples a protein's equilibrium shapes
  directly, without the dynamics.

These form a hierarchy: data from one level trains the emulator at the next (≈44:43). The quantum
chemistry data trains Skala, and DFT then generates data for faster force fields and dynamics. DFT is kept
in the hierarchy, rather than training straight on quantum chemistry data, because it carries so much
physics (≈51:36–53:08).

## The fundamental trilemma

What these methods trade is **accuracy, speed and generality**: "You can have any two of those, no problem
at all, but you need all three" (slide 18, ≈26:21–27:07). The accuracy target is **chemical accuracy**,
about a kilocalorie per mole, at which computation is as good as experiment. It is hard because, as when
weighing a boat's captain by weighing the boat with and without the captain, the energy changes that matter in a
reaction are a small fraction of the total energy (≈27:53–28:39).

## Elsewhere in the course

- [Lecture 6](06-language-models-new-frontiers.md), section 20, introduces diffusion over the 3D coordinates
  of molecules and proteins (slide 66).
- [Reinforcement learning](reinforcement-learning.md) also trains on simulators, for a different reason:
  learning by trial and error on real roads is impossible. A student in lecture 8 compares the gap between
  simulated and real data to robotics (≈54:41–55:27).

## Where this comes up

- [Lecture 8 — AI for Science](08-ai-for-science.md), the whole lecture.
- [Lecture 6 — Language Models and New Frontiers](06-language-models-new-frontiers.md), section 20.
