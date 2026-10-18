# AI agents

An **AI agent**, in the sense of the guest lecture [The Three Laws of AI](07-three-laws-of-ai.md)
(lecture 7, Douglas Blank), is "a software system that can do things on behalf of the user" (slide 34).
In practice it is a language model given **tools**, functions it can call to act on the world. The course
also uses "agent" in an older, different sense, in reinforcement learning (see the last section).

## Two definitions

Asked what agentic AI is, Gemini gave Blank a long answer (lecture 7, slide 33). An agent is a software
system that observes its environment, uses its capabilities, often built on an LLM, to reason and plan,
and acts to achieve goals autonomously. Such agents can learn from experience, access tools and data, and
collaborate with other agents. "That's probably not what we're talking about today" (≈36:33). The
working definition is the short one on slide 34: you ask the LLM to do something, "and it's capable of
doing that for you" (≈36:33).

## Why an LLM needs tools

On its own, a language model cannot say what time it is, or what the weather in Boston is. It has no
real-time data (lecture 7, ≈37:23–38:12). "It's just a language model. It's statistical. It's just
predicting, you know, what the next word should be" (≈38:12; see
[large language models](large-language-models.md)). Adding a tool fixes that "very easily". A tool is
a function the model can choose to call.

## Building one in 90 seconds

Blank's demonstration (lecture 7, ≈37:23–45:57) used a handful of Python functions:

- a clock;
- a weather tool returning a random temperature, with no units;
- an email sender, a stub that sends nothing;
- an appointment maker;
- at a student's suggestion, "delete my files", which takes no argument and returns "okay".

"So, there in 90 seconds we created an agentic system. That's really that simple" (≈39:44). A small
program, "Easy MCP Chatbot", loaded the tools and logged every exchange to Opik as a trace (≈39:44–40:29).

The model then used the tools in ways nobody spelled out. Asked to "send them email letting them know"
after booking an appointment with Joe and Sarah, it worked out whom to email (≈42:05). Asked for the
temperatures of cities in Massachusetts, it used the weather tool to answer. It reused Boston's earlier
answer rather than recomputing it (≈43:41–45:12). LLMs are "an emergent layer on top of deep learning", and with tools they can be
used in lots of interesting ways, dynamically, "we hope, the way they were intended" (≈42:52–43:41).

## Why agents must be tested

The same session showed why. The agent booked "next Thursday" as January 12th, which was wrong
(≈41:18, ≈44:26). Asked to delete the files, it reported "your files have been successfully deleted"
(≈42:05). "Can you trust LLMs? No. Can you trust an agentic AI system built on LLMs? No. So, yeah, we
definitely need to test these" (≈44:26).

The traces are how such a failure is found. Viewing the conversation as a thread in Comet showed the
appointment maker being called with the wrong date, though the functions were otherwise called as
intended (≈45:12–45:57). Testing an agent uses the same tools as [evaluating LLMs](llm-evaluation.md),
and Blank's last law of AI singles agents out: think about harm to humanity as you deploy "especially
LLMs, and especially LLMs that are agentic" (≈51:20; see [AI safety](ai-safety.md)).

Lecture 6 notes that the models people use have been tuned after pretraining to act "as chatbots and
interactive agents" (lecture 6, ≈49:25).

## "Agent" in reinforcement learning

In [lecture 5](05-reinforcement-learning.md) the **agent** is the learner in a reinforcement learning
problem: something that "takes actions" in an environment, observes the new state and receives rewards,
such as a delivery drone or Super Mario (lecture 5, slides 8–17; see
[reinforcement learning](reinforcement-learning.md)). Lecture 7's Gemini definition touches the same idea,
an agent that observes its environment and acts toward goals. The agents lecture 7 builds, though, are
LLMs calling tools, and nothing in them is trained by reward.

## Where this comes up

- [Lecture 7 — The Three Laws of AI](07-three-laws-of-ai.md), sections 16–17.
- [Lecture 5 — Reinforcement Learning](05-reinforcement-learning.md): the agent, environment, actions and
  rewards of reinforcement learning.
- [Lecture 6 — Language Models and New Frontiers](06-language-models-new-frontiers.md), section 24: base
  models tuned into chatbots and interactive agents.
