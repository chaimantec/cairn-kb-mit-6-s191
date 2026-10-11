# What is deep learning?

Deep learning is the part of machine learning that uses neural networks — specifically deep ones — to
learn a task directly from raw data. MIT 6.S191 frames the whole course around that one sentence:
"teaching computers how to learn a task directly from raw data"
([lecture 1](01-introduction.md), slide 7, ≈9:22).

## AI, machine learning, deep learning

The three terms nest inside one another ([lecture 1](01-introduction.md), slide 7, ≈7:47–9:22):

- **Intelligence**, as Alexander Amini defines it, is processing information in order to inform some
  future decision. **Artificial intelligence** is a machine doing the same; slide 7 puts it as "any
  technique that enables computers to mimic human behavior".
- **Machine learning** is the subset of AI that does this *without being explicitly programmed* with
  the steps: it learns how to process the information from data. That is the dividing line between ML
  and AI in general.
- **Deep learning** is the subset of ML that does the learning with neural networks — "extract
  patterns from data using neural networks".

![Slide 7: What is Deep Learning?](../raw/images/01-introduction/slide-7.jpg)

*Lecture 1, slide 7 — artificial intelligence ⊃ machine learning ⊃ deep learning.*

## Why learn features instead of engineering them?

Traditional machine learning relies on features designed by hand, which lecture 1 calls "time
consuming, brittle, and not scalable in practice" (slide 18, ≈12:30). Deep learning instead learns the
features from data, and learns them as a **hierarchy**: low-level lines and edges are composed into
mid-level parts such as eyes, noses and ears, and those into high-level structure such as a whole face
(slide 18, ≈13:16–14:03). This mirrors how a person might reason from first principles about whether
an image contains a face.

## Why now?

The building blocks are decades old. Lecture 1's timeline (slide 19) dates stochastic gradient descent
to 1952, the perceptron to 1958, backpropagation to 1986 and deep convolutional networks for digit
recognition to 1995. Their recent dominance comes from three things (≈14:03–15:37):

1. **Big data**: larger datasets that are easier to collect and store, and these algorithms "live off
   of data".
2. **Hardware**: GPUs, which make the computation massively parallel.
3. **Software**: improved techniques, new models, and toolboxes such as TensorFlow and PyTorch that
   democratize building, training and deploying models.

## Where this comes up

- [Lecture 1 — Introduction to Deep Learning](01-introduction.md), sections 1, 2 and 4: the pace of
  the field, the definitions, and why deep learning works now.
- The building block every later idea rests on is the [perceptron](perceptron.md).
