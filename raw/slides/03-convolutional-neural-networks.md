---
title: Lecture 3 — Convolutional Neural Networks (slide deck)
lecture: 3
slides: 70
source_pdf: https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L3.pdf
note: Slide N = PDF page N (N = 1..70). The deck prints no slide numbers; the "1/6/26" in each footer is the lecture date (6 January 2026).
---

# Lecture 3 — Convolutional Neural Networks: slide-by-slide

Text and figures of all 70 slides of
[`6S191_MIT_DeepLearning_L3.pdf`](https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L3.pdf)
(MIT 6.S191 Introduction to Deep Learning, 2026 edition; lecturer Alexander Amini; the title slide
reads "Deep Computer Vision"), transcribed from the deck. Cite these as "slide N", where N is the PDF
page number. Diagrams, photographs, matrices and code are described in prose or reproduced, since the
KB is read as text.

Many slides are **build steps**: the same slide re-shown with one more element revealed. They are
transcribed individually, so that a citation to any one of them resolves, with a note of what each
adds to the one before.

## Numbering: slide numbers vs PDF pages

The PDF is a flattened export: every page is a single 1280×720 image with no text layer, and no
page prints a slide number. Headings therefore use the PDF page number, and a reader who opens page
N of the PDF sees slide N. The standard footer on content slides (MIT logo, "MIT Introduction to
Deep Learning", introtodeeplearning.com, @MITDeepLearning, "1/6/26") is not repeated below; citations
printed beside it are, as "Footer credit" lines.

## Images

33 slides carry their page image under the heading: 3, 6, 12, 13, 16, 20, 22, 24, 25, 27–30, 32, 40,
41, 44, 47–52, 56–65 — every slide with a distinct figure. The rest are the title, section dividers,
application photographs and collages, build steps contained in an included slide, code transcribed
exactly (53–54), a video still (66), the summary, and the lab and announcement slides. Use only an
image path that appears below; slides without one have no image.

## Contents

| Slides | Section |
| ------ | ------- |
| 1 | Title: "Deep Computer Vision" |
| 2–8 | What vision is ("to know what is where by looking"); the rise and impact of computer vision: facial detection and recognition, self-driving cars, medicine, biology and healthcare, accessibility |
| 9–13 | What computers "see": images are numbers (a grayscale pixel matrix, RGB as three channels); tasks in computer vision, regression and classification |
| 14–18 | High-level feature detection; manual feature extraction and its problems (viewpoint, illumination, scale and other variation); learning a hierarchy of feature representations |
| 19–25 | Learning visual features: fully connected networks and their drawbacks; using spatial structure (patches, sliding windows); feature extraction with convolution |
| 26–42 | A case study: "X or X?", the features of X and filters that detect them, the convolution operation worked step by step on a 5×5 image with a 3×3 filter, feature maps produced by different filters, feature extraction with convolution |
| 43–54 | Convolutional neural networks: the CNN pipeline, convolutional layers and local connectivity, the output volume, ReLU, max pooling, representation learning, CNNs for classification, TensorFlow and PyTorch code |
| 55–67 | An architecture for many applications: classification (breast cancer screening), object detection (a naive solution, R-CNN, Faster R-CNN), semantic segmentation (fully convolutional networks), continuous control (end-to-end navigation), impact |
| 68–70 | Summary; Lab 2 (facial detection); announcements |

## Slide 1 — Deep Computer Vision

Title slide. Black background; at left a glowing blue network of nodes and lines (a mesh of connected points). A faint large diagonal watermark "MIT 6.S191" sits behind the text. Text, centred at right:

"Deep Computer Vision"
"Alexander Amini"
"MIT Introduction to Deep Learning"
"January 6, 2026"

The MIT logo is at bottom centre-left and an "MIT EECS" logo at bottom right.

*Figure: no*

## Slide 2 — [Quote: "To know what is where by looking."]

Full-slide black-and-white close-up photograph of a human eye (side view, with long eyelashes), with only the iris coloured blue. Text at bottom left, in bold: "To know what is where by looking."

*Figure: yes — close-up photograph of a blue eye with the quote at bottom left*

## Slide 3 — [To discover from images what is present in the world]

![Slide 3 — [To discover from images what is present in the world]](../images/03-convolutional-neural-networks/slide-3.jpg)

Full-slide photograph of a busy New York City street (a yellow taxi in the centre, a black car at right, a white van at left, pedestrians crossing, traffic lights). A dark translucent banner across the top reads: "To discover from images what is present in the world, where things are, what actions are taking place, to predict and anticipate events in the world".

Red rectangular bounding boxes are drawn around the white van at left, a group of pedestrians at left, the yellow taxi, a pedestrian crossing at centre, a distant bus, a traffic light at upper right, a pedestrian at right, and a black car at centre-right. Two short red arrows between the central pedestrian and the pedestrian at right point towards each other (predicted motion). The figure shows detection of objects, locations and actions.

*Figure: yes — street photograph with red bounding boxes around vehicles, people and a traffic light, and red motion arrows*

## Slide 4 — The rise and impact of computer vision

Title: "The rise and impact of computer vision". A collage of five panels, each with a bold label:

- "Robotics": a photo of a humanoid robot (white and black) mid-stride on a blue floor in a large laboratory with yellow railings.
- "Accessibility": a smartphone showing a social-network news feed; a post by "Manohor Paluri" reading "With my college buddies in my favorite place - ready for a great weekend!" with a photo of tall trees seen from below, and an overlaid caption "Image may contain: tree, sky, outdoor".
- "Biology & Medicine": two greyscale mammogram X-ray images side by side, each with a small orange square marking a region of interest.
- "Autonomous driving": a colourful lidar point-cloud scene of a street and parked cars, with a car in the centre surrounded by concentric rings.
- "Mobile computing": a smartphone camera screen in landscape showing three smiling people at a table, with square boxes drawn on the detected faces.

Footer credit: Boston Dynamics; P. Isola 6.869

*Figure: yes — five application photos: humanoid robot, phone image-captioning feed, mammograms with marked regions, lidar autonomous-driving scene, phone camera face detection*

## Slide 5 — Impact: Facial Detection & Recognition

Left column, top to bottom, a vertical flow of three icons joined by downward arrows: a black eye icon, a trapezoid (wide at top, narrow at bottom) containing a small layered network of circles (a neural network), and a black silhouette of a human head in profile. Right: two greyscale portrait photos of the same young man's face side by side. The left photo has yellow dots marking facial landmarks (eyebrows, eyes, nose, lips, jaw outline). The right photo has a yellow triangular mesh drawn over the whole face.

*Figure: yes — eye to network to head flow icons, with a face showing yellow landmark dots and a face covered by a yellow triangle mesh*

## Slide 6 — Impact: Self-Driving Cars

![Slide 6 — Impact: Self-Driving Cars](../images/03-convolutional-neural-networks/slide-6.jpg)

Left column: the same eye, network-trapezoid, arrow flow as slide 5, but ending in a black steering-wheel icon. Right: a video still from inside a car, a man in the driver's seat looking ahead with hands near the wheel, trees outside. Overlay text at top left: a green circle with "AUTONOMOUS" and "24.0 mph". A red circular play button is at the centre. An inset at lower right shows the forward camera view of a paved road lined with trees, with a green rectangle and a blue curve drawn on the road (the planned path).

Footer credit: Amini+ *ICRA* 2019.

*Figure: yes — eye to network to steering wheel flow icons and a video still of an autonomous drive with a camera inset showing the planned path*

## Slide 7 — Impact: Medicine, Biology, Healthcare

Left column: the eye, network-trapezoid flow, ending in a black stethoscope icon. Right, three labelled groups of images:

- "Breast cancer": a mammogram X-ray with an orange square around a region near the bottom.
- "COVID-19": a greyscale chest X-ray.
- "Skin cancer": four close-up photos of skin lesions (brown or tan patches of differing size and shape, the last with a hair across it).

Footer credit: Esteva+ *Nature* 2017, McKinney+ *Nature* 2020, Wang+ *Sci. Rep.* 2020.

*Figure: yes — eye to network to stethoscope flow icons, a mammogram with a marked region, a chest X-ray and four skin-lesion photos*

## Slide 8 — Impact: Accessibility

Two panels. Left: a photograph from behind of a man running on a paved forest path with a yellow line painted down the left side, wearing a cap, grey shirt and an orange waist pack. Upper right: a close-up of a hand holding a smartphone whose screen shows a road with a green line along the painted line, another hand holding a cord or leash. Lower right: a grid of about 5 by 5 small road-surface images, each with a green or yellow line segmented along the painted line.

Footer credit: Google Project Guideline

*Figure: yes — runner on a path with a painted yellow line, phone showing the detected line, and a grid of road images with the line highlighted*

## Slide 9 — What Computers "See"

Section-divider slide: blue background, centred white title "What Computers "See"".

*Figure: no*

## Slide 10 — Images are Numbers

A low-resolution greyscale portrait (a face with a beard, each pixel a visible grey square) at left: the same portrait as slides 11–12, whose 16 rows by 12 columns of values slide 12 prints. Nothing else on the slide.

Footer credit: Levin *Image Processing & Computer Vision.*

*Figure: yes — pixelated greyscale portrait*

## Slide 11 — Images are Numbers

Build step: adds a numbered pixel grid to slide 10.

Same pixelated portrait at left. Beside it, the same image again with each pixel square labelled with its numeric grey value (the numbers are printed on the grey cells, whose shades follow the values; the same numbers are given in full on slide 12).

Footer credit: Levin *Image Processing & Computer Vision.*

*Figure: yes — pixelated portrait next to the same image with a number printed in each pixel*

## Slide 12 — Images are Numbers

![Slide 12 — Images are Numbers](../images/03-convolutional-neural-networks/slide-12.jpg)

Build step: adds a plain number matrix, a label and a caption to slide 11.

Same pixelated portrait (left) and same numbered-pixel image (centre). A third panel at right, labelled "What the computer sees", shows only the numbers on a white grid (16 rows by 12 columns), transcribed here:

$$\begin{bmatrix}
157 & 153 & 174 & 168 & 150 & 152 & 129 & 151 & 172 & 161 & 155 & 156 \cr
155 & 182 & 163 & 74 & 75 & 62 & 33 & 17 & 110 & 210 & 180 & 154 \cr
180 & 180 & 50 & 14 & 34 & 6 & 10 & 33 & 48 & 106 & 159 & 181 \cr
206 & 109 & 5 & 124 & 131 & 111 & 120 & 204 & 166 & 15 & 56 & 180 \cr
194 & 68 & 137 & 251 & 237 & 239 & 239 & 228 & 227 & 87 & 71 & 201 \cr
172 & 105 & 207 & 233 & 233 & 214 & 220 & 239 & 228 & 98 & 74 & 206 \cr
188 & 88 & 179 & 209 & 185 & 215 & 211 & 158 & 139 & 75 & 20 & 169 \cr
189 & 97 & 165 & 84 & 10 & 168 & 134 & 11 & 31 & 62 & 22 & 148 \cr
199 & 168 & 191 & 193 & 158 & 227 & 178 & 143 & 182 & 106 & 36 & 190 \cr
205 & 174 & 155 & 252 & 236 & 231 & 149 & 178 & 228 & 43 & 95 & 234 \cr
190 & 216 & 116 & 149 & 236 & 187 & 86 & 150 & 79 & 38 & 218 & 241 \cr
190 & 224 & 147 & 108 & 227 & 210 & 127 & 102 & 36 & 101 & 255 & 224 \cr
190 & 214 & 173 & 66 & 103 & 143 & 96 & 50 & 2 & 109 & 249 & 215 \cr
187 & 196 & 235 & 75 & 1 & 81 & 47 & 0 & 6 & 217 & 255 & 211 \cr
183 & 202 & 237 & 145 & 0 & 0 & 12 & 108 & 200 & 138 & 243 & 236 \cr
195 & 206 & 123 & 207 & 177 & 121 & 123 & 200 & 175 & 13 & 96 & 218
\end{bmatrix}$$

Caption below the three panels: "An image is just a matrix of numbers [0,255]!" and "i.e., 1080x1080x3 for an RGB image".

Footer credit: Levin *Image Processing & Computer Vision.*

*Figure: yes — pixelated portrait, numbered-pixel overlay and the plain number matrix labelled "What the computer sees"*

## Slide 13 — Tasks in Computer Vision

![Slide 13 — Tasks in Computer Vision](../images/03-convolutional-neural-networks/slide-13.jpg)

Left to right: a pixelated greyscale portrait labelled "Input Image"; an arrow to the plain number grid labelled "Pixel Representation" (same matrix as slide 12); an arrow labelled "classification" to a column vector of four labelled values:

| Class | Value |
| --- | --- |
| Lincoln | 0.8 |
| Washington | 0.1 |
| Jefferson | 0.05 |
| Obama | 0.05 |

Below, two bullets:
- "**Regression**: output variable takes continuous value"
- "**Classification**: output variable takes class label. Can produce probability of belonging to a particular class"

*Figure: yes — input image to pixel matrix to classification output vector Lincoln 0.8, Washington 0.1, Jefferson 0.05, Obama 0.05*

## Slide 14 — High Level Feature Detection

Subtitle: "Let's identify key features in each image category". Three photos in a row, each with a caption below:

- A portrait of a woman in a wide-brimmed hat with a feather: "Nose, Eyes, Mouth"
- A dark Jeep-style SUV on a dirt road in front of a hill: "Wheels, License Plate, Headlights"
- A blue two-storey house with white trim, porch and steps: "Door, Windows, Steps"

*Figure: yes — three photos (a face, a car, a house) with their key features listed beneath*

## Slide 15 — Manual Feature Extraction

Three blue chevron arrows in a row, left to right: "Domain knowledge", "Define features", "Detect features to classify". Below them, centred, large text: "Problems?"

*Figure: yes — three-step chevron pipeline*

## Slide 16 — Manual Feature Extraction

![Slide 16 — Manual Feature Extraction](../images/03-convolutional-neural-networks/slide-16.jpg)

Build step: adds a grid of example photos to slide 15 (replacing "Problems?").

Same three blue chevrons: "Domain knowledge", "Define features", "Detect features to classify". Below, a grid of labelled photo examples of why manual features struggle:

- "Viewpoint variation": three photos of the same sculpted face from different angles.
- "Illumination conditions": three photos of a group of penguin figurines under different lighting.
- "Scale variation": a very tall man in black holding a laptop next to a very short man holding a laptop.
- "Deformation": a white cat lying in a twisted pose on a sofa.
- "Background clutter": a spotted cat camouflaged against a leopard-print background.
- "Occlusion": a black cat with only its head visible above a ledge.
- "Intra-class variation": six different chairs (a lounge chair, a red curved chair, a multi-seat bench, a red and yellow chair, a brown chaise, a wire diamond chair).

Footer credit: Li/Johnson/Yeung C231n.

*Figure: yes — grid of photos showing viewpoint variation, illumination, scale, deformation, background clutter, occlusion and intra-class variation*

## Slide 17 — Manual Feature Extraction

Build step: highlights the third chevron of slide 16.

Same photo grid as slide 16 (same labels). The first two chevrons, "Domain knowledge" and "Define features", are faded to very light blue, and only "Detect features to classify" remains in full blue.

Footer credit: Li/Johnson/Yeung C231n.

*Figure: yes — the photo grid of variation examples with only the third chevron highlighted*

## Slide 18 — Learning Feature Representations

Text: "Can we learn a **hierarchy of features** directly from the data instead of hand engineering?" Below, three image grids (each 4 rows by 6 columns of small greyscale tiles), each with a heading above and a description below:

- "Low level features" / "Edges, dark spots": tiles of oriented edge and blob detectors (short dark and light strokes at various angles on grey).
- "Mid level features" / "Eyes, ears, nose": tiles showing parts of faces (eyes, eyebrows, noses, mouths).
- "High level features" / "Facial structure": tiles showing whole faces.

Footer credit: Lee+ *ICML* 2009.

*Figure: yes — three tile grids of learned features: edges and spots, face parts, whole faces*

## Slide 19 — Learning Visual Features

Section-divider slide: blue background, centred white title "Learning Visual Features".

*Figure: no*

## Slide 20 — Fully Connected Neural Network

![Slide 20 — Fully Connected Neural Network](../images/03-convolutional-neural-networks/slide-20.jpg)

Diagram of a fully connected network with five columns of light-blue circles, every circle joined by a line to every circle in the next column: an input column of 8 circles, three hidden columns of 9 circles each, and an output column of 4 circles. No labels.

*Figure: yes — fully connected network with 8 input nodes, three hidden layers of 9 nodes and 4 output nodes*

## Slide 21 — Fully Connected Neural Network

Left text block, headed "**Input:**": bullets "2D image" and "Vector of pixel values".

Centre diagram: inputs labelled $x_1$, $x_2$, vertical dots, and $x_p$, each with an arrow to its own blue circle; arrows from each of these three circles converge on a single blue circle at the right.

Right text block, headed "**Fully Connected:**": bullets "Connect neuron in hidden layer to all neurons in input layer", "No spatial information!", "And many, many parameters!"

*Figure: yes — input values x1 to xp each connected to a single hidden neuron*

## Slide 22 — Fully Connected Neural Network

![Slide 22 — Fully Connected Neural Network](../images/03-convolutional-neural-networks/slide-22.jpg)

Build step: adds a closing question to slide 21.

Same slide as slide 21 ("**Input:**" with "2D image" and "Vector of pixel values"; the diagram of $x_1$, $x_2$, dots, $x_p$ feeding one hidden neuron; "**Fully Connected:**" with "Connect neuron in hidden layer to all neurons in input layer", "No spatial information!", "And many, many parameters!"). New text at the bottom: "How can we use **spatial structure** in the input to inform the architecture of the network?"

*Figure: yes — input values x1 to xp each connected to a single hidden neuron*

## Slide 23 — Using Spatial Structure

Left text: "**Input:** 2D image. Array of pixel values". Centre: a square grid of white circles (about 13 by 13) representing the input pixels. A red square outlines a 4 by 4 patch near the upper middle; lines run from the four corner pixels of the patch to a single blue circle at the lower right, outside the grid. Right text: "**Idea:** connect patches of input to neurons in hidden layer." and, in smaller text, "Neuron connected to region of input. Only "sees" these values."

*Figure: yes — pixel grid with a red 4 by 4 patch whose corner pixels connect to a single hidden neuron*

## Slide 24 — Using Spatial Structure

![Slide 24 — Using Spatial Structure](../images/03-convolutional-neural-networks/slide-24.jpg)

Two side-by-side copies of a diagram, separated by a vertical dotted line. In each, a grid of about 13 by 13 white circles (input) shows a red square outlining a 4 by 4 patch with lines from its corner pixels to one neuron in a smaller 6 by 6 grid of circles (the next layer). In the left diagram the patch is at the top-left of the input and the connected neuron is the top-left neuron of the small grid. In the right diagram the patch has slid two pixels to the right and the connected neuron is the next neuron along the top row of the small grid.

Text below: "Connect patch in input layer to a single neuron in subsequent layer." "Use a sliding window to define connections." "*How can we **weight** the patch to detect particular features?*"

*Figure: yes — two diagrams of a sliding 4 by 4 patch on the input mapping to successive neurons in a smaller layer*

## Slide 25 — Feature Extraction with Convolution

![Slide 25 — Feature Extraction with Convolution](../images/03-convolutional-neural-networks/slide-25.jpg)

Top left: the input grid of circles with a red 4 by 4 patch at the top-left connected by lines to the top-left neuron of a smaller grid of circles (the same picture as slide 24, left). Top right, three dashed bullets:
- "Filter of size 4x4 : 16 different weights"
- "Apply this same filter to 4x4 patches in input"
- "Shift by 2 pixels for next patch"

Then: "This "patchy" operation is **convolution**".

Below, three numbered lines:
- "1) Apply a set of weights – a filter – to extract **local features**"
- "2) Use **multiple filters** to extract different features"
- "3) **Spatially share** parameters of each filter"

*Figure: yes — input pixel grid with a red patch connected to one neuron of a smaller output grid*

## Slide 26 — Feature Extraction and Convolution: A Case Study

Section-divider slide: blue background, centred white title "Feature Extraction and Convolution" with the subtitle "A Case Study".

*Figure: no*

## Slide 27 — X or X?

![Slide 27 — X or X?](../images/03-convolutional-neural-networks/slide-27.jpg)

Two 9 by 9 pixel grids, each pixel printed as -1 (black) or 1 (white), with a large dark-blue question mark above an equals sign between them (an "=?" comparison). Both grids show an X made of 1s on a background of -1s.

Left grid (a clean, symmetric X):

$$\begin{bmatrix}
-1 & -1 & -1 & -1 & -1 & -1 & -1 & -1 & -1 \cr
-1 & 1 & -1 & -1 & -1 & -1 & -1 & 1 & -1 \cr
-1 & -1 & 1 & -1 & -1 & -1 & 1 & -1 & -1 \cr
-1 & -1 & -1 & 1 & -1 & 1 & -1 & -1 & -1 \cr
-1 & -1 & -1 & -1 & 1 & -1 & -1 & -1 & -1 \cr
-1 & -1 & -1 & 1 & -1 & 1 & -1 & -1 & -1 \cr
-1 & -1 & 1 & -1 & -1 & -1 & 1 & -1 & -1 \cr
-1 & 1 & -1 & -1 & -1 & -1 & -1 & 1 & -1 \cr
-1 & -1 & -1 & -1 & -1 & -1 & -1 & -1 & -1
\end{bmatrix}$$

Right grid (a deformed, slightly shifted X):

$$\begin{bmatrix}
-1 & -1 & -1 & -1 & -1 & -1 & -1 & -1 & -1 \cr
-1 & -1 & -1 & -1 & -1 & -1 & 1 & -1 & -1 \cr
-1 & 1 & -1 & -1 & -1 & 1 & -1 & -1 & -1 \cr
-1 & -1 & 1 & 1 & -1 & 1 & -1 & -1 & -1 \cr
-1 & -1 & -1 & -1 & 1 & -1 & -1 & -1 & -1 \cr
-1 & -1 & -1 & 1 & -1 & 1 & 1 & -1 & -1 \cr
-1 & -1 & -1 & 1 & -1 & -1 & -1 & 1 & -1 \cr
-1 & -1 & 1 & -1 & -1 & -1 & -1 & -1 & -1 \cr
-1 & -1 & -1 & -1 & -1 & -1 & -1 & -1 & -1
\end{bmatrix}$$

Text below: "Image is represented as matrix of pixel values… and computers are literal!" and "We want to be able to classify an X as an X even if it's shifted, shrunk, rotated, deformed."

Footer credit: Rohrer *How do CNNs work?*

*Figure: yes — two 9 by 9 grids of minus one and one pixel values each showing an X, one clean and one deformed, with an equals-question-mark between them*

## Slide 28 — Features of X

![Slide 28 — Features of X](../images/03-convolutional-neural-networks/slide-28.jpg)

Two black-and-white pixel grids (about 9 by 9, no numbers printed), the same two Xs as slide 27, left the clean X and right the deformed X. Three small coloured squares/rectangles are drawn on each grid, and lines of the same colour run from each marked region on the left grid, via a large equals sign in the centre column, to the matching region on the right grid:

- Teal box (2 by 2 pixels): in the upper left arm of the X, a diagonal pair of white pixels; teal lines converge on the top "=" sign.
- Orange box (3 by 3 pixels): at the centre of the X, a white-black checker pattern (white at the four corners and centre); orange lines converge on the middle "=" sign.
- Purple box (2 by 2 pixels): in the lower left arm, a diagonal pair of white pixels in the other direction; purple lines converge on the bottom "=" sign.

The slide shows that the same small local features appear in both X images even though the whole images differ.

Footer credit: Rohrer *How do CNNs work?*

*Figure: yes — two X pixel images with matching teal, orange and purple local patches linked by equals signs*

## Slide 29 — Filters to Detect X Features

![Slide 29 — Filters to Detect X Features](../images/03-convolutional-neural-networks/slide-29.jpg)

Left label: "filters". Three 3 by 3 filters in a row (white cells are 1, black cells are -1):

First filter (diagonal from top left to bottom right):

$$\begin{bmatrix} 1 & -1 & -1 \cr -1 & 1 & -1 \cr -1 & -1 & 1 \end{bmatrix}$$

Second filter (centre and four corners):

$$\begin{bmatrix} 1 & -1 & 1 \cr -1 & 1 & -1 \cr 1 & -1 & 1 \end{bmatrix}$$

Third filter (diagonal from top right to bottom left):

$$\begin{bmatrix} -1 & -1 & 1 \cr -1 & 1 & -1 \cr 1 & -1 & -1 \end{bmatrix}$$

Below is a 9 by 9 black-and-white image of an X (white pixels on black; no numbers printed; the same clean X as the left grid of slide 27). A teal 3 by 3 box is drawn on rows 2–4, columns 2–4, the top-left arm of the X, and teal lines run from the corners of this box up to the corners of the first filter, showing that filter being applied at that patch.

Footer credit: Rohrer *How do CNNs work?*

*Figure: yes — three 3 by 3 filters for X features and an X image with a teal patch linked to the first filter*

## Slide 30 — The Convolution Operation

![Slide 30 — The Convolution Operation](../images/03-convolutional-neural-networks/slide-30.jpg)

A worked example of applying the first X filter to one patch of the clean X image.

Top left: the 3 by 3 filter

$$\begin{bmatrix} 1 & -1 & -1 \cr -1 & 1 & -1 \cr -1 & -1 & 1 \end{bmatrix}$$

with its bottom-right entry (1) boxed in orange. Orange lines run from that entry to an orange box in the equation "1 x 1 = 1", where the second factor is boxed in yellow. Yellow lines connect that second factor to the yellow-boxed bottom-right pixel of the highlighted patch in the image below. A teal outline marks the 3 by 3 patch (rows 2 to 4, columns 2 to 4) of the image, and teal lines connect the filter's corners to that patch.

The image (9 by 9, same clean X as the left grid of slide 27):

$$\begin{bmatrix}
-1 & -1 & -1 & -1 & -1 & -1 & -1 & -1 & -1 \cr
-1 & 1 & -1 & -1 & -1 & -1 & -1 & 1 & -1 \cr
-1 & -1 & 1 & -1 & -1 & -1 & 1 & -1 & -1 \cr
-1 & -1 & -1 & 1 & -1 & 1 & -1 & -1 & -1 \cr
-1 & -1 & -1 & -1 & 1 & -1 & -1 & -1 & -1 \cr
-1 & -1 & -1 & 1 & -1 & 1 & -1 & -1 & -1 \cr
-1 & -1 & 1 & -1 & -1 & -1 & 1 & -1 & -1 \cr
-1 & 1 & -1 & -1 & -1 & -1 & -1 & 1 & -1 \cr
-1 & -1 & -1 & -1 & -1 & -1 & -1 & -1 & -1
\end{bmatrix}$$

At right, labels "element wise multiply" and "add outputs". An element-wise product symbol (a circle with a dot) joins the filter-patch comparison to a 3 by 3 grid in which every entry is 1 (the bottom-right 1 is boxed in teal):

$$\begin{bmatrix} 1 & 1 & 1 \cr 1 & 1 & 1 \cr 1 & 1 & 1 \end{bmatrix}$$

followed by "= 9" (the sum of the nine products).

Footer credit: Rohrer *How do CNNs work?*

*Figure: yes — filter applied to a matching patch of the X image, element-wise products all 1, summing to 9*

## Slide 31 — The Convolution Operation

Text: "Suppose we want to compute the convolution of a 5x5 image and a 3x3 filter:". Left, a 5 by 5 green grid labelled "image":

$$\begin{bmatrix} 1 & 1 & 1 & 0 & 0 \cr 0 & 1 & 1 & 1 & 0 \cr 0 & 0 & 1 & 1 & 1 \cr 0 & 0 & 1 & 1 & 0 \cr 0 & 1 & 1 & 0 & 0 \end{bmatrix}$$

A circled-cross convolution symbol, then a 3 by 3 orange grid labelled "filter":

$$\begin{bmatrix} 1 & 0 & 1 \cr 0 & 1 & 0 \cr 1 & 0 & 1 \end{bmatrix}$$

Bottom text: "We slide the 3x3 filter over the input image, element-wise multiply, and add the outputs…"

Footer credit: Karn *Intuitive CNNs*

*Figure: yes — 5 by 5 binary image and 3 by 3 filter joined by the convolution symbol*

## Slide 32 — The Convolution Operation

![Slide 32 — The Convolution Operation](../images/03-convolutional-neural-networks/slide-32.jpg)

Build step: adds the first filter position and a feature map to slide 31.

Text: "We slide the 3x3 filter over the input image, element-wise multiply, and add the outputs:". The same 5 by 5 image as slide 31, with the top-left 3 by 3 patch coloured orange; each cell in the patch carries a small red subscript giving the filter weight it is multiplied by:

| | col 1 | col 2 | col 3 |
| --- | --- | --- | --- |
| row 1 | 1 (×1) | 1 (×0) | 1 (×1) |
| row 2 | 0 (×0) | 1 (×1) | 1 (×0) |
| row 3 | 0 (×1) | 0 (×0) | 1 (×1) |

The remaining cells stay green. Then the convolution symbol, the filter (1 0 1 / 0 1 0 / 1 0 1, label "filter"), an equals sign and an empty 3 by 3 grid labelled "feature map" whose top-left cell is shaded pink and holds 4.

Footer credit: Karn *Intuitive CNNs*

*Figure: yes — filter patch at the top-left of the image with per-cell weights, and a feature map whose first entry is 4*

## Slide 33 — The Convolution Operation

Build step: moves the filter one pixel to the right on slide 32.

Same text and layout. The orange patch is now columns 2 to 4 of rows 1 to 3 of the 5 by 5 image, with weights shown as red subscripts:

| | col 2 | col 3 | col 4 |
| --- | --- | --- | --- |
| row 1 | 1 (×1) | 1 (×0) | 0 (×1) |
| row 2 | 1 (×0) | 1 (×1) | 1 (×0) |
| row 3 | 0 (×1) | 1 (×0) | 1 (×1) |

The feature map (3 by 3) now has its first two cells filled and shaded pink: 4 and 3; the rest is empty.

Footer credit: Karn *Intuitive CNNs*

*Figure: yes — filter shifted one pixel right and a feature map holding 4 and 3*

## Slide 34 — The Convolution Operation

Build step: moves the filter one more pixel to the right on slide 33.

Same text and layout. The orange patch is now columns 3 to 5 of rows 1 to 3 of the 5 by 5 image, with weights as red subscripts:

| | col 3 | col 4 | col 5 |
| --- | --- | --- | --- |
| row 1 | 1 (×1) | 0 (×0) | 0 (×1) |
| row 2 | 1 (×0) | 1 (×1) | 0 (×0) |
| row 3 | 1 (×1) | 1 (×0) | 1 (×1) |

The feature map's first row is now filled (shaded pink): 4, 3, 4.

Footer credit: Karn *Intuitive CNNs*

*Figure: yes — filter at the top-right position and a feature map whose first row is 4, 3, 4*

## Slide 35 — The Convolution Operation

Build step: moves the filter back to the left edge and down one pixel on slide 34.

Same text and layout. The orange patch is now rows 2 to 4, columns 1 to 3 of the 5 by 5 image, with weights as red subscripts:

| | col 1 | col 2 | col 3 |
| --- | --- | --- | --- |
| row 2 | 0 (×1) | 1 (×0) | 1 (×1) |
| row 3 | 0 (×0) | 0 (×1) | 1 (×0) |
| row 4 | 0 (×1) | 0 (×0) | 1 (×1) |

The feature map is now: first row 4, 3, 4; second row begins with 2 (shaded pink), the other cells empty.

Footer credit: Karn *Intuitive CNNs*

*Figure: yes — filter at the left of the second row of positions and a feature map holding 4, 3, 4 and 2*


## Slide 36 — The Convolution Operation

Build step: moves the filter window one pixel right from slide 35 and fills in the next feature-map value.

"We slide the 3x3 filter over the input image, element-wise multiply, and add the outputs:"

Left, a 5x5 input image (green cells, binary values):

$$\begin{bmatrix} 1 & 1 & 1 & 0 & 0 \cr 0 & 1 & 1 & 1 & 0 \cr 0 & 0 & 1 & 1 & 1 \cr 0 & 0 & 1 & 1 & 0 \cr 0 & 1 & 1 & 0 & 0 \end{bmatrix}$$

The 3x3 window now highlighted in orange covers rows 2–4, columns 2–4. Each cell carries a small red subscript giving the filter weight it is multiplied by: row 2: $1_{\times 1}, 1_{\times 0}, 1_{\times 1}$; row 3: $0_{\times 0}, 1_{\times 1}, 1_{\times 0}$; row 4: $0_{\times 1}, 1_{\times 0}, 1_{\times 1}$.

Middle, after a circled-cross (convolution) symbol, the "filter" (orange):

$$\begin{bmatrix} 1 & 0 & 1 \cr 0 & 1 & 0 \cr 1 & 0 & 1 \end{bmatrix}$$

After an equals sign, the "feature map" (3x3 grid, filled cells pink): first row 4, 3, 4; second row 2, 4, and an empty cell; third row empty.

Footer credit: Karn *Intuitive CNNs*

*Figure: yes — convolution worked example with 5x5 input, window shifted right, 3x3 filter and partly filled feature map*

## Slide 37 — The Convolution Operation

Build step: moves the filter window one pixel right from slide 36 and fills in the next feature-map value.

"We slide the 3x3 filter over the input image, element-wise multiply, and add the outputs:"

Same 5x5 input image as slide 36 (rows 1 1 1 0 0 / 0 1 1 1 0 / 0 0 1 1 1 / 0 0 1 1 0 / 0 1 1 0 0). The orange window now covers rows 2–4, columns 3–5, with weight subscripts: row 2: $1_{\times 1}, 1_{\times 0}, 0_{\times 1}$; row 3: $1_{\times 0}, 1_{\times 1}, 1_{\times 0}$; row 4: $1_{\times 1}, 1_{\times 0}, 0_{\times 1}$.

Same filter (1 0 1 / 0 1 0 / 1 0 1). Feature map: first row 4, 3, 4; second row 2, 4, 3; third row empty.

Footer credit: Karn *Intuitive CNNs*

*Figure: yes — convolution worked example with window at rows 2–4, columns 3–5 and two feature-map rows filled*

## Slide 38 — The Convolution Operation

Build step: moves the filter window to the start of the next row (from slide 37) and fills in the next feature-map value.

"We slide the 3x3 filter over the input image, element-wise multiply, and add the outputs:"

Same 5x5 input image. The orange window now covers rows 3–5, columns 1–3, with weight subscripts: row 3: $0_{\times 1}, 0_{\times 0}, 1_{\times 1}$; row 4: $0_{\times 0}, 0_{\times 1}, 1_{\times 0}$; row 5: $0_{\times 1}, 1_{\times 0}, 1_{\times 1}$.

Same filter. Feature map: first row 4, 3, 4; second row 2, 4, 3; third row 2, empty, empty.

Footer credit: Karn *Intuitive CNNs*

*Figure: yes — convolution worked example with window at rows 3–5, columns 1–3 and feature map filled through its first cell of row three*

## Slide 39 — The Convolution Operation

Build step: moves the filter window one pixel right from slide 38 and fills in the next feature-map value.

"We slide the 3x3 filter over the input image, element-wise multiply, and add the outputs:"

Same 5x5 input image. The orange window covers rows 3–5, columns 2–4, with weight subscripts: row 3: $0_{\times 1}, 1_{\times 0}, 1_{\times 1}$; row 4: $0_{\times 0}, 1_{\times 1}, 1_{\times 0}$; row 5: $1_{\times 1}, 1_{\times 0}, 0_{\times 1}$.

Same filter. Feature map: first row 4, 3, 4; second row 2, 4, 3; third row 2, 3, and an empty cell.

Footer credit: Karn *Intuitive CNNs*

*Figure: yes — convolution worked example with window at rows 3–5, columns 2–4 and feature map missing only its last cell*

## Slide 40 — The Convolution Operation

![Slide 40 — The Convolution Operation](../images/03-convolutional-neural-networks/slide-40.jpg)

Build step: moves the filter window to the last position and completes the feature map from slide 39.

"We slide the 3x3 filter over the input image, element-wise multiply, and add the outputs:"

Same 5x5 input image. The orange window covers rows 3–5, columns 3–5, with weight subscripts: row 3: $1_{\times 1}, 1_{\times 0}, 1_{\times 1}$; row 4: $1_{\times 0}, 1_{\times 1}, 0_{\times 0}$; row 5: $1_{\times 1}, 0_{\times 0}, 0_{\times 1}$.

Same filter. The completed feature map (all cells pink):

$$\begin{bmatrix} 4 & 3 & 4 \cr 2 & 4 & 3 \cr 2 & 3 & 4 \end{bmatrix}$$

Footer credit: Karn *Intuitive CNNs*

*Figure: yes — convolution worked example, final window position and completed 3x3 feature map*

## Slide 41 — Producing Feature Maps

![Slide 41 — Producing Feature Maps](../images/03-convolutional-neural-networks/slide-41.jpg)

Four greyscale square images in a row, each with a caption below. All are the same portrait photograph of a woman in a wide-brimmed hat, looking over her shoulder, with a dark curved shape at right.

1. "Original": the unmodified photograph.
2. "Sharpen": the photograph with crisper detail. A cyan-outlined 3x3 grid overlaid at the lower right shows the kernel:

$$\begin{bmatrix} 0 & -1 & 0 \cr -1 & 5 & -1 \cr 0 & -1 & 0 \end{bmatrix}$$

3. "Edge Detect": a mostly black image in which only faint outlines of the hat, hair and face show as thin light lines. Overlaid kernel:

$$\begin{bmatrix} 0 & 1 & 0 \cr 1 & -4 & 1 \cr 0 & 1 & 0 \end{bmatrix}$$

4. "\"Strong\" Edge Detect" (printed as "Strong" in quotation marks): a black image with brighter, more pronounced edge lines of the hat, hair and face. Overlaid kernel:

$$\begin{bmatrix} -1 & -2 & -1 \cr 0 & 0 & 0 \cr 1 & 2 & 1 \end{bmatrix}$$

The slide shows how different filters applied to the same image produce different feature maps. No footer credit is printed.

*Figure: yes — original photograph and three filtered versions (sharpen, edge detect, strong edge detect) with their 3x3 kernels*

## Slide 42 — Feature Extraction with Convolution

Diagram: at upper left a large square grid of small empty circles (roughly 14 by 14, neurons or pixels, the input layer). A red square outlines a 4x4 patch of circles in its top-left corner. Four black arrows run from the corners of that red patch to the top-left circle of a smaller square grid of circles at the lower right (roughly 6 by 6, the output layer), showing that the whole patch maps to one output unit.

Below the diagram, three centred lines:

"1) Apply a set of weights – a filter – to extract **local features**"
"2) Use **multiple filters** to extract different features"
"3) **Spatially share** parameters of each filter"

*Figure: yes — grid of input circles with a highlighted patch connected by arrows to one circle in a smaller output grid*

## Slide 43 — [Section divider: Convolutional Neural Networks (CNNs)]

Section-divider slide: blue background, centred white title "Convolutional Neural Networks (CNNs)".

*Figure: no*

## Slide 44 — CNNs for Classification

![Slide 44 — CNNs for Classification](../images/03-convolutional-neural-networks/slide-44.jpg)

Diagram of a CNN pipeline, left to right, drawn as line art:
- "Input image": a single square. A small dashed square patch inside it is joined by dashed lines to a small dashed square in the first of the next stack.
- "Convolution (feature maps)": a stack of three overlapping squares (feature maps).
- "Maxpooling": a smaller stack of three overlapping squares, joined to the previous stack by dashed lines.
- "Fully-connected layer": a column of six circles arranged along a diagonal, joined to the pooled maps by dashed lines.

Below the diagram, a numbered list with code chips at either side. At left, under an orange TensorFlow logo, three dark chips: `tf.keras.layers.Conv2D`, `tf.keras.activations.*`, `tf.keras.layers.MaxPool2D`. At right, under an orange PyTorch logo, three chips: `torch.nn.Conv2d`, `torch.nn.ReLU,…`, `torch.nn.MaxPool2d`. Between them:

"1. **Convolution**: Apply filters to generate feature maps."
"2. **Non-linearity**: Often ReLU."
"3. **Pooling**: Downsampling operation on each feature map."

Bottom, bold, centred: "Train model with image data." / "Learn weights of filters in convolutional layers."

*Figure: yes — CNN pipeline diagram (input image, convolution feature maps, maxpooling, fully-connected layer) with TensorFlow and PyTorch code chips*

## Slide 45 — Convolutional Layers: Local Connectivity

Diagram: at left a large grid of empty circles (about 14 columns by 13 rows, the input layer) with a red square outlining a 4x4 patch in the top-left corner. Four black arrows run from the patch corners to the top-left circle of a smaller grid of circles (about 6 by 6) at the centre right, showing that one hidden neuron takes its inputs from the patch.

At top right, two code chips: a TensorFlow logo with `tf.keras.layers.Conv2D` and a PyTorch logo with `torch.nn.Conv2d`.

Text at right: "For a neuron in hidden layer:" followed by three dashed items:
"- Take inputs from patch"
"- Compute weighted sum"
"- Apply bias"

*Figure: yes — input grid with a highlighted 4x4 patch connected by arrows to one neuron in a smaller hidden grid, plus code chips*

## Slide 46 — Convolutional Layers: Local Connectivity

Build step: adds the formula and a summary list to slide 45.

Same diagram, code chips and "For a neuron in hidden layer:" list as slide 45. New elements below the diagram:

- At left: "4x4 filter: matrix of weights $w_{ij}$"
- Centre, formula:

$$\sum_{i=1}^{4} \sum_{j=1}^{4} w_{ij} \thinspace x_{i+p, \thinspace j+q} + b$$

with caption "for neuron (p,q) in hidden layer".
- At right, centred three lines: "1) applying a window of weights" / "2) computing linear combinations" / "3) activating with non-linear function"

*Figure: yes — local-connectivity diagram (input grid, 4x4 patch, hidden grid) with the weighted-sum formula for neuron (p,q)*

## Slide 47 — CNNs: Spatial Arrangement of Output Volume

![Slide 47 — CNNs: Spatial Arrangement of Output Volume](../images/03-convolutional-neural-networks/slide-47.jpg)

Diagram at left: a pale pink slab (the input) labelled "32" along its side, "32" along its bottom and "3" at its lower left (depth). A small darker pink block inside the slab sends four black lines to a row of five blue circles inside a horizontal blue bar, which sits within a large pale-blue cube (the output volume). The cube's edges are labelled "depth" (green, top), "height" (dark blue, right) and "width" (red, bottom right). The row of circles runs along the depth direction, showing that one input patch feeds a column of neurons through the full depth.

Text at right:

"**Layer Dimensions:**" then $h \times w \times d$ (h in blue, w in red, d in green) then "where h and w are spatial dimensions" / "d (depth) = number of filters"
"**Stride:**" "Filter step size"
"**Receptive Field:**" "Locations in input image that a node is path connected to" (printed as "path connected"; presumably "patch")

Code chips at the bottom:

```
tf.keras.layers.Conv2D( filters=d, kernel_size=(h,w), strides=s )
```

```
torch.nn.Conv2d( in_channels=3, out_channels=d, kernel_size=(h,w), stride=s )
```

(the "3" in the PyTorch chip is highlighted in pink). Italic note beside the PyTorch chip: "Need to specify input dimensionality!"

*Figure: yes — input slab (32 by 32 by 3) connected to a 3D output volume labelled height, width and depth, with code chips*

## Slide 48 — Introducing Non-Linearity

![Slide 48 — Introducing Non-Linearity](../images/03-convolutional-neural-networks/slide-48.jpg)

Left text:
"- Apply after every convolution operation (i.e., after convolutional layers)"
"- ReLU: pixel-by-pixel operation that replaces all negative values by zero. **Non-linear operation!**"

Below, a black panel with two greyscale feature-map images joined by a blue arrow labelled "ReLU". Left image, titled "Input Feature Map", is a grey edge-response map of a city-like building scene, with caption "Black = negative; white = positive values". Right image, titled "Rectified Feature Map", is the same map in which the dark (negative) regions have become uniform mid-grey, with caption "Only non-negative values".

Right: heading "Rectified Linear Unit (ReLU)" above a plot. Horizontal axis: ticks at −10, −5, 5, 10 (origin at the axis crossing); vertical axis: ticks at 2, 4, 6, 8, 10. One series, a purple line: zero for negative inputs, then rising along the diagonal to reach 10 at an input of 10. Under the plot: $g(z) = \max(0, z)$. Code chips: `tf.keras.layers.ReLU` (with TensorFlow logo) and `torch.nn.ReLU` (with PyTorch logo).

Footer credit: Karn *Intuitive CNNs*

*Figure: yes — input and rectified feature-map images with ReLU arrow, ReLU plot, and code chips*

## Slide 49 — Pooling

![Slide 49 — Pooling](../images/03-convolutional-neural-networks/slide-49.jpg)

Left: a 4x4 grid of numbers with colour-coded 2x2 blocks, an upward arrow at its left labelled "x" and a rightward arrow below labelled "y":

| | col 1 | col 2 | col 3 | col 4 |
| --- | --- | --- | --- | --- |
| row 1 (top) | 1 | 1 | 2 | 4 |
| row 2 | 5 | 6 | 7 | 8 |
| row 3 | 3 | 2 | 1 | 0 |
| row 4 (bottom) | 1 | 2 | 3 | 4 |

The top-left block (1 1 / 5 6) is pink, top-right (2 4 / 7 8) green, bottom-left (3 2 / 1 2) yellow, bottom-right (1 0 / 3 4) blue.

A rightward arrow carries the label "max pool with 2x2 filters and stride 2" to the output, a 2x2 grid in the matching colours:

$$\begin{bmatrix} 6 & 8 \cr 3 & 4 \end{bmatrix}$$

Under the arrow, two code chips:

```
tf.keras.layers.MaxPool2D(
   pool_size=(2,2),
   strides=2
)
```

```
torch.nn.MaxPool2d(
   kernel_size=(2,2),
   stride=2
)
```

At right of the output: "1) Reduced dimensionality" / "2) Spatial invariance". Bottom, centred: "How else can we downsample and preserve spatial invariance?"

*Figure: yes — max-pooling worked example on a 4x4 grid with colour-coded 2x2 blocks giving a 2x2 output, plus code chips*

## Slide 50 — Representation Learning in Deep CNNs

![Slide 50 — Representation Learning in Deep CNNs](../images/03-convolutional-neural-networks/slide-50.jpg)

Three rows of greyscale image tiles, left to right, joined by two black right-pointing arrows. Each group is titled above and labelled below.

1. "Low level features" (4 rows by 6 columns of small tiles showing oriented edge, stripe and blob patterns and dark spots); beneath: "Edges, dark spots" and "Conv Layer 1".
2. "Mid level features" (4 by 6 tiles showing parts of faces such as eyes, ears, noses and brow shapes); beneath: "Eyes, ears, nose" and "Conv Layer 2".
3. "High level features" (4 by 6 tiles each showing a whole face); beneath: "Facial structure" and "Conv Layer 3".

The slide shows features becoming more complex with depth.

Footer credit: Lee+ *ICML* 2009.

*Figure: yes — three grids of learned feature visualisations (edges, facial parts, whole faces) for convolutional layers 1 to 3*

## Slide 51 — CNNs for Classification: Feature Learning

![Slide 51 — CNNs for Classification: Feature Learning](../images/03-convolutional-neural-networks/slide-51.jpg)

Blue line-art diagram of a full CNN, left to right. Input: a stack of pages showing a filled blue silhouette of a car (front view), labelled "INPUT". A small patch on the car is joined by lines to a tall box (labelled "CONVOLUTION + RELU"), then to a smaller box ("POOLING"), then a second box ("CONVOLUTION + RELU"), then another ("POOLING"), then "…" and a final small box. Below these, a curly brace spanning input-side stages from "CONVOLUTION + RELU" through the second "POOLING" is labelled "FEATURE LEARNING". The right part of the diagram (flattened column, fully-connected column, and a softmax column with output labels "CAR", "TRUCK", "VAN", "…", "BICYCLE", under the stage labels "FLATTEN", "FULLY CONNECTED", "SOFTMAX", and a brace labelled "CLASSIFICATION") is drawn faded, so the feature-learning part is highlighted.

Text below:
"1. Learn features in input image through **convolution**"
"2. Introduce **non-linearity** through activation function (real-world data is non-linear!)"
"3. Reduce dimensionality and preserve spatial invariance with **pooling**"

*Figure: yes — full CNN diagram with the feature-learning stages highlighted and the classification stages faded*

## Slide 52 — CNNs for Classification: Class Probabilities

![Slide 52 — CNNs for Classification: Class Probabilities](../images/03-convolutional-neural-networks/slide-52.jpg)

Build step: same diagram as slide 51, with the highlighting reversed.

The feature-learning part (input car image, convolution + ReLU and pooling stages, "FEATURE LEARNING") is now faded, and the classification part is highlighted: a flattened column, a fully-connected column and a softmax column with output labels "CAR", "TRUCK", "VAN", "…", "BICYCLE", under the labels "FLATTEN", "FULLY CONNECTED", "SOFTMAX" and the brace "CLASSIFICATION".

Text below:
"- CONV and POOL layers output high-level features of input"
"- Fully connected layer uses these features for classifying input image"
"- Express output as **probability** of image belonging to a particular class"

At right, the formula:

$$\text{softmax}(y_i) = \frac{e^{y_i}}{\sum_j e^{y_j}}$$

*Figure: yes — same CNN diagram as the previous slide with the classification stages highlighted, plus the softmax formula*

## Slide 53 — Putting it all together: CNN in TensorFlow

Dark-background code slide with the TensorFlow logo at top right. The first three lines of the model (the comment, Conv2D and MaxPool2D) are enclosed in a green rounded box.

```python
import tensorflow as tf

def generate_model():
   model = tf.keras.Sequential([
      # first convolutional layer
      tf.keras.layers.Conv2D(32, filter_size=3, activation='relu’),
      tf.keras.layers.MaxPool2D(pool_size=2, strides=2),

      # second convolutional layer
      tf.keras.layers.Conv2D(64, filter_size=3, activation='relu’),
      tf.keras.layers.MaxPool2D(pool_size=2, strides=2),

      # fully connected classifier
      tf.keras.layers.Flatten(),
      tf.keras.layers.Dense(1024, activation='relu’),
      tf.keras.layers.Dense(10, activation=‘softmax’)  # 10 outputs
   ])
   return model
```

Note: as printed, the Conv2D calls use the keyword `filter_size` (the slide's own spelling; slide 47's code uses `kernel_size`), each `'relu’` opens with a straight quote and closes with a typographic one, and `‘softmax’` has typographic quotes at both ends.

At lower right, a small copy of the CNN diagram from slide 51 with the first convolution + ReLU and pooling stages outlined in a green box (the input is outside the box), tying the highlighted code to that part of the network.

*Figure: yes — small CNN diagram with the first convolution and pooling stage outlined, beside the code*

## Slide 54 — Putting it all together: CNN in PyTorch

Dark-background code slide with the PyTorch logo at top right. A green rounded box encloses the first Conv2d, ReLU and MaxPool2d lines and the blank line after them.

```python
import torch

def generate_model():
   model = nn.Sequential([
      # first and second convolutional layer
      torch.nn.Conv2d(in_channels=3,out_channels=32, filter_size=3),
      torch.nn.ReLU(),
      torch.nn.MaxPool2d(kernel_size=2, stride=2),

      torch.nn.Conv2d(in_channels=32, out_channels=64, filter_size=3),
      torch.nn.ReLU(),
      torch.nn.MaxPool2d(kernel_size=2, stride=2),

      # fully connected classifier
      torch.nn.Flatten(),
      torch.nn.Linear(64*6*6, 1024), # flattened dim after 2 conv layers
      torch.nn.ReLU(),
      torch.nn.Linear(1024, 10),  # 10 outputs
   ])
   return model
```

Note: as printed, the code imports only `torch` yet calls `nn.Sequential`, and uses `filter_size` as the keyword (the slide's own spelling). The comment says "first and second convolutional layer" while the box surrounds only the first convolution block.

At lower right, the same small CNN diagram as on slide 53 with the first convolution + ReLU and pooling stages outlined (the input is outside the box).

*Figure: yes — small CNN diagram with the first convolution and pooling stage outlined, beside the code*

## Slide 55 — [Section divider: An Architecture for Many Applications]

Section-divider slide: blue background, centred white title "An Architecture for Many Applications".

*Figure: no*

## Slide 56 — An Architecture for Many Applications

![Slide 56 — An Architecture for Many Applications](../images/03-convolutional-neural-networks/slide-56.jpg)

The CNN diagram from slide 51 (car input, "CONVOLUTION + RELU" and "POOLING" stages twice, "FEATURE LEARNING" brace). Here the classification part (flatten, fully connected, softmax with "CAR", "TRUCK", "VAN", "…", "BICYCLE") is faded and enclosed in a dashed rounded box. A blue arrow leads out of the bottom of that box and points left, towards a centred list of four applications:

"Classification"
"Object detection"
"Segmentation"
"Probabilistic control"

The slide shows that the feature-learning part is kept and the classification head can be swapped for different tasks.

*Figure: yes — CNN diagram with the classification head boxed and faded, an arrow pointing to a list of other applications*

## Slide 57 — Classification: Breast Cancer Screening

![Slide 57 — Classification: Breast Cancer Screening](../images/03-convolutional-neural-networks/slide-57.jpg)

Left: a figure from a Nature article headed "International evaluation of an AI system for breast cancer screening" (with the "nature" logo). Two ROC-style plots, panels labelled "b" and "c". In both, the horizontal axis is "1 – Specificity" (ticks 0, 0.2, 0.4, 0.6, 0.8, 1.0). Only panel b labels its vertical axis, "Sensitivity" (ticks 0 to 1.0 in steps of 0.2); panel c has the same tick marks without numbers or label. Each panel has a legend with two series, "AI" (black) and "MD Readers" (purple).

Panel b, titled "Breast cancer in 2 years (USA)":
- AI (black solid curve, with a dashed black stepped line hugging it): rises steeply near the origin, about 0.55 at 1 – Specificity 0.2, about 0.7 at 0.4, about 0.82 at 0.6, and reaches 1.0 at 1.0. It lies above the purple curve everywhere.
- MD Readers (purple curve with five purple diamond markers): diamonds at roughly (0, 0), (0.01, 0.08), (0.09, 0.21), (0.2, 0.37) and (0.27, 0.44); the curve passes about 0.55 at 0.4 and about 0.68 at 0.6 and reaches 1.0 at 1.0.

Panel c, titled "Breast cancer in 1 year (USA)":
- AI (black solid curve, with a dashed black stepped line): rises very steeply, about 0.8 at 0.2, about 0.9 at 0.4, about 0.95 at 0.6, reaching 1.0 at 1.0.
- MD Readers (purple curve with five diamond markers): diamonds at roughly (0, 0.01), (0.02, 0.16), (0.09, 0.36), (0.2, 0.58) and (0.27, 0.64); the curve is about 0.78 at 0.4 and about 0.9 at 0.6, reaching 1.0 at 1.0. It lies below the AI curve everywhere; the two nearly converge above about 0.8 sensitivity but do not cross.

(All curve values are approximate readings.)

Right: two greyscale mammogram images side by side (two views of a breast), each with a yellow-orange square drawn around a small suspicious region.

Captions: under the plots, "CNN-based system outperformed expert radiologists at detecting breast cancer from mammograms"; under the images, "Breast cancer case missed by radiologist but detected by AI".

Footer credit: McKinney+ *Nature* 2020.

*Figure: yes — two sensitivity versus 1 – specificity plots (AI above MD readers) and two mammograms with boxed regions*

## Slide 58 — Object Detection

![Slide 58 — Object Detection](../images/03-convolutional-neural-networks/slide-58.jpg)

Two rows, each with the same street photograph of a yellow taxi seen from behind (with a pedestrian and a cyclist at left), captioned "Image $x$" (printed as "Image x"). In each row a black arrow leads to a green trapezoid labelled "CNN" (wide at the left, narrowing to the right), then another black arrow to the output.

Top row: output is a white box containing "Taxi", captioned "Class label $y$" (printed as "Class label y").

Bottom row: output is the same photograph with a red bounding box drawn around the taxi, a red tag "taxi" at the box's top-left, a red dot at the box's bottom-left corner labelled "(x,y)", the box's bottom edge labelled "w" and its left edge labelled "h". Caption: "Label (x, y, w, h)".

The slide contrasts predicting one class label for the whole image with predicting a bounding box.

*Figure: yes — two rows with a taxi photo into a CNN, one giving a class label and one giving a labelled bounding box*

## Slide 59 — Object Detection

![Slide 59 — Object Detection](../images/03-convolutional-neural-networks/slide-59.jpg)

Two rows, each a three-step flow from left to right with black arrows between steps. All photographs are the street scene with the yellow taxi.

Top row: "Image $x$" (printed "Image x", the taxi photo) then the same photo with a red box around the taxi and a red "taxi" tag, then a white output box reading "**Output:**" / "taxi: (x1, y1, w1, h1)" (the word "taxi" in red).

Bottom row: "Image $x$", a wider crop of the same street with a truck at left, several pedestrians, a bicycle and traffic cones, and the taxi at right; then the same photo with boxes: a green box with green tag "truck" at the far left, three tall purple boxes around three pedestrians with a purple tag "person", and a red box with red tag "taxi" around the taxi; then a white output box:

"**Output:**"
"taxi: (x1, y1, w1, h1)" (taxi in red)
"person: (x2, y2, w2, h2)" (person in purple)
"person: (x3, y3, w3, h3)" (person in purple)
"…."

The slide shows that detection outputs a class and a box for every object in the image, however many there are.

*Figure: yes — taxi photo with detected boxes and printed outputs, one object in the top row and several objects (truck, persons, taxi) in the bottom row*

## Slide 60 — Naïve Solution to Object Detection

![Slide 60 — Naïve Solution to Object Detection](../images/03-convolutional-neural-networks/slide-60.jpg)

Flow, left to right with black arrows: the street photograph (truck, pedestrians, taxi) then the same photograph covered with a dense overlay of many thin white rectangles of different sizes and positions, then a green trapezoid labelled "CNN", then a white box "Class?".

At lower right, a thinking-face emoji. Below, centred: "**Problem**: Way too many inputs! This results in too many scales, positions, sizes!"

*Figure: yes — photo, the same photo covered by many candidate boxes, CNN and a "Class?" output*

## Slide 61 — Object Detection with R-CNNs

![Slide 61 — Object Detection with R-CNNs](../images/03-convolutional-neural-networks/slide-61.jpg)

Subtitle: "R-CNN algorithm: Find regions that we think have objects. Use CNN to classify."

Diagram in four numbered stages, left to right:
1. "1. Input image": a photograph of a man in a cowboy hat and plaid shirt on a horse.
2. "2. Extract region proposals (~2k)": the same photograph with several yellow rectangles of different sizes (around the man, the horse, a left-hand structure and a small corner).
3. "3. Compute CNN features": three dashed arrows from yellow boxes lead to a small picture labelled "warped region" (a cropped, resized yellow-boxed region of the man), which enters a dashed box containing a stack of squares and a small feature-map pyramid labelled "CNN".
4. "4. Classify regions": from the CNN, dashed arrows lead to three boxes: "aeroplane? no.", "person? yes.", "tvmonitor? no.", with vertical dots between them.

Below, "**Problems:** 1) Slow! Many regions; time intensive inference." / "2) Brittle! Manually defined region proposals."

Footer credit: Girshick+ *CVPR* 2014.

*Figure: yes — the four-stage R-CNN pipeline from input photo to region proposals, CNN features and class labels*

## Slide 62 — Faster R-CNN Learns Region Proposals

![Slide 62 — Faster R-CNN Learns Region Proposals](../images/03-convolutional-neural-networks/slide-62.jpg)

Build step (first stage of a progressive build): a Faster R-CNN diagram begins to appear; only the first block is drawn so far.

Drawn so far: at bottom centre, a flat tilted photograph labelled "image" under a white box (3D block) labelled "conv layers", with a small yellow arrow pointing up from the top of the block. Text labels placed around the empty canvas:
- at left bottom: "Image input directly into convolutional feature extractor" then in bold green "Fast! Only input image once!"
- at upper left: "Feature extraction over proposed regions"
- at upper right: "Classification of regions → object detection"
- at right middle: "Region proposal network to learn candidate regions" then in bold green "Learned, data-driven"

Footer credit: Ren+ *IEEE* 2016.

*Figure: yes — partial Faster R-CNN diagram showing an image and a block of convolutional layers, with text labels for the other stages*

## Slide 63 — Semantic Segmentation: Fully Convolutional Networks

![Slide 63 — Semantic Segmentation: Fully Convolutional Networks](../images/03-convolutional-neural-networks/slide-63.jpg)

Centred text: "FCN: Fully Convolutional Network." / "Network designed with all convolutional layers," / "with **downsampling** and **upsampling** operations"

Diagram, left to right:
- Left: a photograph of a black-and-white cow on grass, labelled "Input: 3 x H x W".
- Centre: an encoder–decoder drawing of blocks. Blocks of decreasing size (grey, with pink-tinted blocks marking downsampling) lead down to a narrow bottleneck, then blocks of increasing size (grey, with blue-tinted blocks marking upsampling). Labels, in order: "High-res: $D_1$ x H/2 x W/2" (below the thin slabs at lower left), "Med-res: $D_2$ x H/4 x W/4" (above the left blocks), "Low-res: $D_3$ x H/4 x W/4" (below the bottleneck), "Med-res: $D_2$ x H/4 x W/4" (above the right blocks), "High-res: $D_1$ x H/2 x W/2" (below the thin slabs at lower right). All printed in the form "D<sub>k</sub> x H/n x W/n".
- Right: a colour segmentation map of the same cow scene (brown cow region, green grass, pink background, blue sky), labelled "Predictions: H x W".

Bottom code chips: TensorFlow logo with `tf.keras.layers.Conv2DTranspose` (left) and PyTorch logo with `torch.nn.ConvTranspose2d` (right).

Footer credit: Long+ *CVPR* 2015.

*Figure: yes — encoder–decoder (fully convolutional) network diagram from a cow photograph to a colour segmentation map, with code chips*

## Slide 64 — Continuous Control: Navigation from Vision

![Slide 64 — Continuous Control: Navigation from Vision](../images/03-convolutional-neural-networks/slide-64.jpg)

Left column, with labels:
- "**Raw Perception** $I$ (ex. camera)": a forward-facing camera image of a residential street seen from low down (a dark helmet or vehicle front at the bottom edge), with a green rectangle drawn on the road ahead.
- "**Coarse Maps** $M$ (ex. GPS)": two small black squares showing a street map as white lines (a grid of roads); in the right square a red line traces a route along some of the roads.
- A black eye icon beneath.

A large blue right-pointing arrow leads to the right column: "**Possible Control Commands**" above the same street photo with three red fan-shaped streaks starting from the vehicle and curving left, straight ahead and right (the candidate paths). A black steering-wheel icon sits beneath.

Footer credit: Amini+ *ICRA* 2019.

*Figure: yes — camera image and coarse route maps as inputs, arrow to the street image with three red candidate-path trajectories, with eye and steering-wheel icons*

## Slide 65 — End-to-End Framework for Autonomous Navigation

![Slide 65 — End-to-End Framework for Autonomous Navigation](../images/03-convolutional-neural-networks/slide-65.jpg)

Subtitle: "Entire model is trained end-to-end **without any human labelling or annotations**"

Network diagram, left to right. Left: four input pictures stacked vertically: three camera images of road scenes, each with a green polygon outline on the road, and a black map image with white road lines. Each feeds a pale-blue box labelled "convolutional" (four boxes), enclosed in a dark-blue frame. Each convolutional box feeds an orange vertical box labelled "flatten"; the four flatten boxes feed a pink vertical box labelled "concatenate" (enclosed in a trapezoid-shaped dark-blue outline together with the flatten boxes). The pink box feeds two green vertical boxes labelled "f.c." in sequence. The second f.c. box feeds:
- upward, a third green "f.c." box, which feeds three purple output boxes labelled $\phi_i$, $\mu_i$ and $\sigma_i$ through arrows annotated with the equations $\phi_i = \frac{e^{a_i}}{\sum_{j=1}^{K} e^{a_j}}$, $\mu_i = a_i$ and $\sigma_i = \exp(a_i)$;
- downward, a second pink "concatenate" box.

A separate branch starts from a small "Routed Map" image (black map with a red route): it goes through a blue "conv" box, an orange "flatten" box, and into the second "concatenate" box, which feeds a green "f.c." box.

Right, inside a green frame: "Probabilistic Control Output", a street image with three red fan-shaped streaks; under it the equation

$$P(\theta | I, M) = \sum_{i=1}^{K} \phi_i \thinspace \mathcal{N}(\mu_i, \sigma_i^2)$$

then "Deterministic Control", a street image with one red curved path, and the caption "Optional output if routed map is provided as input".

Bottom, centred, the loss:

$$L = -\log(P(\theta | I, M)$$

(As printed: the loss closes only one of its two parentheses.)

Footer credit: Amini+ *ICRA* 2019.

*Figure: yes — end-to-end navigation network diagram with convolutional branches, concatenation and fully connected layers giving probabilistic and deterministic control outputs*

## Slide 66 — [Video: autonomous driving demonstration, "Auto ON"]

Full-bleed video still taken from inside a car (a Toyota steering wheel and dashboard visible) with a man in a dark blue sweater in the driver's seat, his hands resting off the wheel, looking out at a wooded road under blue sky. A red circular play button with a white triangle is centred on the frame. At top left a green filled circle with the text "Auto ON" and "Navigation and Localization" in green. At top right a black inset map of white road lines with a red route and a green triangle marking the car's position. At bottom right, in red: "Amini+ ICRA 2019."

Footer credit: Amini+ ICRA 2019. (printed at bottom right, in red, over the video)

*Figure: yes — in-car video still of autonomous driving with a play button and a route-map inset*

## Slide 67 — Deep Learning for Computer Vision: Impact

A collage of overlapping images, no captions except the text inside the images:
- Top left: a dark sedan driving on a dirt road, motion-blurred, with a green pattern overlaid on its body (self-driving car).
- Left centre: a stylised version of the Mona Lisa repainted in swirling blue and yellow brushstrokes (style transfer).
- Top centre: a silver robotic hand reaching toward a wooden block with round and square cut-outs.
- Top right: a pair of lung CT scan slices in black and white, one with a small green circle marking a spot.
- Right: a cover of the journal Nature, reading "nature" / "THE INTERNATIONAL WEEKLY JOURNAL OF SCIENCE" / "LESIONS LEARNT" / "Artificial intelligence powers detection of skin cancer from images", showing a phone screen with a red-boxed skin lesion.
- Bottom left: a colour-coded semantic-segmentation map (orange, blue, red and purple regions) beside a photograph of red tulips and a building with green outlines.
- Bottom centre: a photograph of people sitting on a bench near palm trees, with object-detection boxes and tags "person" (several, magenta), "skateboard" (green) and "dog" (yellow).
- Bottom right: a greyscale portrait of a young man's face covered by a yellow triangular mesh of facial landmarks.

*Figure: yes — collage of vision applications: self-driving car, style transfer, robotics, medical imaging, segmentation, object detection and facial landmark mesh*

## Slide 68 — Deep Learning for Computer Vision: Summary

Three blue header boxes, each with a bullet list and a picture below.

"Foundations":
- "Why computer vision?"
- "Representing images"
- "Convolutions for feature extraction"
Picture: the strong-edge-detect image from slide 41 (black image with white edge lines of the woman in the hat) with the kernel overlay (−1 −2 −1 / 0 0 0 / 1 2 1).

"CNNs":
- "CNN architecture"
- "Application to classification"
- "ImageNet"
Picture: the spatial-arrangement diagram from slide 47 (input slab labelled 32, 32 and 3 feeding a 3D output volume).

"Applications":
- "Segmentation, image captioning, control"
- "Security, medicine, robotics"
Picture: a segmentation map of a cat (yellow) on green grass with a pink and blue background.

*Figure: yes — three small pictures (edge-detection kernel result, CNN output volume, segmentation map) under the three summary columns*

## Slide 69 — [Lab 2: Facial Detection Systems]

Black slide. At left a blurred, averaged face image (a smiling man, soft focus). Text at right, centred:

"MIT 6.S191"
"Introduction to Deep Learning"
"Lab 2: Facial Detection Systems"

"Link to download labs:"
"introtodeeplearning.com#schedule" (red underlined link)
"github.com/MITDeepLearning/introtodeeplearning" (red underlined link)

"1. Open the lab in Google Colab"
"2. Start executing code blocks and filling in the #TODOs"
"3. Need help? Come to 32-123!"

*Figure: yes — blurred average face photograph at left (decorative lab slide)*

## Slide 70 — Announcements and Reminders

Black slide with the same blurred averaged face at left. Text at right, centred:

"Introduction to Deep Learning"
"Announcements and Reminders"

"Lecture 4: Generative Modeling starting soon!"

"Lab 2 begins today!"
"Prizes for participants!"
"Enter for a chance to win" followed by three dollar signs and "!"

"Lots of swag will be available after class tomorrow!"

"Interested in cutting-edge AI jobs?"
"introtodeeplearning.com/jobs.html" (red underlined link)

*Figure: yes — blurred average face photograph at left (decorative)*
