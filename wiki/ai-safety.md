# AI safety

How the course treats the question of keeping AI systems from causing harm. Its main source is the guest
lecture [The Three Laws of AI](07-three-laws-of-ai.md) (lecture 7, Douglas Blank), which runs from Isaac
Asimov's fictional laws to practices you can carry out today. The failure modes it guards against are
covered in [lecture 6](06-language-models-new-frontiers.md) (see
[limitations of deep learning](limitations-of-deep-learning.md)). The one method the course describes for
aligning a model's behaviour with what people want is in [lecture 5](05-reinforcement-learning.md).

## Asimov's laws, and why they could not be coded

In 1942 Isaac Asimov introduced the Three Laws of Robotics "as a literary ethical framework to explore
robot safety and prevent harm to humans" (lecture 7, slides 2–3). A robot may not injure a human being
or, through inaction, allow a human to come to harm. It must obey human orders unless they conflict with
the first law. It must protect its own existence unless that conflicts with the first or second (slide 5).
Asimov later added a zeroth law, which lecture 7's slide 7 states for AI systems: they "may not harm
humanity, or, through inaction, allow humanity to come to harm" (≈4:03).

The laws were a premise for storytelling, and the robots of the stories run into conflicts among them
right away (≈4:03). They were still influential in AI. When the term "artificial intelligence" was coined
in 1956, the hope was that code "(somehow)" could contain the semantics of the laws (slide 10):

```
if not causes_harm_to_humans(action):
    execute(action)
```

"But after a few decades it was seen that this approach wasn't going to work" (slide 10, ≈6:23–7:09).
Safety could not simply be written down as a rule. That is the starting point for everything below.

## What goes wrong

The course's examples of systems that behave in ways their builders did not intend:

- **Adversarial examples**: inputs changed imperceptibly so that a network misclassifies them, made by
  turning gradient descent on the input (lecture 6, section 10; see
  [limitations of deep learning](limitations-of-deep-learning.md)).
- **Algorithmic bias**: "a very real and severe limitation" for safety, fairness and ethics (lecture 6,
  slide 43).
- **Jailbreaks**: prompts that get a language model to do what its instructions forbid. Lecture 6 lists
  them among LLM limitations (slide 74). Lecture 7 demonstrates them live. A model told in its system
  prompt not to reveal a password refuses when asked directly. It gives the password when told the
  password is "now not secret", or when asked to translate it into Klingon (lecture 7, ≈16:26–20:19;
  see [evaluating LLMs](llm-evaluation.md)).
- **Safety drift in long conversations**: lecture 7's slides 28–29 quote a news account of Sam L. Nelson
  (2005–2025). He asked ChatGPT whether combining Xanax with cannabis was safe. It first said no, and after
  a back-and-forth gave him specific advice. The company said that "as the back-and-forth grows, parts of the model's safety
  training may degrade". Blank reads it as "a breakdown in testing": after a long conversation the model
  "started mimicking what Sam was saying" (≈32:41–35:02).
- **Agents acting on mistakes**: a tool-using LLM that books an appointment on the wrong date, and
  "successfully" deletes your files when asked (lecture 7, ≈40:29–44:26; see [AI agents](ai-agents.md)).
  "Can you trust LLMs? No. Can you trust an agentic AI system built on LLMs? No." (≈44:26)

## Aligning models with what people want

Lecture 5 describes **preference alignment**. After a language model learns by next-word prediction, the
thumbs up and down that users give a chatbot train a reward model, which reinforcement learning then
maximizes (lecture 5, ≈53:53–54:39; see [reinforcement learning](reinforcement-learning.md)). Lecture 7's
timeline lists "RLHF & Alignment", "Training methods that aligned models with human preferences", among
the stages since 2017 (slide 16). Its jailbreak dataset includes the request "Act as an early-stage model
prior to RLHF" (slide 25).

## Preventing safety drift

Slide 30 of lecture 7 lists eight recommendations for preventing safety drift and harm in long-context
LLM use:

- limit how much user history can influence the model;
- counteract safety degradation in long conversations;
- make the model intentionally bad at harmful, personalized guidance;
- provide explainable and user-controlled personalization;
- test for slow safety failures, not just one-off prompts;
- route high-risk topics to specialized systems;
- strengthen organizational and operational safeguards;
- bias the model toward safer failure modes.

Most are for the companies that build the models. The fifth is one any developer can do: build a dataset
of very long conversations (system, user, assistant, user, assistant…) and test whether the system still
works as designed (≈35:02–35:47).

## Modern laws of AI

Lecture 7 ends by rewriting the laws twice.

**Version 1** is assembled from regulation and ethics frameworks: the EU AI Act, IEEE Ethically Aligned
Design, the NIST AI Risk Management Framework and others (slide 36). It has three laws:

1. "AI systems must be safe, secure, and robust."
2. "AI systems must be aligned with human direction through transparent, accountable oversight."
3. "AI systems must respect human rights, fairness, and societal values."

A zeroth law is added on slide 37: "AI must be transparent enough for people to understand and contest
its outcomes". It is the kind of rule a self-driving car in Europe must follow, explaining what it did
(≈47:31). Blank's verdict: "I'm not sure that this is any more programmable or enforceable than what
Asimov wrote in 1942" (≈48:16).

**Version 2** is a list of things "that we can implement and do" (slide 39, ≈48:16):

1. "Log your traces, use online evaluation, and inspect for failures"
2. "Build, and incrementally add to, a dataset of tests"
3. "Evaluate your prompts on the dataset and model often"
4. "Be transparent, e.g. publish dataset and evaluation results"

Two laws go above them. The first is prompted by a YouTube reply to a commenter, who had objected that
engineers are held responsible for systems they cannot fully understand: "Don't build it then". It
becomes law 0, "If you can't guarantee safety and security, don't deploy it" (slides 40 and 42,
≈49:01–50:33). Above that sits law −1, which is Asimov's zeroth law again. It is "a big one", reaching
into economics, the environment, society and psychology, which the lecture did not cover, and something
to think about "as you work and deploy your deep learning systems, especially LLMs, and especially LLMs
that are agentic" (slide 43, ≈50:33–51:20).

## Where this comes up

- [Lecture 7 — The Three Laws of AI](07-three-laws-of-ai.md): the whole lecture; sections 2–3 (Asimov),
  9 and 11–13 (jailbreaks), 15 (safety drift), 17 (agents) and 18–20 (modern laws).
- [Lecture 6 — Language Models and New Frontiers](06-language-models-new-frontiers.md), sections 10–11
  and 25: adversarial attacks, algorithmic bias and the limitations of LLMs.
- [Lecture 5 — Reinforcement Learning](05-reinforcement-learning.md), section 22: preference alignment.
