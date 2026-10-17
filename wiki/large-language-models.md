# Large language models

A **large language model (LLM)** is, for simplicity, a very large neural network trained on a very large
set of text (lecture 6, ≈44:07). The dominant way to train one is **next-token prediction**: given a
sequence of tokens, predict the next token, scored with a cross-entropy loss. The text supplies its own
labels, so no annotation is needed, and the combination of that simple objective with very large data,
models and compute is what gives LLMs their capabilities. Citations are to
[lecture 6](06-language-models-new-frontiers.md) unless another lecture is named; "slide N" is page N of
that lecture's PDF.

## Where LLMs sit

Slide 69 nests LLMs inside the course's opening definitions (≈44:07): "Artificial Intelligence" ("Any
technique that enables computers to mimic human behavior") contains "Deep Learning" ("Extract patterns
from data using neural networks"), which contains "Large Language Models" ("Very, very large neural
networks trained on very, very large sets of text"). They are a special class of deep learning models,
trained with different tasks or objectives in general-purpose ways. See
[what is deep learning?](what-is-deep-learning.md)

![Slide 69: LLMs inside deep learning inside AI](../raw/images/06-language-models-new-frontiers/slide-69.jpg)

*Lecture 6, slide 69 — large language models within deep learning, within artificial intelligence.*

## Training data and tokens

The pipeline behind models like GPT (slide 70, ≈44:52–45:37) starts from a general-purpose, unannotated
dataset scraped from the web: Common Crawl, Wikipedia, WebText, code and other text. The text is split into
chunks called **tokens** — that chunking is what "tokenization" means — and each token has a numerical ID,
which is what the model takes as input, after embedding (≈44:52–47:08). On turning words into numbers, and
embeddings, see [sequence modeling](sequence-modeling.md).

On scale (≈45:37): GPT-3 was reported to have 175 billion parameters (slide 70, "175B parameters
(GPT3)"), and later GPT models have often scaled beyond that; at the other end, small language models such
as Liquid AI's are orders of magnitude smaller and still capable.

## Next-token prediction and the loss

The task and objective (slide 70): "Given a sequence of tokens, predict the next token. Update model
parameters given how good next-token prediction is." It is the next-word prediction problem that lecture 2
calls "the basis for basically all language models" (see [sequence modeling](sequence-modeling.md)).

Slide 71 works it through on "MIT deep learning is so awesome" (≈47:08–48:40). The text is tokenized —
shown as words for simplicity — and embedded, and the LLM predicts each next token. Its output at each
position is a **probability for every token in the vocabulary**. Because the vocabulary is a discrete set,
predicting the next token is a **classification** problem, and the loss is the **cross-entropy** between
the predicted probabilities and the true next token, as for classification in lecture 1 (see
[loss functions](loss-functions.md)).

![Slide 71: next-token prediction and the cross-entropy loss](../raw/images/06-language-models-new-frontiers/slide-71.jpg)

*Lecture 6, slide 71 — tokens in, a probability for every possible next token out, compared with the true next token by a cross-entropy loss.*

What makes this "so beautiful in its simplicity" (≈48:40): the data are their own signal. No external
labels are required beyond the structure of the text itself, so the same loss can learn structure in very
large, very complex text datasets.

## From base model to chatbot

A **base** language model does next-token prediction. The models people use have been tuned and refined
afterwards to follow structured prompts and act as chatbots and interactive agents, with a clear split
between the user's prompt and the model's response (≈49:25–50:10). Slide 72's example: "I'm giving a talk
on AI at MIT. Can you outline it?" in, a four-part outline out. Lecture 6 does not say how that tuning is
done. [Lecture 5](05-reinforcement-learning.md) describes one part of it: after imitation by next-word
prediction, LLMs face a "preference alignment problem", and the thumbs up and down users give a chatbot
train a reward model for reinforcement learning (lecture 5, ≈53:53–54:39; see
[reinforcement learning](reinforcement-learning.md)). The course's third software lab fine-tunes an LLM
(slide 78).

Lecture 6 does not discuss the architecture inside an LLM. Lecture 2 ends by saying self-attention is the
basis for many large language models, and that transformers power language models such as BERT and GPT
(see [attention and transformers](attention-and-transformers.md)).

## Capabilities and limitations

The simple objective, combined with the scale of data, models and compute, lets LLMs learn patterns in
very large datasets (≈50:10). Slide 73 lists capabilities "feasible and reliable now": knowledge retrieval,
a writing co-pilot and a planning co-pilot — "LLMs like GPT have shown mastery over natural language."

The limitations echo [those of deep learning in general](limitations-of-deep-learning.md) (slide 74,
≈50:10–51:43):

- **Robustness and confidence.** A very probable generation is not the same as a confident one, and
  quantifying LLM uncertainty is still open (slide 74, "Robustness: How confident?", with a garbled prompt
  as its example).
- **Hallucination.** Text that seems feasible, consistent and logical but is not right, as someone who
  knows the field can tell ("'Hallucinations': Confidently wrong"). Amini adds that recent work has shown
  that well-calibrated language models will necessarily hallucinate (≈51:43).
- **Jailbreaks.** As with adversarial attacks, there are still ways to jailbreak these models and probe
  them to expose adversarial failure modes ("Guardrails and Jailbreaks").
- **Long-term planning and logic.** Recent advances in reasoning help, but there is still a long way to go
  ("Logic and Numerics").

## Emergent abilities

Over the past couple of years, LLMs have been seen to **generalize** to tasks that stretch their
capabilities, and much of this is attributed to **emergent abilities** (≈52:30). Systematic evaluation as
a function of training data and model size found that, past a threshold of scale, capabilities change in
steps that seem to come only from scaling data, compute and parameters (≈52:30–53:15). Slide 75 (credited
"Wei+ TMLR 2022.") defines it: "An ability is **emergent** if it is not present in smaller models but is
present in larger models." Its three charts — structuring language, understanding phonetics, performing
arithmetic — stay at their baseline across smaller models and rise sharply at the largest.

![Slide 75: emergent abilities with scale](../raw/images/06-language-models-new-frontiers/slide-75.jpg)

*Lecture 6, slide 75 — performance flat at the baseline for smaller models, then a sharp rise at the largest scales.*

The picture is a hierarchy of abilities unlocked as models grow (≈53:15; slide 76's tree of question
answering, arithmetic and language understanding). Lecture 6 ends on what this suggests (slide 77,
"Foundation Models Spawn a Powerful Idea"): a central reasoning system for general-purpose AI, and the
relationship between artificial and human intelligence — the goal being that these models remain a
technology that augments and accelerates human capabilities (≈54:02–54:49).

## Where this comes up

- [Lecture 6 — Language Models and New Frontiers](06-language-models-new-frontiers.md), sections 21–27.
- [Lecture 2 — Recurrent Neural Networks, Transformers, and Attention](02-rnns-transformers-attention.md):
  next-word prediction, embeddings and self-attention.
- [Lecture 5 — Reinforcement Learning](05-reinforcement-learning.md), section 22: preference alignment.
- [Lecture 1 — Introduction to Deep Learning](01-introduction.md): cross-entropy loss, and lab 3.
