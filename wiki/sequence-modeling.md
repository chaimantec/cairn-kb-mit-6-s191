# Sequence modeling

Sequence modeling is learning from data that is resolved in time, or that can be modeled as a
sequence, in order to predict something about it: the next position of a moving ball, the next word
of a sentence, the sentiment of a tweet. In MIT 6.S191 it is the subject of
[lecture 2](02-rnns-transformers-attention.md), where Ava Amini calls it "a very very powerful and
general paradigm" that has become super relevant with the arrival of powerful language models (≈0:00).

## Why the history matters

Lecture 2 opens with a ball in a 2D space. From a single snapshot, any guess about where it goes next
is "a random proposal"; given its past positions as well, the most likely next path is obvious (slides
2–5, ≈1:32). Sequential data of this kind is "truly all around us": audio split into chunks of sound
waves, text split into characters or words, medical signals, financial time series, biological
sequences, patterns of movement, video and weather (slides 6–7, ≈2:18–3:04).

## Four shapes of problem

Sequence tasks are classified by how many inputs map to how many outputs (slides 8 and 29,
≈3:49–4:36, ≈20:46–21:32):

| Shape | Lecture's examples |
| --- | --- |
| One to one | A "vanilla" network for binary classification: lecture 1's "Will I pass this class?" |
| Many to one | Sentiment classification: a tweet in, an emotion or sentiment out |
| One to many | Image captioning (an image in, a sentence describing it out); text generation |
| Many to many | Translation (English text into Mandarin), forecasting, music generation |

Language modeling, machine translation and much of natural language processing are many-to-many
problems (≈21:32).

![Slide 29: RNNs for Sequence Modeling](../raw/images/02-rnns-transformers-attention/slide-29.jpg)

*Lecture 2, slide 29 — one to one, many to one, one to many and many to many, with applications under each.*

## Design criteria, through next-word prediction

Next-word prediction — given "This morning I took my cat for a", predict "walk" — is "the basis for
basically all language models" (slides 32–34, ≈21:32–23:08). Lecture 2 uses it to set out what any
sequence model must be able to do, and Amini recommends the same habit for your own work: relate the
problem to design criteria, then choose the architecture (≈22:20). The slides list four criteria
(slides 30 and 40), and the lecture adds a fifth aloud, which it calls "number one" (≈27:46):

1. **Represent the data numerically.** Neural networks "cannot interpret words"; they operate on
   numbers (slide 35, ≈24:43). See the next section.
2. **Handle variable-length sequences.** "The food was great" and "We were hungry but cleaned the house
   before eating" must both work (slide 37, ≈28:32). A feed-forward network takes a fixed number of
   inputs and breaks down here; a model that processes the data one step at a time does not.
3. **Track long-term dependencies.** In "**France** is where I grew up, but I now live in Boston. I
   speak fluent ___.", the clue comes from the distant past (slide 38, ≈29:17).
4. **Maintain information about order.** "The food was good, not bad at all" and "The food was bad, not
   good at all" use the same words with opposite meanings (slide 39, ≈29:17).
5. **Share parameters across the sequence** (slides 30 and 40).

[Recurrent neural networks](recurrent-neural-networks.md) meet these criteria (slide 40, ≈30:04).
Their limitations led to [attention and transformers](attention-and-transformers.md), which process
the whole sequence at once and so have to encode order separately, as a positional embedding.

## Representing language as numbers: embeddings

To feed words to a network, they must become vectors, and the network's numerical prediction must be
mapped back to a word (≈24:43–25:28). Ideally the numbers also capture meaning: "learning" and
"education" should land closer together than "learning" and "tennis" (≈25:28). Slide 36 calls this an
**embedding** — "transform indexes into a vector of fixed size" — built in three steps:

1. **Vocabulary**: the corpus of words.
2. **Indexing**: each word gets a unique index ("a" → 1, "cat" → 2, …, "walk" → N).
3. **Embedding**: each index becomes a fixed-size vector.

A **one-hot** embedding puts a single 1 at the word's index and zeros elsewhere ("cat" = [0, 1, 0, 0,
0, 0]); it identifies the word but says nothing about its meaning (≈26:14). A **learned** embedding
places related words near each other — on the slide, "run" near "walk", "dog" near "cat", "day" near
"sun", "happy" near "sad". The popular schemes in today's language models map chunks of words that
frequently occur together to nearby parts of the embedding space (≈27:01). In a student exchange the
lecture also mentions tokenization as one strategy for turning text into numbers (≈23:56–25:28); it
does not go into a particular tokenizer.

![Slide 36: Encoding Language for a Neural Network](../raw/images/02-rnns-transformers-attention/slide-36.jpg)

*Lecture 2, slide 36 — vocabulary, word-to-index, one-hot embedding and learned embedding.*

The general point holds beyond language: whatever the data modality, you have to find a way to map it
into numerical input the network can process (≈27:46).

## Where this comes up

- [Lecture 2 — Recurrent Neural Networks, Transformers, and Attention](02-rnns-transformers-attention.md),
  sections 1, 2 and 5.
