# Convolutional neural networks

A convolutional neural network (CNN) is a neural network built around the **convolution**: a small
filter of learned weights slid across an image, which responds wherever the image contains the pattern
the filter encodes. Stacking convolutions, non-linearities and pooling lets a network learn its own
visual features, from edges up to whole objects, without flattening away the image's spatial
structure. This page follows MIT 6.S191 [lecture 3](03-convolutional-neural-networks.md), sections 4–16
(≈11:39–43:15). For the tasks CNNs are used for, see [computer vision](computer-vision.md).

## Why not a fully connected network?

A fully connected network ([neural network layers](neural-network-layers.md)) takes a one-dimensional
input, so an image has to be **flattened** first. That throws away all of the image's spatial
information before training starts, and it costs a great many parameters: a 100 by 100 pixel image
becomes a 10,000-dimensional input, so the first weight matrix is already 10,000 by some other big
number (lecture 3, slides 20–22, ≈12:24–13:57). The CNN's answer is to keep the image two-dimensional
and connect each neuron of the next layer to **only a patch** of input pixels, sliding the patch across
the image so that every neuron sees one local region (slides 23–24, ≈13:57–15:30).

## The convolution

Sliding a patch of weights across the image is a convolution (≈16:17). In lecture 3's first example a
$4 \times 4$ filter has 16 weights, the same filter is applied to every $4 \times 4$ patch of the input, and each next
patch is 2 pixels over (slide 25). At each position the filter does what a neuron does: multiply its
weights element-wise with the pixels under it, add them up with a bias, and apply a non-linearity. Slide
25 states the three ideas:

1. Apply a set of weights — a filter — to extract **local features**.
2. Use **multiple filters** to extract different features.
3. **Spatially share** parameters of each filter.

For a $4 \times 4$ filter with weights $w_{ij}$, the neuron at position $(p, q)$ of the hidden layer, with input
pixels $x$ and bias $b$, computes (slide 46)

$$\sum_{i=1}^{4} \sum_{j=1}^{4} w_{ij} \thinspace x_{i+p, \thinspace j+q} + b$$

A filter is "nothing more than just a miniature image" (≈20:08). In lecture 3's case study, an X is
recognized not by comparing whole images pixel by pixel — a shifted or deformed X differs everywhere —
but by finding the same small features in both: two diagonals and a crossing, each detected by a $3 \times 3$
filter of +1 and −1 values (slides 27–29, ≈18:35–20:54).

### Worked example

Slides 31–40 convolve a $5 \times 5$ binary image with a $3 \times 3$ filter, one pixel at a time (the slides write the
operation as a circled cross):

$$\begin{bmatrix} 1 & 1 & 1 & 0 & 0 \cr 0 & 1 & 1 & 1 & 0 \cr 0 & 0 & 1 & 1 & 1 \cr 0 & 0 & 1 & 1 & 0 \cr 0 & 1 & 1 & 0 & 0 \end{bmatrix} \otimes \begin{bmatrix} 1 & 0 & 1 \cr 0 & 1 & 0 \cr 1 & 0 & 1 \end{bmatrix} = \begin{bmatrix} 4 & 3 & 4 \cr 2 & 4 & 3 \cr 2 & 3 & 4 \end{bmatrix}$$

The first output comes from the top-left $3 \times 3$ patch: its element-wise product with the filter sums to
$1 + 1 + 1 + 1 = 4$, from the four positions where both the pixel and the weight are 1 (slide 32,
≈23:12). The output image is the **feature map**: it shows where the filter's feature appears in the
input, with very positive values marking strong matches (≈23:57).

![Slide 40: The Convolution Operation](../raw/images/03-convolutional-neural-networks/slide-40.jpg)

*Lecture 3, slide 40 — the filter at its last position and the completed feature map.*

### Hand-written filters versus learned ones

Before CNNs, people wrote filter weights by hand to create effects and detect features (≈27:47). Slide
41 shows three: a sharpening filter, an edge detector and a "strong" edge detector, each producing a
different feature map from the same photograph.

$$\begin{bmatrix} 0 & -1 & 0 \cr -1 & 5 & -1 \cr 0 & -1 & 0 \end{bmatrix} \qquad \begin{bmatrix} 0 & 1 & 0 \cr 1 & -4 & 1 \cr 0 & 1 & 0 \end{bmatrix} \qquad \begin{bmatrix} -1 & -2 & -1 \cr 0 & 0 & 0 \cr 1 & 2 & 1 \end{bmatrix}$$

In a CNN the weights are not written down: they are learned "like the weights of any part of a neural
network" (≈24:44). Training a CNN means learning the numbers in every filter of every convolutional
layer (slide 44, ≈30:52).

![Slide 41: Producing Feature Maps](../raw/images/03-convolutional-neural-networks/slide-41.jpg)

*Lecture 3, slide 41 — one image through a sharpening filter, an edge detector and a "strong" edge detector.*

## A convolutional layer: depth, stride, receptive field

A layer has many filters, one per feature it looks for, and each produces its own feature map, so the
layer's output is a **volume** in which every slice is one feature map (slide 47, ≈32:26–33:12). Its
dimensions are $h \times w \times d$: $h$ and $w$ are spatial, and the depth $d$ is the number of
filters. The **stride** is the filter's step size, and a neuron's **receptive field** is the set of
input locations it is connected to. Whether successive filter positions overlap is a design choice;
overlap often helps, because a feature can be cut off at the edge of one position (≈24:44–25:30).

```python
tf.keras.layers.Conv2D( filters=d, kernel_size=(h,w), strides=s )
torch.nn.Conv2d( in_channels=3, out_channels=d, kernel_size=(h,w), stride=s )
```

PyTorch needs the number of input channels, here 3 for an RGB image (slide 47).

![Slide 47: CNNs: Spatial Arrangement of Output Volume](../raw/images/03-convolutional-neural-networks/slide-47.jpg)

*Lecture 3, slide 47 — a 32 by 32 by 3 input and the output volume, with height, width and depth labelled.*

## The three operations of a CNN

A CNN repeats three operations (slide 44, ≈30:06):

1. **Convolution**, "the main workhorse": apply filters to generate feature maps.
2. **Non-linearity**, usually ReLU, $g(z) = \max(0, z)$, applied after every convolution. It works pixel
   by pixel, setting negative values to zero and passing positive ones unchanged, like a threshold at
   zero (slide 48, ≈33:12–33:58). See [activation functions](activation-functions.md).
3. **Pooling**: downsampling each feature map. **Max pooling** keeps the largest value in each patch;
   with $2 \times 2$ filters and stride 2, a $4 \times 4$ map becomes $2 \times 2$ (slide 49, ≈34:44–35:29). Pooling reduces only
   height and width, never depth: 32 feature maps in, 32 out (≈43:15).

Pooling is what gives the network its sense of scale. Early filters are tiny next to the image, so they
find only small features. Each pooling step shrinks the image, which raises the filter's relative size,
so deeper layers detect larger, higher-level features (≈25:30–26:16, ≈30:52). Making the patches bigger
instead would defeat the point of looking locally: small patches catch fine detail, and pooling combines
the results into higher-level compositions (≈35:29–36:15). Slide 49 leaves the question open: "How else
can we downsample and preserve spatial invariance?"

![Slide 49: Pooling](../raw/images/03-convolutional-neural-networks/slide-49.jpg)

*Lecture 3, slide 49 — 2 by 2 max pooling with stride 2.*

## The learned hierarchy

Stacked, these layers learn a hierarchy of features: lines and edges in the first layers, then corners
and curves, then shapes and objects (≈37:49). Slide 50 shows features learned at three convolutional
layers on faces: edges and dark spots, then eyes, ears and noses, then whole facial structure (Lee+
*ICML* 2009). This is the "hierarchy of features" that [what is deep learning?](what-is-deep-learning.md)
describes in general.

![Slide 50: Representation Learning in Deep CNNs](../raw/images/03-convolutional-neural-networks/slide-50.jpg)

*Lecture 3, slide 50 — low-, mid- and high-level features from convolutional layers 1, 2 and 3.*

## A CNN for classification

A classification CNN has two parts (slides 51–52, ≈37:49–38:35). The **feature-learning** part is
convolution, ReLU and pooling, repeated. The **classification** part flattens the high-level features,
passes them through fully connected layers, and outputs class probabilities with a softmax,

$$\text{softmax}(y_i) = \frac{e^{y_i}}{\sum_j e^{y_j}}$$

where $y_i$ is the output for class $i$. It is trained with a classification loss, as on day one (see
[loss functions](loss-functions.md)).

![Slide 51: CNNs for Classification: Feature Learning](../raw/images/03-convolutional-neural-networks/slide-51.jpg)

*Lecture 3, slide 51 — convolution + ReLU and pooling (feature learning), then flatten, fully connected and softmax (classification).*

Slide 53's TensorFlow version, as printed, uses two convolution-and-pooling blocks (32 filters, then 64,
each $3 \times 3$) and a dense head of 1024 units and 10 outputs:

```python
tf.keras.layers.Conv2D(32, filter_size=3, activation='relu’),
tf.keras.layers.MaxPool2D(pool_size=2, strides=2),
tf.keras.layers.Conv2D(64, filter_size=3, activation='relu’),
tf.keras.layers.MaxPool2D(pool_size=2, strides=2),
tf.keras.layers.Flatten(),
tf.keras.layers.Dense(1024, activation='relu’),
tf.keras.layers.Dense(10, activation=‘softmax’)  # 10 outputs
```

The full TensorFlow and PyTorch models, with the slides' own slips noted (`filter_size` where slide 47
uses `kernel_size`; `nn.Sequential` with only `torch` imported), are in the
[lecture page](03-convolutional-neural-networks.md), section 16. The second layer's filters are also $3 \times 3$,
but because the image has been scaled down by a factor of two, they do not cover $3 \times 3$ of the original
image (≈41:43).

## Beyond classification

The feature-learning part is general-purpose, so the same CNN body serves many tasks with a different
head: object detection, semantic segmentation with upsampling layers, and continuous control (lecture 3,
sections 17–20; see [computer vision](computer-vision.md)). Convolution is not tied to images either: it
suits any two-dimensional, spatial input; a convolution over patches of a one-dimensional sequence —
"that's also a valid sequence model" — and the same ideas extend to 3D volumetric scans (≈39:23–40:56; see
[sequence modeling](sequence-modeling.md)).

## Where this comes up

- [Lecture 3 — Convolutional Neural Networks](03-convolutional-neural-networks.md), sections 4–16.
- [Lecture 1 — Introduction to Deep Learning](01-introduction.md): the dense layers, activation
  functions and training that a CNN reuses.
- [Lecture 5 — Reinforcement Learning](05-reinforcement-learning.md), section 13: the deep Q
  network that plays Atari from screen pixels is a CNN, two convolution layers then two fully connected.
