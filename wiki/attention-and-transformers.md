# Attention and transformers

**Self-attention** lets a network learn which parts of an input matter most for representing that
input, and extract them, without processing the input step by step. It is "the foundational building
block of the **Transformer** architecture" — the "T" in GPT and BERT — and it is introduced in MIT
6.S191 [lecture 2](02-rnns-transformers-attention.md) (sections 10–13, ≈40:58–55:41) as the answer to
the limitations of [recurrent neural networks](recurrent-neural-networks.md).

## Why: eliminating recurrence

RNNs carry everything through an internal state, one step at a time, so they have an encoding
bottleneck, cannot be parallelized and have short memory (slide 61). Ideally a sequence model would see
a continuous stream, parallelize, and have long memory (slide 62). Simply concatenating every time step
into one input for a dense network removes the recurrence, but it is not scalable, loses the order,
and has no long memory (slides 63–64, ≈40:58–41:46). What is missing is a way to identify and attend
to what's important (slide 64).

## The intuition: search

Attention has two steps: **identify which parts to attend to**, then **extract the features with high
attention** (slide 66, ≈43:18–44:03). The first is "very similar to this notion of search". Searching
YouTube for "deep learning" (slides 67–69, ≈44:03–46:22):

- the search term is the **query** ($Q$);
- each video's title is a **key** ($K$); comparing every key with the query gives an **attention mask**
  of how similar each is — a sea-turtle video scores low, an introductory deep learning lecture high;
- the video you then retrieve is the **value** ($V$).

![Slide 69: Understanding Attention with Search](../raw/images/02-rnns-transformers-attention/slide-69.jpg)

*Lecture 2, slide 69 — query, keys and the value of a YouTube search.*

## Self-attention in four steps

Lecture 2 works through the sentence "He tossed the tennis ball to serve" (slides 70–77, ≈47:10–53:22).
In self-attention the relationships are found within one input sequence itself.

**1. Encode position.** The data is fed in all at once, so order must be preserved another way: a
**positional embedding** combines each token's embedding with position information (slide 71). The
lecture does not go into how it is implemented (≈47:57).

**2. Extract query, key and value.** Three separate learned layers transform the same positional
embedding into a query matrix, a key matrix and a value matrix, each capturing different information
(slide 72, ≈48:43–49:29).

**3. Compute the attention weighting.** The similarity of queries and keys is their dot product, scaled
— which the slide and the lecturer also call the "cosine similarity" (slides 73–74, ≈49:29–50:16). A
softmax squashes the scores to values between zero and one (slide 75, ≈51:50):

$$\text{softmax}\left(\frac{Q \cdot K^T}{\text{scaling}}\right)$$

The slide gives the denominator only as "scaling".

**4. Extract features with high attention.** Multiply the attention weighting by the values (slide 76,
≈51:50–52:36):

$$\text{softmax}\left(\frac{Q \cdot K^T}{\text{scaling}}\right) \cdot V = A(Q, K, V)$$

The resulting attention matrix shows how strongly each word relates to every other. The diagonal is
highest, since each word matches itself, but related words also score high — "ball" with "tossed"
(slide 75, ≈51:02).

![Slide 75: Learning Self-Attention with Neural Networks](../raw/images/02-rnns-transformers-attention/slide-75.jpg)

*Lecture 2, slide 75 — attention weights for "He tossed the tennis ball to serve".*

## Attention heads and transformers

These operations together form a **self-attention head** that can plug into a larger network: linear
layers for the query, key and value; a matrix multiplication of query and key; scaling; softmax; and a
final multiplication with the value (slide 77, ≈52:36–53:22).

![Slide 77: Learning Self-Attention with Neural Networks](../raw/images/02-rnns-transformers-attention/slide-77.jpg)

*Lecture 2, slide 77 — one self-attention head.*

Attention is very parallelizable, and several heads can be stacked in one network, each learning a
different pattern of importance — in the lecture's image example, one head picks out Iron Man, another
a building, another something in the background (slide 79, ≈53:22–54:09). Transformers built this way
power language models such as BERT and GPT, protein structure models for biological sequences, and
vision transformers in computer vision (slide 80, ≈54:54). Lecture 2 says vision transformers come up in
lecture 3, but [lecture 3](03-convolutional-neural-networks.md) as delivered is about convolutional
networks and does not mention them.

## Where this comes up

- [Lecture 2 — Recurrent Neural Networks, Transformers, and Attention](02-rnns-transformers-attention.md),
  sections 10–13.
