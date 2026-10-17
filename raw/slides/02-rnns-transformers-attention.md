---
title: Lecture 2 — Recurrent Neural Networks, Transformers, and Attention (slide deck)
lecture: 2
slides: 83
source_pdf: https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L2.pdf
note: Slide N = PDF page N (N = 1..83). The deck prints no slide numbers; the "1/5/26" in each footer is the lecture date (5 January 2026).
---

# Lecture 2 — Recurrent Neural Networks, Transformers, and Attention: slide-by-slide

Text and figures of all 83 slides of
[`6S191_MIT_DeepLearning_L2.pdf`](https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L2.pdf)
(MIT 6.S191 Introduction to Deep Learning, 2026 edition; lecturer Ava Amini; the title slide reads
"Deep Sequence Modeling"), transcribed from the deck. Cite these as "slide N", where N is the PDF
page number. Diagrams, photographs and code are described in prose or reproduced, since the KB is
read as text.

Many slides are **build steps**: the same slide re-shown with one more element revealed. They are
transcribed individually, so that a citation to any one of them resolves, with a note of what each
adds to the one before.

## Numbering: slide numbers vs PDF pages

The PDF is a flattened export: every page is a single 1280×720 image with no text layer, and no
page prints a slide number. Headings therefore use the PDF page number, and a reader who opens page
N of the PDF sees slide N. The standard footer on content slides (MIT logo, "MIT Introduction to
Deep Learning", introtodeeplearning.com, @MITDeepLearning, "1/5/26") is not repeated below; citations
printed beside it are. Slides 2–5 have no footer.

## Contents

| Slides | Section |
| ------ | ------- |
| 1 | Title: "Deep Sequence Modeling" |
| 2–8 | Why sequences: the ball example, sequences in the wild, sequence modeling applications (one to one, many to one, one to many, many to many) |
| 9–15 | Neurons with recurrence: the perceptron and feed-forward networks revisited, handling individual time steps, linking time steps through a hidden state |
| 16–29 | Recurrent neural networks: the recurrence relation, pseudocode intuition, state update and output, the computational graph across time, an RNN cell from scratch in TensorFlow, built-in TensorFlow and PyTorch layers, RNN input/output configurations |
| 30–40 | Sequence modeling design criteria, worked through next-word prediction: encoding language (vocabulary, indexing, one-hot and learned embeddings), variable lengths, long-term dependencies, order |
| 41–54 | Backpropagation through time: feed-forward backpropagation recalled, BPTT, gradient flow, exploding and vanishing gradients, the problem of long-term dependencies, gating and LSTMs |
| 55–64 | RNN applications and limitations: music generation, sentiment classification, the three limitations, the goal of sequence modeling, eliminating recurrence |
| 65–80 | "Attention Is All You Need": the intuition behind self-attention, search as query, key and value, self-attention step by step, the attention head, multiple heads, applications |
| 81–83 | Summary; Lab 1; kickoff reception |

## Slide 1 — Deep Sequence Modeling

Title slide. Black background; at left a glowing blue network of nodes and lines (a graph-like mesh). Faint large watermark "MIT 6.S191" runs diagonally behind the text. Text, centred at right:

"Deep Sequence Modeling"
"Ava Amini"
"MIT Introduction to Deep Learning"
"January 5, 2026"

An "MIT EECS" logo sits at bottom right.

*Figure: no*

## Slide 2 — [Given an image of a ball, can you predict where it will go next?]

Blue background. Title text: "Given an image of a ball, can you predict where it will go next?" Below it, a single white filled circle (the ball) near the centre, with no arrows.

*Figure: yes — single white circle (a ball) on blue background*

## Slide 3 — [Given an image of a ball, can you predict where it will go next?]

![Slide 3 — [Given an image of a ball, can you predict where it will go next?]](../images/02-rnns-transformers-attention/slide-3.jpg)

Build step: adds arrows and "???" to slide 2.

Same title text: "Given an image of a ball, can you predict where it will go next?" The white circle now has four white arrows pointing away from it in different directions (up-right, left-up, right-down, and down), with the label "???" beside the right-pointing arrow. It shows that with a single image the direction is ambiguous.

*Figure: yes — ball with four arrows in different directions and "???"*

## Slide 4 — [Given an image of a ball, can you predict where it will go next?]

Same title text: "Given an image of a ball, can you predict where it will go next?" The slide shows four circles in a horizontal row at left: three fainter, semi-transparent circles followed by one solid white circle at the right end (the ball's previous positions fading into the current position). No arrows.

*Figure: yes — row of three faded circles and one solid circle showing a ball's past positions*

## Slide 5 — [Given an image of a ball, can you predict where it will go next?]

![Slide 5 — [Given an image of a ball, can you predict where it will go next?]](../images/02-rnns-transformers-attention/slide-5.jpg)

Build step: adds an arrow to slide 4.

Same title text: "Given an image of a ball, can you predict where it will go next?" Same row of three faded circles and one solid white circle, plus a single white arrow to the right of the solid circle pointing right (the predicted direction).

*Figure: yes — past ball positions with a single rightward arrow*

## Slide 6 — Sequences in the Wild

Centre: a blue audio waveform (amplitude versus time, no axis labels or numbers) that starts with large spikes at the left, then settles to a lower, fairly uniform amplitude with a few isolated spikes. Caption below: "Audio"

*Figure: yes — blue audio waveform*

## Slide 7 — Sequences in the Wild

Same title as slide 6; the waveform is replaced by further examples (no captions are printed).

A collage of overlapping photos, with no captions or labels except a date stamp in one image:
- Top left: a stock-market screen of green and red price numbers with a rising green candlestick/line chart.
- Top centre: a camera on a tripod whose rear screen shows a smiling woman, with a blurred woman gesturing in the background (video).
- Top right: lines of letters A, C, G and T (DNA sequence text) on a dark blue background.
- Bottom left: a photo of a man in a red top and dark shorts running, with motion blur in a green background.
- Bottom centre: an electrocardiogram (ECG) paper strip with a heartbeat trace on gridded paper.
- Right: a false-colour globe viewed from the south pole (blue centre, green, yellow and red outwards) with the date text "p 08, 2019" partly visible at top left (the beginning of the date is covered by another image).

*Figure: yes — collage of sequence data types: stock prices, video, DNA, motion, ECG, and a dated polar globe map*

## Slide 8 — Sequence Modeling Applications

![Slide 8 — Sequence Modeling Applications](../images/02-rnns-transformers-attention/slide-8.jpg)

Four diagrams of recurrent networks, in columns (a vertical black line separates the first column from the other three). In each, a blue circle row at the bottom is the input, green rounded rectangles in the middle are network units, and purple circles at the top are the outputs. Arrows point from input up to unit and from unit up to output; in multi-unit diagrams horizontal arrows connect each green unit to the next one on its right.

1. "One to One" / "**Binary Classification**": one blue circle labelled $x$, one green box, one purple circle labelled $\hat{y}$. Image: a green thumbs-up and a red thumbs-down. Text: "Will I pass this class?" / "Student → Pass?"
2. "Many to One" / "**Sentiment Classification**": three blue input circles, three connected green boxes, a single purple output circle above the rightmost box. Image: a tweet by Ivar Hagendoorn reading "The @MIT Introduction to #DeepLearning is definitely one of the best courses of its kind currently available online introtodeeplearning.com" (timestamp "12:45 PM - 12 Feb 2018"), with a smiling emoji below it.
3. "One to Many" / "**Image Captioning**": one blue input circle under the leftmost of three connected green boxes, three purple output circles. Image: a photo of a baseball pitcher in a grey uniform mid-throw. Caption: "A baseball player throws a ball."
4. "Many to Many" / "**Machine Translation**": three blue input circles, three connected green boxes, three purple output circles. Image: the Google Translate-style blue icon (a Chinese character and the letter "A").

*Figure: yes — four recurrent-network diagrams (one-to-one, many-to-one, one-to-many, many-to-many) with example images*

## Slide 9 — Neurons with Recurrence

Section-divider slide: blue background, centred white title "Neurons with Recurrence".

*Figure: no*

## Slide 10 — The Perceptron Revisited

![Slide 10 — The Perceptron Revisited](../images/02-rnns-transformers-attention/slide-10.jpg)

Diagram: three blue input circles stacked vertically, labelled $x^{(1)}$, $x^{(2)}$, $x^{(m)}$. Arrows from each go to a single green circle labelled $z$; the arrows are labelled $w_1$, $w_2$ and $w_m$ respectively. From $z$ a black arrow labelled $y = g(z)$ goes to a purple circle labelled $\hat{y}$.

*Figure: yes — perceptron diagram: inputs* $x^{(1)}..x^{(m)}$ *with weights into* $z$, *then* $y=g(z)$ *to* $\hat{y}$

## Slide 11 — Feed-Forward Networks Revisited

![Slide 11 — Feed-Forward Networks Revisited](../images/02-rnns-transformers-attention/slide-11.jpg)

Diagram: three blue input circles labelled $x^{(1)}$, $x^{(2)}$, $x^{(m)}$ at left, each with arrows to every one of four small green circles stacked inside a larger green rounded rectangle (fully connected layer). Each green circle has one arrow to its own purple output circle at right, labelled $\hat{y}^{(1)}$, $\hat{y}^{(2)}$, $\hat{y}^{(3)}$, $\hat{y}^{(n)}$. Below the left side: $\boldsymbol{x} \in \mathbb{R}^m$. Below the right side: $\hat{\boldsymbol{y}} \in \mathbb{R}^n$.

*Figure: yes — fully connected feed-forward layer from* $\boldsymbol{x} \in \mathbb{R}^m$ *to* $\hat{\boldsymbol{y}} \in \mathbb{R}^n$

## Slide 12 — Feed-Forward Networks Revisited

Diagram: a blue circle labelled $x_t$ with an arrow to a single large green rounded rectangle (no label inside), which has an arrow to a purple circle labelled $\hat{y}_ t$. Below the left: $\boldsymbol{x_t} \in \mathbb{R}^m$. Below the right: $\hat{\boldsymbol{y}}_ t \in \mathbb{R}^n$.

*Figure: yes — the feed-forward network collapsed to one box from* $x_t$ *to* $\hat{y}_ t$

## Slide 13 — Handling Individual Time Steps

![Slide 13 — Handling Individual Time Steps](../images/02-rnns-transformers-attention/slide-13.jpg)

Left of a vertical black line: a single column with a blue circle $x_t$ (labelled "input vector"), an arrow up to a green rounded rectangle, and an arrow up to a purple circle $\hat{y}_ t$ (labelled "output vector").

Right of the line: three such columns side by side, each with its own green box and no connections between the boxes: inputs $x_0$, $x_1$, $x_2$ and outputs $\hat{y}_ 0$, $\hat{y}_ 1$, $\hat{y}_ 2$. A blue rectangle outlines the inputs $x_0$ and $x_1$; a purple rectangle outlines the output $\hat{y}_ 2$. Below, the equation:

$$\hat{y}_ t = f(x_t)$$

*Figure: yes — independent feed-forward copies at each time step, with no links between them*

## Slide 14 — Neurons with Recurrence

Same layout as slide 13 (the single column with "input vector" $x_t$ and "output vector" $\hat{y}_ t$ on the left of a vertical line; three columns with inputs $x_0$, $x_1$, $x_2$, outputs $\hat{y}_ 0$, $\hat{y}_ 1$, $\hat{y}_ 2$ on the right), without the blue and purple outline rectangles. New: horizontal arrows join the green boxes, labelled $h_0$ (from the first box to the second) and $h_1$ (from the second to the third). Below, the equation:

$$\hat{y}_ t = f(x_t, h_{t-1})$$

with colour-coded underlines and labels: $\hat{y}_ t$ underlined in purple labelled "output"; $x_t$ underlined in blue labelled "input"; $h_{t-1}$ underlined in orange labelled "past memory".

*Figure: yes — unrolled chain of three boxes linked by* $h_0$, $h_1$, *with the equation* $\hat{y}_ t = f(x_t, h_{t-1})$

## Slide 15 — Neurons with Recurrence

![Slide 15 — Neurons with Recurrence](../images/02-rnns-transformers-attention/slide-15.jpg)

Build step: adds the recurrent loop to slide 14.

Same as slide 14, plus: the left single-column box is now labelled "recurrent cell" and has a feedback loop, an arrow leaving the right side of the box, going up, left over the box and back into its left side, with the label $h_t$ at the right side of the box. The right-hand unrolled diagram and the equation $\hat{y}_ t = f(x_t, h_{t-1})$ (with "output", "input", "past memory" labels) are unchanged.

$$\hat{y}_ t = f(x_t, h_{t-1})$$

*Figure: yes — recurrent cell with a feedback loop* $h_t$, *shown beside its unrolled three-step version*

## Slide 16 — Recurrent Neural Networks (RNNs)

Section-divider slide: blue background, centred white title "Recurrent Neural Networks (RNNs)".

*Figure: no*

## Slide 17 — Recurrent Neural Networks (RNNs)

![Slide 17 — Recurrent Neural Networks (RNNs)](../images/02-rnns-transformers-attention/slide-17.jpg)

Left: a diagram of a green rounded box labelled "RNN" with a blue circle $x_t$ below it (label "input vector") and an arrow up to a purple circle $\hat{y}_ t$ above it (label "output vector"). A feedback loop leaves the right side of the box, goes up and over, and returns into the left side; the label $h_t$ sits at the right side of the box.

Right: text "Apply a **recurrence relation** at every time step to process a sequence:" followed by the equation

$$h_t = f_W(x_t, h_{t-1})$$

with colour-boxed parts and labels below: $h_t$ (green box) labelled "cell state"; $f_W$ (green box) labelled "function with weights W"; $x_t$ (blue box) labelled "input"; $h_{t-1}$ (orange box) labelled "old state".

Below the equation: "Note: the same function and set of parameters are used at every time step"

Bottom line: "RNNs have a **state**, $h_t$, that is updated **at each time step** as a sequence is processed"

*Figure: yes — RNN box with feedback loop* $h_t$, *and annotated recurrence relation*

## Slide 18 — RNN Intuition

Dark background. Left, a Python code block (the first four lines are enclosed in a green rounded rectangle on this slide):

```python
my_rnn = RNN()
hidden_state = [0, 0, 0, 0]

sentence = ["I", "love", "recurrent", "neural"]

for word in sentence:
    prediction, hidden_state = my_rnn(word, hidden_state)

next_word_prediction = prediction
# >>> "networks!"
```

Right: the recurrent-cell diagram on a dark background: a green box labelled "RNN" with the smaller text "recurrent cell", blue circle $x_t$ below (label "input vector"), purple circle $\hat{y}_ t$ above (label "output vector"), a feedback loop from the right side of the box back into its left side, and the label $h_t$ beside the right side.

*Figure: yes — recurrent cell diagram (RNN box with feedback loop* $h_t$) *beside pseudocode*

## Slide 19 — RNN Intuition

Build step: moves the green highlight in slide 18 to the loop lines.

Same code and recurrent-cell diagram as slide 18. The green rounded rectangle now encloses the two lines "for word in sentence:" and "    prediction, hidden_state = my_rnn(word, hidden_state)".

```python
my_rnn = RNN()
hidden_state = [0, 0, 0, 0]

sentence = ["I", "love", "recurrent", "neural"]

for word in sentence:
    prediction, hidden_state = my_rnn(word, hidden_state)

next_word_prediction = prediction
# >>> "networks!"
```

Diagram labels: "output vector" $\hat{y}_ t$, "RNN" / "recurrent cell", $h_t$, "input vector" $x_t$.

*Figure: yes — recurrent cell diagram (RNN box with feedback loop* $h_t$) *beside pseudocode*

## Slide 20 — RNN Intuition

Build step: moves the green highlight in slide 19 to the last two lines.

Same code and recurrent-cell diagram as slide 18. The green rounded rectangle now encloses "next_word_prediction = prediction" and "# >>> "networks!"" (the comment is in grey).

```python
my_rnn = RNN()
hidden_state = [0, 0, 0, 0]

sentence = ["I", "love", "recurrent", "neural"]

for word in sentence:
    prediction, hidden_state = my_rnn(word, hidden_state)

next_word_prediction = prediction
# >>> "networks!"
```

Diagram labels: "output vector" $\hat{y}_ t$, "RNN" / "recurrent cell", $h_t$, "input vector" $x_t$.

*Figure: yes — recurrent cell diagram (RNN box with feedback loop* $h_t$) *beside pseudocode*

## Slide 21 — RNN State Update and Output

Left: the RNN diagram: a green box labelled "RNN" with a feedback loop (from the right side, over the top, into the left side) and the label $h_t$ at the right side; blue circle $x_t$ below labelled "input vector", with an arrow up into the box; an arrow from the box up to a purple circle $\hat{y}_ t$ labelled "output vector". The right side of the slide is empty.

*Figure: yes — RNN box with feedback loop* $h_t$, *input* $x_t$ *and output* $\hat{y}_ t$

## Slide 22 — RNN State Update and Output

Build step: adds the input vector label to slide 21.

Same RNN diagram as slide 21. At right, a blue heading "Input Vector" with $x_t$ beneath it.

*Figure: yes — RNN box with feedback loop* $h_t$, *input* $x_t$ *and output* $\hat{y}_ t$

## Slide 23 — RNN State Update and Output

Build step: adds the hidden-state update to slide 22.

Same RNN diagram as slide 21. At right, a teal heading "Update Hidden State" with the equation

$$h_t = \tanh(\boldsymbol{W}_ {hh}^T h_{t-1} + \boldsymbol{W}_ {xh}^T x_t)$$

and below it the blue heading "Input Vector" with $x_t$.

*Figure: yes — RNN box with feedback loop* $h_t$, *input* $x_t$ *and output* $\hat{y}_ t$

## Slide 24 — RNN State Update and Output

![Slide 24 — RNN State Update and Output](../images/02-rnns-transformers-attention/slide-24.jpg)

Build step: adds the output vector equation to slide 23.

Same RNN diagram as slide 21. At right, from top to bottom: a purple heading "Output Vector" with

$$\hat{y}_ t = \boldsymbol{W}_ {hy}^T h_t$$

then the teal heading "Update Hidden State" with

$$h_t = \tanh(\boldsymbol{W}_ {hh}^T h_{t-1} + \boldsymbol{W}_ {xh}^T x_t)$$

then the blue heading "Input Vector" with $x_t$.

*Figure: yes — RNN box with feedback loop* $h_t$, *input* $x_t$ *and output* $\hat{y}_ t$

## Slide 25 — RNNs: Computational Graph Across Time

At bottom left: the RNN diagram: blue circle $x_t$ with an arrow up into a green box labelled "RNN", which has a feedback loop (out of its right side, over the top, back into its left side) and an arrow up to a purple circle $\hat{y}_ t$. To its right an equals sign "=" and the text "Represent as computational graph unrolled across time".

*Figure: yes — RNN with feedback loop followed by an equals sign (unrolled graph not yet shown)*

## Slide 26 — RNNs: Computational Graph Across Time

![Slide 26 — RNNs: Computational Graph Across Time](../images/02-rnns-transformers-attention/slide-26.jpg)

Build step: adds the unrolled graph and loss to slide 25.

Top left legend: a black arrow labelled "Forward pass". Centred text: "Re-use the **same weight matrices** at every time step" (it overlaps the curved loss arrows).

Left: the folded RNN diagram from slide 25 (blue $x_t$, green box "RNN" with feedback loop, purple $\hat{y}_ t$), then "=".

Right: the unrolled graph with four green boxes in a row, with an ellipsis ("...") between the third and fourth columns. Per column:
- Inputs (blue circles, bottom): $x_0$, $x_1$, $x_2$, ..., $x_t$. Each has an arrow up into its box labelled $W_{xh}$.
- Boxes are joined by horizontal arrows to the right, each labelled $W_{hh}$ (three labelled arrows: box 1 to 2, box 2 to 3, box 3 to the last box).
- Each box has an arrow up labelled $W_{hy}$ to a purple output circle: $\hat{y}_ 0$, $\hat{y}_ 1$, $\hat{y}_ 2$, ..., $\hat{y}_ t$.
- Each output has an arrow up to an orange circle: $L_0$, $L_1$, $L_2$, and $L_3$ (the last column's loss is labelled $L_3$ while its input and output are labelled $x_t$ and $\hat{y}_ t$).
- Curved arrows from $L_0$, $L_1$, $L_2$ and $L_3$ all point to a larger orange square labelled $L$ at top right.

*Figure: yes — RNN unrolled across time with shared* $W_{xh}$, $W_{hh}$, $W_{hy}$, *per-step losses* $L_0..L_3$ *summed into* $L$

## Slide 27 — RNNs from Scratch in TensorFlow

Dark background; the TensorFlow logo (orange) at top right. Left, code (the comment-plus-code groups in the `call` method are each enclosed in a green rounded rectangle):

```python
class MyRNNCell(tf.keras.layers.Layer):
  def __init__(self, rnn_units, input_dim, output_dim):
    super(MyRNNCell, self).__init__()

    # Initialize weight matrices
    self.W_xh = self.add_weight([rnn_units, input_dim])
    self.W_hh = self.add_weight([rnn_units, rnn_units])
    self.W_hy = self.add_weight([output_dim, rnn_units])

    # Initialize hidden state to zeros
    self.h = tf.zeros([rnn_units, 1])

  def call(self, x):
    # Update the hidden state
    self.h = tf.math.tanh( self.W_hh * self.h + self.W_xh * x )

    # Compute the output
    output = self.W_hy * self.h

    # Return the current output and hidden state
    return output, self.h
```

Right: the recurrent-cell diagram: green box labelled "RNN" with the smaller text "recurrent cell", feedback loop with label $h_t$, blue circle $x_t$ ("input vector") below and purple circle $\hat{y}_ t$ ("output vector") above.

*Figure: yes — recurrent cell diagram (RNN box with feedback loop* $h_t$) *beside TensorFlow code*

## Slide 28 — RNN Implementation: TensorFlow & PyTorch

Dark background. Left, two code snippets, each with a framework logo beneath it: the TensorFlow logo (orange) under the first, the PyTorch logo (orange flame in a ring) under the second.

```python
from tf.keras.layers import SimpleRNN
    model = SimpleRNN(rnn_units)
```

```python
from torch.nn import RNN
  model = RNN(input_size, rnn_units)
```

Right: the recurrent-cell diagram: green box "RNN" / "recurrent cell", feedback loop with label $h_t$, blue circle $x_t$ ("input vector"), purple circle $\hat{y}_ t$ ("output vector").

(The slide prints "from tf.keras.layers import SimpleRNN", which is not a valid Python import path as printed; kept as is. Indentation is as printed: in the TensorFlow snippet the second line is indented, in the PyTorch snippet the first.)

*Figure: yes — recurrent cell diagram (RNN box with feedback loop* $h_t$) *beside TensorFlow and PyTorch snippets with logos*

## Slide 29 — RNNs for Sequence Modeling

![Slide 29 — RNNs for Sequence Modeling](../images/02-rnns-transformers-attention/slide-29.jpg)

Four diagrams in a row, each built from blue input circles at the bottom, green rounded boxes (RNN cells) in the middle and purple output circles at the top, with upward arrows from inputs to cells and from cells to outputs. A vertical black line separates the first diagram from the others.

- One to One: one blue circle labelled $x$, one green box, one purple circle labelled $\hat{y}$. Caption: "One to One", "“Vanilla” NN" and, in italics, "Binary classification".
- Many to One: three blue circles, three green boxes joined by left-to-right arrows, and only the last (third) box has an arrow up to a purple circle. Caption: "Many to One", italic "Sentiment Classification".
- One to Many: one blue circle feeding only the first of three green boxes (joined by left-to-right arrows); each box has an arrow up to a purple circle (three outputs). Caption: "One to Many", italic "Text Generation" and "Image Captioning".
- Many to Many: three blue circles, three green boxes joined by left-to-right arrows, three purple output circles. Caption: "Many to Many", italic "Translation & Forecasting" and "Music Generation".

Bottom: "… and many other architectures and applications". At bottom right a yellow star icon with bold "6.S191 Lab!".

*Figure: yes — four RNN input/output configurations: one-to-one, many-to-one, one-to-many, many-to-many*

## Slide 30 — Sequence Modeling: Design Criteria

To model sequences, we need to:

1. Handle **variable-length** sequences
2. Track **long-term** dependencies
3. Maintain information about **order**
4. **Share parameters** across the sequence

**Recurrent Neural Networks (RNNs)** meet these sequence modeling design criteria

Right: an unlabelled RNN diagram: blue circle at the bottom with an arrow up into a green box labelled "RNN"; a loop arrow leaves the right side of the box, runs over the top and re-enters the left side; an arrow from the box up to a purple circle.

*Figure: yes — RNN recurrent cell diagram (input circle, RNN box with feedback loop, output circle)*

## Slide 31 — A Sequence Modeling Problem: Predict the Next Word

[Section divider.] White centred title text on a plain blue background: "A Sequence Modeling Problem: Predict the Next Word". No other content.

*Figure: no*

## Slide 32 — A Sequence Modeling Problem: Predict the Next Word

Centred sentence: "This morning I took my cat for a walk."

Footer credit: "H. Suresh, 6.S191 2018."

*Figure: no*

## Slide 33 — A Sequence Modeling Problem: Predict the Next Word

Build step: adds highlighting and the label "given these words" to slide 32.

Centred sentence: "This morning I took my cat for a walk." The words "This morning I took my cat for a" are highlighted in light green and the final word "walk" in light orange. Below the green part, in green bold: "given these words".

Footer credit: "H. Suresh, 6.S191 2018."

*Figure: no*

## Slide 34 — A Sequence Modeling Problem: Predict the Next Word

Build step: adds the label "predict the next word" to slide 33.

Same sentence and highlighting as slide 33 ("This morning I took my cat for a" in green, "walk" in orange), with green bold "given these words" below the green part and, new, orange bold "predict the next word" (on two lines) below the word "walk".

Footer credit: "H. Suresh, 6.S191 2018."

*Figure: no*

## Slide 35 — A Sequence Modeling Problem: Predict the Next Word

Build step: adds the "Representing Language to a Neural Network" section to slide 34.

Same sentence, highlighting and the labels "given these words" (green) and "predict the next word" (orange) as slide 34, plus a heading "Representing Language to a Neural Network" and two small diagrams:

- Left: a large red X; then the word "deep" with an arrow (crossed out by a red X) into a green rounded box, and an arrow (also crossed out by a red X) from the box to the word "learning". Italic caption: "Neural networks cannot interpret words".
- Right: a large green check mark; a column vector [0.1, 0.8, 0.6] (printed as a column) with an arrow into a green rounded box, and an arrow from the box to a column vector [0.9, 0.2, 0.4] (printed as a column). Italic caption: "Neural networks require numerical inputs".

*Figure: yes — words crossed out as network input/output versus numerical vectors accepted as input/output*

## Slide 36 — Encoding Language for a Neural Network

![Slide 36 — Encoding Language for a Neural Network](../images/02-rnns-transformers-attention/slide-36.jpg)

Top: the same two diagrams as slide 35: red X, "deep" and "learning" with crossed-out arrows around a green box, italic caption "Neural networks cannot interpret words"; green check mark, vector [0.1, 0.8, 0.6] (printed as a column) into a green box into vector [0.9, 0.2, 0.4] (printed as a column), italic caption "Neural networks require numerical inputs".

Heading: "Embedding: transform indexes into a vector of fixed size."

Three rounded panels with numbered captions:

- Panel 1, caption "**1. Vocabulary:**" / "Corpus of words": the words "this", "cat", "for", "my", "took", "walk", "I", "a", "morning" scattered in the box.
- Panel 2, caption "**2. Indexing:**" / "Word to index": a list of arrows: "a" → 1; "cat" → 2; "…" → "…"; "walk" → N.
- Panel 3, caption "**3. Embedding:**" / "Index to fixed-sized vector": split by a dashed vertical line into two halves.
  - Left, "One-hot embedding": "“cat” = [ 0, 1, 0, 0, 0, 0 ]" with the 1 in blue and a blue arrow pointing up at it from the blue label "i-th index" ($i$-th index).
  - Right, "Learned embedding": a 2D plot with a horizontal double-headed arrow and a vertical double-headed arrow crossing, with words placed in the four quadrants: upper left "run" and "walk"; upper right "dog" and "cat"; lower left "day" and "sun"; lower right "happy" and "sad".

*Figure: yes — vocabulary, word-to-index table, one-hot vector example and a 2D learned-embedding plot of words*

## Slide 37 — Handle Variable Sequence Lengths

Three centred sentences separated by "vs.". In each, the last word is underlined and highlighted light orange and the preceding words are highlighted light green:

- "The food was great" (orange: "great")
- "vs."
- "We visited a restaurant for lunch" (orange: "lunch")
- "vs."
- "We were hungry but cleaned the house before eating" (orange: "eating")

*Figure: no*

## Slide 38 — Model Long-Term Dependencies

"**France** is where I grew up, but I now live in Boston. I speak fluent ___."

Centred in large bold italic text: "J’aime 6.S191!" flanked by clip-art hearts coloured blue, white and red (three on each side).

"We need information from **the distant past** to accurately predict the correct word."

Footer credit: "H. Suresh, 6.S191 2018."

*Figure: yes — blue, white and red hearts around the French phrase "J’aime 6.S191!"*

## Slide 39 — Capture Differences in Sequence Order

Two sentences separated by "vs.":

- "The food was good, not bad at all." with a black burger-and-drink icon at the left.
- "vs."
- "The food was bad, not good at all." with the same burger-and-drink icon inside a red circle with a diagonal slash (a "no" sign) at the right.

Footer credit: "H. Suresh, 6.S191 2018."

*Figure: yes — burger-and-drink icon beside the first sentence and the same icon in a red prohibition sign beside the second*

## Slide 40 — Sequence Modeling: Design Criteria

To model sequences, we need to:

1. Handle **variable-length** sequences
2. Track **long-term** dependencies
3. Maintain information about **order**
4. **Share parameters** across the sequence

**Recurrent Neural Networks (RNNs)** meet these sequence modeling design criteria

Right: the same unlabelled RNN diagram as slide 30 (blue circle, green box labelled "RNN" with feedback loop, purple circle).

*Figure: yes — RNN recurrent cell diagram (input circle, RNN box with feedback loop, output circle)*

## Slide 41 — Backpropagation Through Time (BPTT)

[Section divider.] White centred title text on a plain blue background: "Backpropagation Through Time (BPTT)". No other content.

*Figure: no*

## Slide 42 — Recall: Backpropagation in Feed Forward Models

![Slide 42 — Recall: Backpropagation in Feed Forward Models](../images/02-rnns-transformers-attention/slide-42.jpg)

Left: a fully connected feed-forward network drawn in three layers: a blue band at the bottom with three circles labelled $x$ (input); a green band in the middle with four circles; a purple band at the top with two circles labelled $y$ (output). Every circle in one layer is joined to every circle in the next by red double-headed (two-way) arrows. To the right of the network, a vertical black arrow pointing up and a vertical red arrow pointing down.

Right, text:

"Backpropagation algorithm:"

1. Take the derivative (gradient) of the loss with respect to each parameter
2. Shift parameters in order to minimize loss

*Figure: yes — three-layer feed-forward network with red bidirectional connections, black upward (forward) and red downward (backward) arrows*

## Slide 43 — RNNs: Backpropagation Through Time

Legend at top left: black arrow, "Forward pass".

Left: the folded RNN: blue circle $x_t$ at the bottom with arrow up into a green box labelled "RNN" with a loop arrow (right side, over the top, into the left side) and an arrow up to a purple circle $\hat{y}_ t$. Then an "=" sign and the unrolled network.

Unrolled network: four green boxes in a row, connected left to right by black arrows labelled $\boldsymbol{W}_ {hh}$ (between box 1 and 2, box 2 and 3, and a longer arrow from box 3 to box 4, with "…" implied between). Below each box, a blue input circle ($x_0$, $x_1$, $x_2$, then a "⋯" and $x_t$) with an upward arrow labelled $\boldsymbol{W}_ {xh}$. Above each box, an upward arrow labelled $\boldsymbol{W}_ {hy}$ to a purple circle ($\hat{y}_ 0$, $\hat{y}_ 1$, $\hat{y}_ 2$, then a "⋯" and $\hat{y}_ t$). Each purple circle has an upward arrow to a peach circle ($L_0$, $L_1$, $L_2$, and $L_3$ over the last one). Curved black arrows run from each of $L_0$, $L_1$, $L_2$, $L_3$ to a larger peach square labelled $L$ at the top right.

*Figure: yes — RNN unrolled through time with weights* $\boldsymbol{W}_ {xh}$, $\boldsymbol{W}_ {hh}$, $\boldsymbol{W}_ {hy}$, *per-step losses* $L_0$ *to* $L_3$ *and total loss* $L$, *forward pass only*

## Slide 44 — RNNs: Backpropagation Through Time

![Slide 44 — RNNs: Backpropagation Through Time](../images/02-rnns-transformers-attention/slide-44.jpg)

Build step: adds the backward pass (red arrows) to slide 43.

Same diagram as slide 43. Legend at top left: black arrow "Forward pass" and, new, red arrow "Backward pass". New red arrows run: from $L$ back to each of $L_0$, $L_1$, $L_2$, $L_3$ (alongside the black arrows); from each $L_i$ down to the corresponding $\hat{y}$ circle; from each $\hat{y}$ circle down into the corresponding green box; and leftwards between green boxes (from box 4 to box 3, 3 to 2, 2 to 1, running against the $\boldsymbol{W}_ {hh}$ arrows). A long red arrow along the bottom of the slide points left, from under the last input $x_t$ to under $x_0$.

Footer credit: "Mozer *Complex Systems* 1989."

*Figure: yes — the unrolled RNN with red backward-pass arrows flowing right to left through time*

## Slide 45 — Standard RNN Gradient Flow

A row of four green rounded boxes, left to right: the first labelled $h_0$, the second and third unlabelled, the last labelled $h_t$. Black arrows labelled $\boldsymbol{W}_ {hh}$ run left to right between consecutive boxes (the last, longer arrow from box 3 to box 4 stands for the omitted steps). Short red arrows run right to left along the top of each gap (box 4 to 3, 3 to 2, 2 to 1). Below each box a blue circle with an upward arrow labelled $\boldsymbol{W}_ {xh}$ into the box: $x_0$, $x_1$, $x_2$, then "⋯", then $x_t$.

*Figure: yes — unrolled RNN hidden-state chain* $h_0$ *to* $h_t$ *with black forward* $\boldsymbol{W}_ {hh}$ *arrows and red backward gradient arrows*

## Slide 46 — Standard RNN Gradient Flow

Build step: adds a sentence to slide 45.

Same diagram as slide 45, plus below it the line: "Computing the gradient wrt $h_0$ involves **many factors of $W_{hh}$ + repeated gradient computation**!" (bold from "many factors of" to "computation").

*Figure: yes — unrolled RNN hidden-state chain* $h_0$ *to* $h_t$ *with forward* $\boldsymbol{W}_ {hh}$ *and red backward arrows*

## Slide 47 — Standard RNN Gradient Flow: Exploding Gradients

Build step: adds the exploding-gradients box to slide 46.

Same diagram and sentence as slide 46 ("Computing the gradient wrt $h_0$ involves **many factors of $W_{hh}$ + repeated gradient computation**!"), plus a rounded-corner box at lower left reading:

"Many values > 1:" / "**exploding gradients**"

"**Gradient clipping** to scale big gradients"

*Figure: yes — unrolled RNN hidden-state chain with red backward gradient arrows, and a text box on exploding gradients*

## Slide 48 — Standard RNN Gradient Flow: Vanishing Gradients

![Slide 48 — Standard RNN Gradient Flow: Vanishing Gradients](../images/02-rnns-transformers-attention/slide-48.jpg)

Build step: adds the vanishing-gradients box to slide 47 and fades the exploding-gradients box.

Same diagram and sentence as slide 46. The lower-left "Many values > 1: exploding gradients / Gradient clipping to scale big gradients" box from slide 47 is now faded (greyed out). New, at lower right, a rounded-corner box:

"Many values < 1:" / "**vanishing gradients**"

1. Activation function
2. Weight initialization
3. Network architecture

*Figure: yes — unrolled RNN hidden-state chain with red backward gradient arrows, and text boxes on exploding and vanishing gradients*

## Slide 49 — The Problem of Long-Term Dependencies

Left column, a top-to-bottom chain joined by black down arrows:

"Why are vanishing gradients a problem?" (bold)

"Multiply many **small numbers** together"

↓

"Errors due to further back time steps have smaller and smaller gradients"

↓

"Bias parameters to capture short-term dependencies"

The right half of the slide is empty.

*Figure: no*

## Slide 50 — The Problem of Long-Term Dependencies

Build step: adds a quoted sentence to slide 49.

Same left column as slide 49. New, at upper right: "“The clouds are in the ___”"

*Figure: no*

## Slide 51 — The Problem of Long-Term Dependencies

Build step: adds an RNN diagram below the sentence on slide 50.

Same left column as slide 49 and the sentence "“The clouds are in the \_\_\_”" at upper right. New, below the sentence: an unrolled RNN with five green boxes joined by left-to-right black arrows; below each box a blue input circle $x_0$, $x_1$, $x_2$, $x_3$, $x_4$ with an upward arrow; above each box a purple output circle $\hat{y}_ 0$, $\hat{y}_ 1$, $\hat{y}_ 2$, $\hat{y}_ 3$, $\hat{y}_ 4$ with an upward arrow. The circles $x_0$, $x_1$ and $\hat{y}_ 3$ have a glowing teal outline (highlighted); the others do not.

*Figure: yes — five-step unrolled RNN with* $x_0$, $x_1$ *and* $\hat{y}_ 3$ *highlighted for the sentence "The clouds are in the ___"*

## Slide 52 — The Problem of Long-Term Dependencies

Build step: adds a second quoted sentence to slide 51.

Same as slide 51 (left column; "“The clouds are in the \_\_\_”"; five-step RNN with $x_0$, $x_1$, $\hat{y}_ 3$ highlighted), plus below the diagram: "“I grew up in France, … and I speak fluent\_\_\_ ”"

*Figure: yes — five-step unrolled RNN with* $x_0$, $x_1$ *and* $\hat{y}_ 3$ *highlighted*

## Slide 53 — The Problem of Long-Term Dependencies

![Slide 53 — The Problem of Long-Term Dependencies](../images/02-rnns-transformers-attention/slide-53.jpg)

Build step: adds a second RNN diagram below the second sentence on slide 52.

Same left column as slide 49 ("Why are vanishing gradients a problem?" / "Multiply many **small numbers** together" ↓ "Errors due to further back time steps have smaller and smaller gradients" ↓ "Bias parameters to capture short-term dependencies"), and the right-hand upper diagram of slide 52: "“The clouds are in the \_\_\_”" above a five-step RNN ($x_0$ to $x_4$ inputs, $\hat{y}_ 0$ to $\hat{y}_ 4$ outputs) with $x_0$, $x_1$ and $\hat{y}_ 3$ glowing teal; below it "“I grew up in France, … and I speak fluent\_\_\_ ”".

New, below that second sentence: another unrolled RNN with four green boxes joined by left-to-right black arrows; the arrow from box 2 to box 3 is long. Inputs below the boxes: $x_0$, $x_1$, then "⋯", then $x_t$, $x_{t+1}$. Outputs above the boxes: $\hat{y}_ 0$, $\hat{y}_ 1$, then "⋯", then $\hat{y}_ t$, $\hat{y}_ {t+1}$. The circles $x_0$, $x_1$ and $\hat{y}_ t$ glow red/orange; the others do not.

*Figure: yes — two unrolled RNNs; short-range dependency (teal highlights*, $x_0$ and $x_1$ *to* $\hat{y}_ 3$) *versus long-range dependency (red highlights*, $x_0$ and $x_1$ *to* $\hat{y}_ t$)

## Slide 54 — Gating Mechanisms in Neurons

![Slide 54 — Gating Mechanisms in Neurons](../images/02-rnns-transformers-attention/slide-54.jpg)

"Idea: use **gates** to selectively **add** or **remove** information within **each recurrent unit with**"

Left: a gate diagram. A horizontal black line with a red-pink circle containing a × at its middle, labelled in red at left "Pointwise multiplication". A vertical black line comes up from below through a pale-yellow rounded square containing a bold $\sigma$ (labelled in yellow at left "Sigmoid neural net layer") and an arrow up into the × circle.

Right: a large green rounded box labelled "gated cell" with the sub-label "LSTM, GRU, etc.". Below it: "Gates optionally let information through the cell".

Bottom: "**Long Short Term Memory (LSTMs)** networks rely on a gated cell to track information throughout many time steps."

*Figure: yes — gate diagram (sigmoid layer feeding a pointwise multiplication) beside a "gated cell" box*

## Slide 55 — RNN Applications & Limitations

[Section divider.] White centred title text on a plain blue background: "RNN Applications & Limitations". No other content.

*Figure: no*

## Slide 56 — Example Task: Music Generation

![Slide 56 — Example Task: Music Generation](../images/02-rnns-transformers-attention/slide-56.jpg)

Left: an unrolled RNN with four green boxes joined by left-to-right black arrows; a blue input circle under each and a purple output circle above each, with upward arrows. Input labels below the blue circles: E, F#, G, C. Output labels above the purple circles: F#, G, C, A. Thin grey curved arrows run from each of the first three purple output circles down to the next step's blue input circle (F# output to F# input, G to G, C to C).

Right, text: "**Input:** sheet music" and "**Output:** next character in sheet music". Below, an orange-yellow video thumbnail with a red circular play button, the text "Listening to 3rd movement" (partly covered by the button) and a blue illustration of a human head profile made of connected dots. At bottom right, a yellow star icon with bold "6.S191 Lab!".

Footer credit: "Huawei."

*Figure: yes — music-generation RNN feeding each predicted note back as the next input, plus a "Listening to 3rd movement" video thumbnail*

## Slide 57 — Example Task: Sentiment Classification

![Slide 57 — Example Task: Sentiment Classification](../images/02-rnns-transformers-attention/slide-57.jpg)

Diagram on the left: a many-to-one RNN. Four blue input circles at the bottom, labelled "I", "love", "this", "class!", each with an upward arrow into a green rounded box (the recurrent cell). The four green boxes are chained left to right by horizontal arrows. Only the last (rightmost) green box has an upward arrow, to a single purple output circle labelled above it "sentiment" / "<positive>".

Right side: "**Input:** sequence of words" and "**Output:** probability of having positive sentiment". Below, a dark code-style bar with the TensorFlow logo:

```python
loss = tf.nn.softmax_cross_entropy_with_logits(y, predicted)
```

Citation beside the footer: "Socher+, EMNLP 2013."

*Figure: yes — many-to-one RNN reading "I love this class!" and outputting sentiment <positive>*

## Slide 58 — Example Task: Sentiment Classification

Same RNN diagram as slide 57 (inputs "I", "love", "this", "class!"; single purple output "sentiment <positive>" from the last cell).

Right side, bold heading "Tweet sentiment classification", then two tweet screenshots:
- Top: tweet by Ivar Hagendoorn (@IvarHagendoorn), with a "Follow" button partly hidden behind a large smiling emoji. Text: "The @MIT Introduction to #DeepLearning is definitely one of the best courses of its kind currently available online introtodeeplearning.com". Timestamp "12:45 PM - 12 Feb 2018".
- Bottom: tweet by Angels-Cave (@AngelsCave), "Replying to @Kazuki2048", with a "Follow" button partly hidden behind a sad crying emoji. Text: "I wouldn't mind a bit of snow right now. We haven't had any in my bit of the Midlands this winter! :(". Timestamp "2:19 AM - 25 Jan 2019".

Citation beside the footer: "H. Suresh, 6.S191 2018."

*Figure: yes — RNN diagram plus two example tweets, one positive (smiling emoji) and one negative (crying emoji)*

## Slide 59 — Limitations of Recurrent Models

Same RNN diagram as slide 57 on the left (inputs "I", "love", "this", "class!"; output "sentiment <positive>").

Right side: underlined heading "Limitations of RNNs", then three items each with an icon:
- (funnel icon) "Encoding bottleneck"
- (clock icon) "Slow, no parallelization"
- (brain emoji) "Not long memory"

*Figure: yes — many-to-one RNN diagram beside icons for the three limitations*

## Slide 60 — Goal of Sequence Modeling

Subtitle: "RNNs: recurrence to model sequence dependencies".

Diagram in three rows with left-hand row labels and right-hand type labels. Bottom row: blue boxes $x_0, x_1, x_2, \ldots, x_{t-2}, x_{t-1}, x_t$ (a gap between $x_2$ and $x_{t-2}$), left label "Sequence of inputs", right label "input". Middle row: yellow three-cell stacked vectors above each input, left label "Sequence of features", right label "feature vector"; horizontal arrows link each vector to the next, with "···" between the third and fourth. Top row: purple boxes $\hat{y}_ 0, \hat{y}_ 1, \hat{y}_ 2, \ldots, \hat{y}_ {t-2}, \hat{y}_ {t-1}, \hat{y}_ t$, left label "Sequence of outputs", right label "output". Each input has an arrow up into its feature vector, and each feature vector an arrow up into its output. Large upward arrows on the left run from "Sequence of inputs" to "Sequence of features" to "Sequence of outputs". A long horizontal arrow along the bottom is labelled $t$.

*Figure: yes — unrolled RNN over time showing inputs, feature vectors and outputs*

## Slide 61 — Goal of Sequence Modeling

![Slide 61 — Goal of Sequence Modeling](../images/02-rnns-transformers-attention/slide-61.jpg)

Build step: adds the "Limitations of RNNs" list on the left of slide 60.

Subtitle: "RNNs: recurrence to model sequence dependencies". The unrolled RNN diagram is the same as slide 60 (inputs $x_0, x_1, x_2, \ldots, x_{t-2}, x_{t-1}, x_t$ in blue; yellow three-cell feature vectors linked left to right by arrows with "···" in the middle; outputs $\hat{y}_ 0, \hat{y}_ 1, \hat{y}_ 2, \ldots, \hat{y}_ {t-2}, \hat{y}_ {t-1}, \hat{y}_ t$ in purple; right labels "output", "feature vector", "input"; time arrow $t$ along the bottom). The row labels "Sequence of ..." and the left arrows are replaced by the following. Left column: underlined heading "Limitations of RNNs" and three items with icons: (funnel) "Encoding bottleneck", (clock) "Slow, no parallelization", (brain) "Not long memory".

*Figure: yes — unrolled RNN diagram beside the three RNN limitations*

## Slide 62 — Goal of Sequence Modeling

Build step: changes the left list of slide 61 from limitations to desired capabilities and adds a question above the diagram.

Question above the diagram (bold): "Can we eliminate the need for recurrence entirely?" The unrolled RNN diagram is the same as slide 61 (inputs $x_0 \ldots x_t$, feature vectors, outputs $\hat{y}_ 0 \ldots \hat{y}_ t$, labels "output", "feature vector", "input", time arrow $t$). Left column: underlined heading "Desired Capabilities" and three items with icons: (blue stream icon) "Continuous stream", (fork-arrow icon) "Parallelization", (brain) "Long memory".

*Figure: yes — unrolled RNN diagram beside the three desired capabilities*

## Slide 63 — Goal of Sequence Modeling

Build step: replaces the recurrent diagram of slide 62 with one in which the whole sequence is processed as a single block, and adds an $x_0$ icon to the left list.

Question above the diagram: "Can we eliminate the need for recurrence entirely?" Left column: underlined heading "Desired Capabilities" and the items (blue stream icon) "Continuous stream", (fork-arrow icon) "Parallelization", and "Long memory", the last now preceded by a small blue square containing $x_0$ instead of the brain icon.

Diagram: a single wide purple bar holding $\hat{y}_ 0, \hat{y}_ 1, \hat{y}_ 2$, a gap, then $\hat{y}_ {t-2}, \hat{y}_ {t-1}, \hat{y}_ t$ (label "output"); a single wide yellow three-row grid of feature cells with "···" in the middle (label "feature vector"); a single wide blue bar holding $x_0, x_1, x_2$, a gap, then $x_{t-2}, x_{t-1}, x_t$ (label "input"). The gaps in the two bars are empty; only the yellow grid prints "···". One arrow goes up from the input bar to the feature grid and one from the grid to the output bar; there are no arrows between positions. Time arrow $t$ along the bottom.

*Figure: yes — all inputs, features and outputs drawn as single wide blocks with no recurrence*

## Slide 64 — Goal of Sequence Modeling

![Slide 64 — Goal of Sequence Modeling](../images/02-rnns-transformers-attention/slide-64.jpg)

Build step: replaces the left list of slide 63 with an evaluation of Idea 1.

Question above the diagram: "Can we eliminate the need for recurrence entirely?" The diagram is the same as slide 63 (wide blue input bar $x_0 \ldots x_t$, wide yellow feature grid, wide purple output bar $\hat{y}_ 0 \ldots \hat{y}_ t$, labels "output", "feature vector", "input", time arrow absent in this slide).

Left column: underlined heading "Idea 1: Feed everything into dense network", then four items: a green check mark "No recurrence" (green text), a red cross "Not scalable", a red cross "No order", a red cross "No long memory". At the bottom left, a brain emoji and the text "Idea: Identify and attend to what's important".

*Figure: yes — wide-block sequence diagram beside check/cross evaluation of the dense-network idea*

## Slide 65 — [Section title: Attention Is All You Need]

Blue full-slide background with white centred text: "Attention Is All You Need".

*Figure: no*

## Slide 66 — Intuition Behind Self-Attention

![Slide 66 — Intuition Behind Self-Attention](../images/02-rnns-transformers-attention/slide-66.jpg)

Subtitle: "Attending to the most important parts of an input."

Image: a photo of the Iron Man character (red and gold armour, glowing blue eyes) flying toward the viewer, with six horizontal white arrows overlaid, alternating direction (right, left, right, left, right, left), like a raster scan across the image.

Below the image, a numbered list: "1. Identify which parts to attend to" (enclosed in a blue rounded box) and "2. Extract the features with high attention". A blue arrow points from the blue-coloured note "Similar to a search problem!" at the right to the boxed item 1.

*Figure: yes — photo of Iron Man overlaid with scan-line arrows, illustrating attending to parts of an input*

## Slide 67 — A Simple Example: Search

A thought-bubble cloud from a thinking-face emoji contains the text "How can I learn more about neural networks?". To the right is a curved wall of many small colourful thumbnail images (video-like tiles: animals, landscapes, balloons, billiard balls, etc.), blurred in the distance, representing a large collection to search.

*Figure: yes — thinking emoji with the query "How can I learn more about neural networks?" facing a wall of thumbnails*

## Slide 68 — Understanding Attention with Search

![Slide 68 — Understanding Attention with Search](../images/02-rnns-transformers-attention/slide-68.jpg)

Dark (black) slide with white title. A screenshot of a YouTube search page: the YouTube logo, a search box containing "deep learning" outlined in blue, with an X and a magnifier button. To the right of the search box, in blue: "Query (Q)".

Three video results are listed vertically; the top and bottom are dimmed, the middle is highlighted:
- Top (dimmed): a sea turtle thumbnail, title "GIANT SEA TURTLES • AMAZING CORAL REEF FISH • 12 HOURS of THE BEST RELAX MUSIC", with a faint orange label "Key (K₁)" at the right.
- Middle (highlighted, title boxed in orange): thumbnail of a man in a blue sweater holding a clicker in front of an MIT-branded red network graphic, duration "52:52". Title "MIT 6.S191 (2020): Introduction to Deep Learning", "1M views • 1 year ago", channel "Alexander Amini", description "MIT Introduction to Deep Learning 6.S191: Lecture 1 Foundations of Deep Learning Lecturer: Amini January 2020 For ...", a "CC" badge. Orange label at right: "Key (K₂)".
- Bottom (dimmed): a basketball thumbnail, title "The Kobe Bryant Fadeaway Shot", with a faint orange label "Key (K₃)".

On the right, white square brackets: a short bracket spanning the Query and Key (K₁) rows, a longer one reaching down to Key (K₂), and a longest one reaching down to Key (K₃), each paired with the query; the text "How similar is the key to the query?" sits beside the top bracket.

Bottom right: "1. **Compute attention mask:** how similar is each key to the desired query?" (bold "Compute attention mask:").

*Figure: yes — YouTube search for "deep learning" showing query Q and keys K1, K2, K3 with similarity brackets*

## Slide 69 — Understanding Attention with Search

![Slide 69 — Understanding Attention with Search](../images/02-rnns-transformers-attention/slide-69.jpg)

Build step: adds the Value (V) highlight and step 2 to slide 68.

Same dark YouTube screenshot as slide 68: search box "deep learning" outlined in blue with "Query (Q)" at right; three results with orange labels "Key (K₁)" (sea turtles, dimmed), "Key (K₂)" (the "MIT 6.S191 (2020): Introduction to Deep Learning" result, title boxed in orange) and "Key (K₃)" (Kobe Bryant video, dimmed). The brackets and "How similar is the key to the query?" text of slide 68 are gone. New: a large purple rounded rectangle surrounds the whole middle result (thumbnail plus text), with the purple label "Value (V)" at its right.

Bottom right: "2. **Extract values based on attention:** Return the values highest attention" (bold "Extract values based on attention:"; the phrase "highest attention" is printed without "with").

*Figure: yes — YouTube search with the middle result enclosed in a purple box labelled Value (V)*

## Slide 70 — Learning Self-Attention with Neural Networks

Left: "Goal: identify and attend to most important features in input." Then a numbered list in which item 1 is in full black and items 2 to 4 are greyed out:
1. Encode **position** information
2. Extract **query, key, value** for search
3. Compute **attention weighting**
4. Extract **features with high attention**

Right: a wide light-blue bar labelled $x$, and below it the words of the sentence, spaced across the bar: "He", "tossed", "the", "tennis", "ball", "to", "serve".

Bottom, centred: "Data is fed in all at once! Need to encode position information to understand order."

*Figure: yes — input bar* $x$ *above the tokens of "He tossed the tennis ball to serve"*

## Slide 71 — Learning Self-Attention with Neural Networks

![Slide 71 — Learning Self-Attention with Neural Networks](../images/02-rnns-transformers-attention/slide-71.jpg)

Build step: adds the embedding, position information and position-aware encoding diagram to slide 70.

Left side and bottom text are as in slide 70 (goal sentence; list with item 1 "Encode **position** information" highlighted and items 2 to 4 greyed; bottom line "Data is fed in all at once! Need to encode position information to understand order.").

Right diagram, top to bottom: the blue bar $x$ with tokens "He", "tossed", "the", "tennis", "ball", "to", "serve" beneath it; a row of seven blue three-cell vectors, one under each token, labelled "embedding" at left; below a "⊕" symbol drawn under the "tennis" column; a row labelled "position information" at left with $p_0, p_1, p_2, p_3, p_4, p_5, p_6$ under the seven columns; an arrow down from $p_3$ into a row of seven green three-cell vectors; caption beneath the green row: "Position-aware encoding".

*Figure: yes — token embeddings combined with position information* $p_0 \ldots p_6$ *to give position-aware encodings*

## Slide 72 — Learning Self-Attention with Neural Networks

![Slide 72 — Learning Self-Attention with Neural Networks](../images/02-rnns-transformers-attention/slide-72.jpg)

Citation beside the footer: "Vaswani+, NeurIPS 2017."

Left: "Goal: identify and attend to most important features in input." and the list, now with item 2 highlighted and items 1 and 2 in black, items 3 and 4 greyed:
1. Encode **position** information
2. Extract **query, key, value** for search
3. Compute **attention weighting** (greyed)
4. Extract **features with high attention** (greyed)

Right: three rows of matrix multiplications, each of the form (green grid) × (small grid) = (larger grid):
- Row 1: green grid labelled "Positional embedding" × a small blue grid labelled "Linear layer" = a blue grid labelled "Output"; bold blue label at right "Q" / "Query".
- Row 2: green grid "Positional embedding" × a small orange grid "Linear layer" = an orange grid "Output"; bold orange label "K" / "Key".
- Row 3: green grid "Positional embedding" × a small purple grid "Linear layer" = a purple grid "Output"; bold purple label "V" / "Value".

The green grids are tall (about 7 rows by 3 columns); the linear-layer grids are small (about 3 rows by 4 columns); the output grids are tall (about 7 rows by 4 columns).

*Figure: yes — three matrix products of positional embedding with linear layers producing Q, K and V*

## Slide 73 — Learning Self-Attention with Neural Networks

![Slide 73 — Learning Self-Attention with Neural Networks](../images/02-rnns-transformers-attention/slide-73.jpg)

Left: "Goal: identify and attend to most important features in input." and the list with items 1 to 3 in black and item 4 greyed:
1. Encode **position** information
2. Extract **query, key, value** for search
3. Compute **attention weighting**
4. Extract **features with high attention** (greyed)

Right: heading "**Attention score**: compute pairwise similarity between each **query** and **key**" (the word "query" in blue, "key" in orange). Below: "How to compute similarity between two sets of features?"

Diagram: from a common origin point (black dot), two arrows fan out upward: a blue arrow labelled "Q" (steeper, pointing up and slightly right) and an orange arrow labelled "K" (pointing up-right at about 45 degrees). To the right, a thick black arrow labelled "Dot product" above and "Scale" below points to a red dashed box containing the fraction

$$\frac{Q \cdot K^T}{\text{scaling}}$$

(Q in blue, K^T in orange), captioned in red "Similarity metric". Below, small text: "Also known as the "cosine similarity"".

*Figure: yes — two vectors Q and K from a common origin leading to the scaled dot-product similarity metric*

## Slide 74 — Learning Self-Attention with Neural Networks

![Slide 74 — Learning Self-Attention with Neural Networks](../images/02-rnns-transformers-attention/slide-74.jpg)

Build step: replaces the two arrows of slide 73 with matrices Q and K^T.

Left column, heading and list as in slide 73 (items 1 to 3 in black, item 4 greyed). Right: same heading "**Attention score**: compute pairwise similarity between each **query** and **key**" and question "How to compute similarity between two sets of features?"

Diagram: a blue grid labelled "Q" above and "Query" below, a black dot (dot-product sign), an orange grid labelled "K^T" above and "Key" below; the Q grid is taller than wide (about 7 rows by 4 columns) and the K^T grid is wider than tall (about 4 rows by 6 columns). Then, as in slide 73, a thick arrow labelled "Dot product" / "Scale" to the red dashed box with $\frac{Q \cdot K^T}{\text{scaling}}$ and the red caption "Similarity metric". Below, small text: "Also known as the "cosine similarity"".

*Figure: yes — query and key matrices combined by dot product and scaling into a similarity metric*

## Slide 75 — Learning Self-Attention with Neural Networks

![Slide 75 — Learning Self-Attention with Neural Networks](../images/02-rnns-transformers-attention/slide-75.jpg)

Citation beside the footer: "Vaswani+, NeurIPS 2017."

Left: "Goal: identify and attend to most important features in input." and the list as in slide 74 (items 1 to 3 in black, item 4 greyed).

Right: heading "Attention weighting: where to attend to! How similar is the key to the query?"

Attention map (heat map): a 7 by 7 grid in shades of pink to dark red. Both the row labels (left) and the column labels (top, rotated) are the tokens "He", "tossed", "the", "tennis", "ball", "to", "serve". The diagonal cells are the darkest red. Off-diagonal cells are mostly very pale pink; the stronger ones (medium red) are: row "tossed", column "ball"; row "tennis", columns "ball" and "serve"; row "ball", columns "tossed" and "tennis"; row "serve", column "tennis". Light pink cells: row "He", column "tossed"; row "tossed", column "He" and column "serve"; row "serve", column "tossed". Rows "the" and "to" have only the diagonal cell shaded.

Right of the map, the equation

$$\text{softmax}\left(\frac{Q \cdot K^T}{\text{scaling}}\right)$$

with a red underline and the red label "Attention weighting".

*Figure: yes — 7x7 attention-weight heat map over "He tossed the tennis ball to serve", with the softmax equation*

## Slide 76 — Learning Self-Attention with Neural Networks

![Slide 76 — Learning Self-Attention with Neural Networks](../images/02-rnns-transformers-attention/slide-76.jpg)

Citation beside the footer: "Vaswani+, NeurIPS 2017."

Left: "Goal: identify and attend to most important features in input." and the list with all four items in black:
1. Encode **position** information
2. Extract **query, key, value** for search
3. Compute **attention weighting**
4. Extract **features with high attention**

Right: heading "Last step: self-attend to extract features".

Diagram: the 7 by 7 attention heat map (same pattern as slide 75, tokens not labelled here), labelled in red "Attention weighting", times ("×") a purple grid labelled "V" above and "Value" below (about 7 rows by 4 columns), equals ("=") a grey grid labelled "Output" (about 7 rows by 4 columns).

Below, the equation

$$\text{softmax}\left(\frac{Q \cdot K^T}{\text{scaling}}\right) \cdot V = A(Q, K, V)$$

with a red underline beneath the softmax term, a purple underline beneath $V$, and a grey underline beneath $A(Q, K, V)$.

*Figure: yes — attention-weighting matrix times Value matrix gives the output, with the attention equation*

## Slide 77 — Learning Self-Attention with Neural Networks

![Slide 77 — Learning Self-Attention with Neural Networks](../images/02-rnns-transformers-attention/slide-77.jpg)

Citation beside the footer: "Vaswani+, NeurIPS 2017."

Left: "Goal: identify and attend to most important features in input." and the list with all four items in black:
1. Encode **position** information
2. Extract **query, key, value** for search
3. Compute **attention weighting**
4. Extract **features with high attention**

Below the list, in a red rounded box: "These operations form a self-attention head that can plug into a larger network. Each head attends to a different part of input."

Right: a block diagram inside a rounded grey frame, flowing upward. At the bottom, the green label "Positional Encoding" and three green grids (one under each Linear box). Each grid feeds an upward arrow into a "Linear" box: blue "Linear" labelled "Query", orange "Linear" labelled "Key", purple "Linear" labelled "Value". The Query and Key outputs both feed a grey "MatMul" box, then upward through grey boxes "Scale", "Softmax", and a wide grey "Matmul" box at the top. The Value output goes by a long arrow directly up into the top "Matmul". An arrow leaves the top of "Matmul" out of the frame.

Below the frame, the equation

$$\text{softmax}\left(\frac{Q \cdot K^T}{\text{scaling}}\right) \cdot V$$

with red boxes: one around the whole softmax term plus $\cdot V$, and an inner one around $\frac{Q \cdot K^T}{\text{scaling}}$ (with a further small box on $Q \cdot K^T$).

*Figure: yes — self-attention head block diagram (Positional Encoding, Linear Q/K/V, MatMul, Scale, Softmax, Matmul) with the equation*

## Slide 78 — Learning Self-Attention with Neural Networks

Citation beside the footer: "Vaswani+, NeurIPS 2017."

Build step: replaces the red note and the equation of slide 77 with a closing line.

Left: "Goal: identify and attend to most important features in input." and the list of four items, all in black, as in slide 77. Right: the same self-attention head block diagram as slide 77 (Positional Encoding; Linear boxes for Query, Key, Value; MatMul, Scale, Softmax, Matmul).

Bottom, centred: "Attention is the foundational building block of the **Transformer** architecture." ("Transformer" bold and underlined.)

*Figure: yes — self-attention head block diagram (Positional Encoding, Linear Q/K/V, MatMul, Scale, Softmax, Matmul)*

## Slide 79 — Applying Multiple Self-Attention Heads

![Slide 79 — Applying Multiple Self-Attention Heads](../images/02-rnns-transformers-attention/slide-79.jpg)

Six image panels in two rows, all built from the Iron Man photo of slide 66. Top row, with an "×" between the first two and "=" between the last two:
- "Attention weighting": a grey image with a white blob in the shape of the Iron Man figure's head and body on the left side (white = attended region).
- "Value": the full-colour Iron Man photo (red and gold armour, with a building on the right edge).
- "Output": Iron Man figure shown in full colour with the background washed to grey.

Bottom row:
- "Output of attention head 1": the Iron Man figure in colour on a grey background.
- "Output of attention head 2": mostly faint grey, with a building facade visible in colour along the right side.
- "Output of attention head 3": almost entirely faint grey, with a small piece of red-and-gold debris visible near the top right.

*Figure: yes — attention weighting times Value gives Output on the Iron Man image, and the outputs of three different attention heads*

## Slide 80 — Self-Attention Applied

![Slide 80 — Self-Attention Applied](../images/02-rnns-transformers-attention/slide-80.jpg)

Three columns, each with a heading, an image, a caption line, and citations.
- "Language Processing": an image of an avocado-shaped armchair (green outside, yellow cushion), caption "An armchair in the shape of an avocado". Below: "Transformers: BERT, GPT"; citations "Devlin et al., *NAACL* 2019" and "Brown et al., *NeurIPS* 2020". A star icon with bold "6.S191 Lab and Lectures!" sits at the bottom left.
- "Biological Sequences": a ribbon rendering of a protein structure, two overlaid structures in blue and green. Below: "Protein Structure Models"; citations "Jumper et al., *Nature* 2021" and "Lin et al., *Science* 2023".
- "Computer Vision": a photo of a golden retriever puppy sitting in grass with orange flowers, overlaid by a white grid dividing the image into square patches. Below: "Vision Transformers"; citation "Dosovitskiy et al., *ICLR* 2020".

*Figure: yes — avocado armchair, protein structure and patch-gridded puppy photo as examples of self-attention in language, biology and vision*

## Slide 81 — Deep Learning for Sequence Modeling: Summary

A numbered list:
1. RNNs are well suited for **sequence modeling** tasks
2. Model sequences via a **recurrence relation**
3. Training RNNs with **backpropagation through time**
4. Models for **music generation**, classification, machine translation, and more
5. Self-attention to model **sequences without recurrence**
6. Self-attention is the basis for many **large language models** – stay tuned!

A multicolour audio-waveform graphic (rainbow gradient from red/pink on the left through blue, green and yellow to orange on the right) runs along the bottom.

*Figure: no*

## Slide 82 — 6.S191: Introduction to Deep Learning

Black slide with white text and a rainbow audio-waveform graphic along the bottom.

"Lab 1: Deep Learning in Python and Music Generation with RNNs"

"Link to download labs:
http://introtodeeplearning.com#schedule"

1. Open the lab in Google Colab
2. Start executing code blocks and filling in the #TODOs
3. Need help? Find a TA/instructor!

*Figure: no*

## Slide 83 — 6.S191: Introduction to Deep Learning

Black slide with white text and a rainbow audio-waveform graphic along the bottom.

Bold: "Kickoff Reception at One Kendall Square!"

Bold with red link: "Register here: luma.com/47iswo1i"

"Join us at 5:00pm for a special kickoff reception at 1 Kendall Square!"

"Food and drinks will be provided!
Special thanks to John Werner and Link Ventures for hosting."

*Figure: no*
