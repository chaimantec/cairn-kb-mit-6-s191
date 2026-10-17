---
title: Lecture 4 — Deep Generative Modeling (slide deck)
lecture: 4
slides: 84
source_pdf: https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L4.pdf
note: Slide N = PDF page N (N = 1..84). The deck prints no slide numbers; the "1/6/26" in each footer is the lecture date (6 January 2026).
---

# Lecture 4 — Deep Generative Modeling: slide-by-slide

Text and figures of all 84 slides of
[`6S191_MIT_DeepLearning_L4.pdf`](https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L4.pdf)
(MIT 6.S191 Introduction to Deep Learning, 2026 edition; lecturer Ava Amini), transcribed from the
deck. Cite these as "slide N", where N is the PDF page number. Diagrams, photographs, plots and
equations are described in prose or reproduced, since the KB is read as text.

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

39 slides carry their page image under the heading: 2, 5–10, 15–17, 22, 26, 27, 29–32, 34–37,
39–41, 49, 50, 55, 57, 60, 62, 64, 68, 70, 72, 74, 76–79 — every slide with a distinct figure. The rest
are the title, text-only slides, section dividers, build steps contained in an included slide (among
them most steps of the GAN number-line sequence, 51–68, whose states are described in prose), repeats
of an included figure (11, 20, 33, 38, 42, 69, 73, 81), the VAE summary build (43–47), a video still
(80), the diffusion teaser (82) and the lab and announcement slides. Use only an image path that
appears below; slides without one have no image.

## Contents

| Slides | Section |
| ------ | ------- |
| 1 | Title: "Deep Generative Modeling" |
| 2–8 | "Which face is real?"; supervised versus unsupervised learning; generative modeling as density estimation and sample generation; why generative models: debiasing, outlier detection, sample generation |
| 9–11 | Latent variable models (autoencoders and VAEs; GANs); what a latent variable is: the Myth of the Cave |
| 12–18 | Autoencoders: the encoder, the decoder and the reconstruction loss; latent dimensionality versus reconstruction quality; autoencoders for representation learning |
| 19–22 | Variational autoencoders: the key difference from a traditional autoencoder (mean and standard deviation vectors) |
| 23–32 | VAE optimization: reconstruction loss plus regularization term; priors on the latent distribution and the KL divergence; intuition on regularization and the Normal prior (continuity and completeness) |
| 33–38 | The VAE computation graph; reparametrizing the sampling layer; sampling to generate |
| 39–47 | Latent perturbation; disentanglement and β-VAEs; debiasing; VAE summary |
| 48–50 | Generative adversarial networks: sampling without modelling density; generator and discriminator |
| 51–68 | Intuition behind GANs: generator and discriminator on a one-dimensional number line, turn by turn |
| 69–73 | Training GANs: the discriminator's and generator's objectives, the min-max loss; generating new data |
| 74–80 | GANs as distribution transformers and latent interpolation; distribution transformations; CycleGAN (horse to zebra, speech, a synthesized-speech video) |
| 81–82 | Summary; diffusion models, "more to come in Lectures 6 and 7" |
| 83–84 | Lab 2 (facial detection systems); announcements |

## Slide 1 — Deep Generative Modeling

Title slide. Black background; at left a glowing blue network of nodes and lines (a mesh of connected points). A faint large diagonal watermark "MIT 6.S191" sits behind the text. Text, centred at right:

"Deep Generative Modeling"
"Ava Amini"
"MIT Introduction to Deep Learning"
"January 6, 2026"

The MIT logo is at bottom centre-left and an "MIT EECS" logo at bottom right.

*Figure: no*

## Slide 2 — Which face is real?

![Slide 2 — Which face is real?](../images/04-deep-generative-modeling/slide-2.jpg)

Text: "Which face is real?". Below it, three colour photographs side by side, each labelled underneath with a large letter: "A", "B", "C".

- A: a smiling young girl with long braided hair and a striped top, outdoors against a blurred green background with yellow flowers.
- B: an older man with grey hair and a lined face, neutral expression, wearing a grey sweater over a collared shirt, in front of a blurred shelf.
- C: a smiling older woman with shoulder-length brown hair, looking to the side, wearing a knitted beige sweater, in front of a blurred window, plants and bookshelf.

Footer credit: Google Gemini

*Figure: yes — three portrait photographs of faces labelled A, B and C*

## Slide 3 — Supervised vs unsupervised learning

Two columns separated by a vertical black line. The left column is in full black text; the right column is greyed out (faded).

Left column, "Supervised Learning":
"Data: $(x, y)$", and beneath it, $x$ is data, $y$ is label
"Goal: Learn function to map $x \rightarrow y$"
"Examples: Classification, regression, object detection, semantic segmentation, etc."

Right column (greyed), "Unsupervised Learning":
"Data: $x$", and beneath it, $x$ is data, no labels!
"Goal: Learn some *hidden* or *underlying structure* of the data"
"Examples: Clustering, feature or dimensionality reduction, etc."

*Figure: no*

## Slide 4 — Supervised vs unsupervised learning

Build step: the right column of slide 3 is no longer greyed out; both columns are now in full black text. Right column wording changes slightly: "the" replaces "some" in the goal.

Left column, "Supervised Learning":
"Data: $(x, y)$", and beneath it, $x$ is data, $y$ is label
"Goal: Learn function to map $x \rightarrow y$"
"Examples: Classification, regression, object detection, semantic segmentation, etc."

Right column, "Unsupervised Learning":
"Data: $x$", and beneath it, $x$ is data, no labels!
"Goal: Learn the *hidden* or *underlying structure* of the data"
"Examples: Clustering, feature or dimensionality reduction, etc."

*Figure: no*

## Slide 5 — Generative modeling

![Slide 5 — Generative modeling](../images/04-deep-generative-modeling/slide-5.jpg)

Text: "Goal: Take as input training samples from some distribution and learn a model that represents that distribution". Two labelled halves below.

Left half, "Density Estimation": a single blue curve over a horizontal row of translucent blue dots labelled "samples" at the left. The curve has a small bump at left and a much taller peak right of centre, with a dip between them, and flattens at low values at both ends. The dots lie in a row under the curve: a tight cluster under the small bump, a gap, then a long dense cluster under the tall peak, and one isolated dot at the far right. The figure shows a probability density fitted to one-dimensional samples, with high density where the samples are dense.

Right half, "Sample Generation": two 2 by 2 grids of small colour photographs. The left grid is captioned "Input samples" and "Training data $\sim P_{data}(x)$": a cup of coffee on a saucer, a brown mushroom, an interior scene with a standing person, a butterfly with eyespots on its wings. The right grid is captioned "Generated samples" and "Generated $\sim P_{model}(x)$": a cat lying down, a white teapot with flowers, a person swimming in water, a domed building against an orange sky.

Bottom text: "How can we learn $P_{model}(x)$ similar to $P_{data}(x)$?"

*Figure: yes — density curve over 1D samples, and grids of input photographs versus generated photographs*

## Slide 6 — Why generative models? Debiasing

![Slide 6 — Why generative models? Debiasing](../images/04-deep-generative-modeling/slide-6.jpg)

Text: "Capable of uncovering **underlying features** in a dataset".

Two grids of small face photographs (6 rows by 10 columns each) separated by "vs". The left grid shows faces that look alike in framing and are mostly light-skinned, frontal and smiling, captioned "Homogeneous skin color, pose". The right grid shows faces that vary widely in skin tone, head pose, lighting, and accessories such as sunglasses and hats, captioned "Diverse skin color, pose, illumination".

Bottom text: "How can we use this information to create fair and representative datasets?"

At bottom right, a gold star with the bold label "Software Lab!".

Footer credit: Amini/Soleimany+ *AAAI/AIES* 2019.

*Figure: yes — two grids of face photographs, one homogeneous and one diverse, contrasted by "vs"*

## Slide 7 — Why generative models? Outlier detection

![Slide 7 — Why generative models? Outlier detection](../images/04-deep-generative-modeling/slide-7.jpg)

Bullets at upper left:
"• **Problem:** How can we detect when we encounter something new or rare?"
"• **Strategy:** Leverage generative models, detect outliers in the distribution"
"• Use outliers during training to improve even more!"

At lower left, a dark blue bell-shaped curve (one peak slightly left of centre, long flat tails). A green dot sits on the peak and a green line runs right from it, then up, ending in an arrow pointing at a photograph at upper right. The photograph is headed "95% of Driving Data:" / "(1) sunny, (2) highway, (3) straight road" and shows a dashboard-view of a sunny multi-lane highway with a few distant cars. A red dot sits on the flat right tail of the curve, with a red line running right then up to an arrow pointing at three photographs at the bottom right, headed by the text "Detect outliers to avoid unpredictable behavior when training". The three photographs, captioned below: "Edge Cases" (a road scene with an aeroplane in the air close to the road), "Harsh Weather" (a road in heavy rain or spray), "Pedestrians" (people at a crossing, one in an orange top, close to the camera). The figure shows common data at the peak of the distribution and rare data in the tail.

Footer credit: Amini+ *IROS* 2018.

*Figure: yes — density curve with the peak linked to a typical highway photo and the tail linked to rare-case photos*

## Slide 8 — Why generative models? Sample generation

![Slide 8 — Why generative models? Sample generation](../images/04-deep-generative-modeling/slide-8.jpg)

Bullets at left:
"• **Generative models learn probability distributions**"
"• **Sampling** from that distribution → new data instances"
"• **Backbone of Generative AI:** generate language, images, and more"

At lower left, the same density-estimation picture as slide 5: a blue curve with a small bump at left and a tall peak right of centre, above a row of translucent blue dots labelled "samples" (a cluster under the small bump, a long dense cluster under the peak, one isolated dot at the right).

At right, three rows with bold labels at the far right:

- "Natural Language", with a gold star and the text "6.S191 Guest Lectures!": a dark screenshot headed "ChatGPT" with three columns, "Examples" (with the sample text ""Explain quantum computing in simple terms" →"), "Capabilities" ("Remembers what user said earlier in the conversation") and "Limitations" ("May occasionally generate incorrect information").
- "Images & Videos": three painting-style images side by side: a fox sitting in a colourful meadow, a white bird with a long curved beak among plants by water, and a spotted cat-like animal with pale fur on snow facing the viewer.
- "Molecules", with a gold star and the text "6.S191 Guest Lecture!": three purple ribbon diagrams of folded molecular structures (helices and sheets).

*Figure: yes — density curve with samples, and example generated outputs for language, images and molecules*

## Slide 9 — Latent variable models

![Slide 9 — Latent variable models](../images/04-deep-generative-modeling/slide-9.jpg)

Blue background, white text and a faint "MIT 6.S191" watermark. Title "Latent variable models". Two rounded white-outlined boxes side by side.

Left box: "Autoencoders and Variational Autoencoders (VAEs)". Its diagram, left to right: a tall pale-blue rectangle, a green trapezoid narrowing to the right, a small pink-orange square, a purple trapezoid widening to the right, and a tall periwinkle-blue rectangle. It is an hourglass: input, encoder narrowing to a small bottleneck, decoder widening to an output.

Right box: "Generative Adversarial Networks (GANs)". Its diagram: at lower left a small pink-orange square, then a purple trapezoid widening to the right, then a tall periwinkle-blue rectangle. Above that rectangle is a second tall pale-blue rectangle. White curved lines run from both rectangles into a green trapezoid narrowing to the right, which ends in a small yellow circle. So a generator (noise square into purple trapezoid) produces an output that, together with a real-data rectangle, feeds a discriminator (green trapezoid) that outputs a single value.

*Figure: yes — schematic block diagrams of an autoencoder and of a GAN*

## Slide 10 — What is a latent variable?

![Slide 10 — What is a latent variable?](../images/04-deep-generative-modeling/slide-10.jpg)

A full-width illustration, captioned at lower right in bold italics "Myth of the Cave", of a cutaway cave. On the left cave wall are dark shadow shapes: a vase, a rearing horse, a ring, and a bird-like shape. A seated figure sits at the lower left facing the wall. In the middle, a row of robed figures stand behind a low brick wall, holding up poles topped with a vase, a horse, a ring and a bird. To the right a fire burns on a rocky ledge, and at the upper right a figure climbs towards the cave's opening at the top, with grass above. The figure shows shadows on a wall cast by objects the viewer in the cave cannot see directly.

Footer credit: Plato, *Republic.*

*Figure: yes — illustration of the Myth of the Cave with shadows on the wall, carried objects, a fire and an exit*

## Slide 11 — What is a latent variable?

Build step: adds a line of text under the illustration of slide 10 (the caption "Myth of the Cave" is no longer shown).

Same cave illustration as slide 10. Text below: "Can we learn the **true explanatory factors**, e.g. latent variables, from only observed data?"

Footer credit: Plato, *Republic.*

*Figure: yes — illustration of the Myth of the Cave (same as slide 10)*

## Slide 12 — Autoencoders

Section-title slide. Blue background with a faint "MIT 6.S191" watermark; centred white text "Autoencoders".

*Figure: no*

## Slide 13 — Autoencoders: background

Text: "Unsupervised approach for learning a **lower-dimensional** feature representation from unlabeled training data".

Diagram, left to right: a small black-and-white image of a handwritten digit in a thin grey frame (a handwritten "2"), then a tall pale-blue rounded rectangle labelled $x$, then three green rounded rectangles of decreasing height (about 220, 150 and 100 pixels tall), then a small pink rounded rectangle labelled $z$. It shows an encoder network narrowing from the input $x$ to a small latent vector $z$.

At right, the text "Why do we care about a low-dimensional $z$?" next to a thinking-face emoji.

Bottom text: "“Encoder” learns mapping from the data, $x$, to a low-dimensional latent space, $z$"

*Figure: yes — encoder diagram from a handwritten digit image through narrowing layers to a small latent block z*

## Slide 14 — Autoencoders: background

Build step: extends slide 13 with the decoder half and a reconstructed image; the encoder text is replaced.

Text: "How can we learn this latent space?" / "Train the model to use these features to **reconstruct the original data**".

Diagram, left to right: the handwritten "2" image in a black frame; a tall pale-blue rectangle labelled $x$; three green rectangles of decreasing height; a small pink rectangle labelled $z$; three purple rectangles of increasing height; a tall blue-violet rectangle labelled $\hat{x}$; then a blurry, smudged version of the same "2" in a black frame. The shape is symmetric, an hourglass narrowing to $z$ and widening back.

Bottom text: "“Decoder” learns mapping back from latent space, $z$, to a reconstructed observation, $\hat{x}$"

*Figure: yes — full autoencoder diagram from the input digit through the latent block z to a blurred reconstruction*

## Slide 15 — Autoencoders: background

![Slide 15 — Autoencoders: background](../images/04-deep-generative-modeling/slide-15.jpg)

Build step: adds a loss arrow and the loss function to slide 14; the bottom decoder text is replaced.

Same text and diagram as slide 14. Now a black line runs from the bottom of the input image frame down, across to the right beneath the network, and up with an arrowhead to the bottom of the reconstructed image frame, linking the input and its reconstruction. Beneath the line:

$$\mathcal{L}(x, \hat{x}) = \Vert x - \hat{x} \Vert^2$$

and at right the text "Loss function doesn't use any labels!!"

*Figure: yes — autoencoder diagram with a loss arrow connecting the input image to its reconstruction*

## Slide 16 — Autoencoders: background

![Slide 16 — Autoencoders: background](../images/04-deep-generative-modeling/slide-16.jpg)

Build step: replaces the stacks of rectangles of slide 15 with two trapezoids.

Same text, loss arrow, equation and images as slide 15:

$$\mathcal{L}(x, \hat{x}) = \Vert x - \hat{x} \Vert^2$$

"Loss function doesn't use any labels!!" Text above: "How can we learn this latent space?" / "Train the model to use these features to **reconstruct the original data**".

The diagram is now: the handwritten "2" image; the pale-blue rectangle $x$; one large green trapezoid tall at the left and narrowing to the right; the small pink rectangle $z$; one large purple trapezoid narrow at the left and widening to the right; the blue-violet rectangle $\hat{x}$; and the blurry reconstructed "2". The black loss arrow runs under the network from the input image to the reconstructed image, as on slide 15. The slide shows the encoder (green) and decoder (purple) as funnel shapes either side of $z$.

*Figure: yes — autoencoder diagram with encoder and decoder drawn as trapezoids, plus the loss arrow*

## Slide 17 — Dimensionality of latent space → reconstruction quality

![Slide 17 — Dimensionality of latent space → reconstruction quality](../images/04-deep-generative-modeling/slide-17.jpg)

Text: "Autoencoding is a form of compression!" / "Smaller latent space will force a larger training bottleneck". The title prints an arrow character between "space" and "reconstruction".

Three panels side by side, each a 10 by 10 grid of white handwritten digits on black, with captions above: "2D latent space", "5D latent space", "Ground Truth". The three grids show the same 100 digits in the same positions. The first row of the Ground Truth grid reads 7 2 1 0 4 1 4 9 5 9 and the last row 3 6 9 3 1 4 1 7 6 9.

- "2D latent space": the digits are blurry and smudged; many are hard to tell apart and some are visibly different digits from the ground truth.
- "5D latent space": the digits are much sharper and mostly match the ground truth, with a few distorted ones.
- "Ground Truth": the original crisp digits.

The panels show that reconstructions improve as the latent dimension grows.

*Figure: yes — three grids of handwritten digits: blurry 2D-latent reconstructions, sharper 5D-latent reconstructions, and the originals*

## Slide 18 — Autoencoders for representation learning

Three text blocks:

"**Bottleneck hidden layer** forces network to learn a compressed latent representation"

"**Reconstruction loss** forces the latent representation to capture (or encode) as much “information” about the data as possible"

"**Autoencoding** = **Auto**matically **encoding** data; “Auto” = **self**-encoding"

*Figure: no*

## Slide 19 — Variational Autoencoders (VAEs)

Section-title slide. Blue background with a faint "MIT 6.S191" watermark; centred white text "Variational Autoencoders (VAEs)".

*Figure: no*

## Slide 20 — Traditional autoencoders

Diagram, left to right: the handwritten "2" image in a black frame; a tall pale-blue rectangle labelled $x$; a green trapezoid narrowing to the right; a small pink rectangle labelled $z$; a purple trapezoid widening to the right; a tall blue-violet rectangle labelled $\hat{x}$; the blurry reconstructed "2" in a black frame. There is no loss arrow or other text. It is the deterministic autoencoder, with a single latent block $z$.

*Figure: yes — traditional autoencoder diagram with a single latent block z*

## Slide 21 — VAEs: key difference with traditional autoencoder

Same diagram as slide 20, except that the single latent block $z$ is replaced by two stacked light-yellow rounded rectangles, labelled $\mu$ (upper) and $\sigma$ (lower), placed at the narrow end of the green trapezoid. Short orange arrows run from each of $\mu$ and $\sigma$ into the pink block $z$, which sits just to their right and feeds the purple decoder trapezoid. The rest is as before: the "2" image, $x$, the green encoder, the purple decoder, $\hat{x}$ and the blurred reconstruction.

Footer credit: Kingma+ *ICLR* 2014.

*Figure: yes — VAE diagram where the encoder outputs mu and sigma blocks that feed z*

## Slide 22 — VAEs: key difference with traditional autoencoder

![Slide 22 — VAEs: key difference with traditional autoencoder](../images/04-deep-generative-modeling/slide-22.jpg)

Build step: adds labels and text to slide 21.

Same diagram as slide 21. New labels: above the $\mu$ block, "mean vector" with a black arrow pointing down to it; below the $\sigma$ block, "standard deviation vector" with a black arrow pointing up to it. Bottom text, bold: "Variational autoencoders are a probabilistic twist on autoencoders!" and in regular weight: "Sample from the mean and standard deviation to compute latent sample".

Footer credit: Kingma+ *ICLR* 2014.

*Figure: yes — VAE diagram with mean vector and standard deviation vector labels*

## Slide 23 — VAE optimization

Same VAE diagram as slide 21 (without the "mean vector" and "standard deviation vector" labels). Two black curly braces are drawn under it. The left brace spans from the input $x$ rectangle to the $\mu$ and $\sigma$ blocks, with the text "Encoder computes: $q_{\phi}(\mathrm{z} \vert x)$". The right brace spans from $z$ to the $\hat{x}$ rectangle, with the text "Decoder computes: $p_{\theta}(\mathrm{x} \vert z)$".

Note on the printed notation: in $q_{\phi}(\mathrm{z} \vert x)$ the $z$ is printed upright (not italic) and $x$ is italic; in $p_{\theta}(\mathrm{x} \vert z)$ the $x$ is upright and $z$ is italic.

Footer credit: Kingma+ *ICLR* 2014.

*Figure: yes — VAE diagram with braces marking the encoder q(z|x) and decoder p(x|z)*

## Slide 24 — VAE optimization

Build step: adds the loss equation to slide 23; the encoder and decoder expressions are set in a smaller size.

Same VAE diagram and braces as slide 23 ("Encoder computes: $q_{\phi}(\mathrm{z} \vert x)$", "Decoder computes: $p_{\theta}(\mathrm{x} \vert z)$"; same upright-versus-italic $z$ and $x$ as noted on slide 23). New line at the bottom:

$$\mathcal{L}(\phi, \theta, x) = \text{(reconstruction loss)} + \text{(regularization term)}$$

Footer credit: Kingma+ *ICLR* 2014.

*Figure: yes — VAE diagram with encoder and decoder braces, above the two-term loss*

## Slide 25 — VAE optimization

Build step: highlights the parameters $\phi$ and $\theta$ on slide 24.

Same as slide 24, but $\phi$ is highlighted with a green background and $\theta$ with a purple background in the loss $\mathcal{L}(\phi, \theta, x)$, and the subscript $\phi$ in $q_{\phi}(\mathrm{z} \vert x)$ is highlighted green and the subscript $\theta$ in $p_{\theta}(\mathrm{x} \vert z)$ purple. The colours match the green encoder and purple decoder in the diagram. The equation reads:

$$\mathcal{L}(\phi, \theta, x) = \text{(reconstruction loss)} + \text{(regularization term)}$$

Footer credit: Kingma+ *ICLR* 2014.

*Figure: yes — VAE diagram with parameters phi (green) and theta (purple) highlighted in the loss and the encoder and decoder expressions*

## Slide 26 — VAE optimization

![Slide 26 — VAE optimization](../images/04-deep-generative-modeling/slide-26.jpg)

Build step: adds a red loss arrow and a red box around the reconstruction term on slide 25.

Same as slide 25. A red line runs from the top of the input "2" image up, across the top of the slide, and down with an arrowhead onto the top of the reconstructed image. Under the horizontal part, in red: "e.g. log-likelihood, $\Vert x - \hat{x} \Vert^2$". In the bottom equation, "(reconstruction loss)" is enclosed in a red rectangle:

$$\mathcal{L}(\phi, \theta, x) = \text{(reconstruction loss)} + \text{(regularization term)}$$

Footer credit: Kingma+ *ICLR* 2014.

*Figure: yes — VAE diagram with a red arrow from input to reconstruction labelled as the reconstruction loss*

## Slide 27 — VAE optimization

![Slide 27 — VAE optimization](../images/04-deep-generative-modeling/slide-27.jpg)

Build step: replaces the red loss arrow of slide 26 with a red regularization expression and moves the red box to the regularization term.

Same as slide 25, with the parameter highlights. Above the $\mu$ and $\sigma$ blocks, in red, two labels with arrows pointing down: "Inferred latent distribution" pointing at the first argument and "Fixed prior on latent distribution" pointing at the second argument of the expression

$$D\left(q_{\phi}(\mathrm{z} \vert x) \Vert p(z)\right)$$

At the bottom, "(regularization term)" is now enclosed in a red rectangle:

$$\mathcal{L}(\phi, \theta, x) = \text{(reconstruction loss)} + \text{(regularization term)}$$

Footer credit: Kingma+ *ICLR* 2014.

*Figure: yes — VAE diagram with the regularization expression D(q(z|x) || p(z)) and labels for the two distributions*

## Slide 28 — Priors on the latent distribution

Top, the expression

$$D\left(q_{\phi}(\mathrm{z} \vert x) \Vert p(z)\right)$$

with two labels beneath it joined to it by black elbow arrows: "Inferred latent distribution" pointing at $q_{\phi}(\mathrm{z} \vert x)$ and "Fixed prior on latent distribution" pointing at $p(z)$.

Lower right, bold: "Common choice of prior – Normal Gaussian:" followed by

$$p(z) = \mathcal{N}(\mu = 0, \sigma^2 = 1)$$

and two bullets:
"• Encourages encodings to distribute encodings evenly around the center of the latent space"
"• Penalize the network when it tries to “cheat” by clustering points in specific regions (i.e., by memorizing the data)"

Lower left, a two-dimensional scatter plot on a light lavender background with white grid lines: thousands of small pastel-coloured dots in a single roughly circular cloud, densest at the centre and thinning towards the edge, with the twelve colours thoroughly mixed rather than grouped. To its right is a vertical colour bar of 12 colour blocks, bottom to top: teal, pale yellow, lavender, coral red, blue, orange, lime green, pink, grey, purple, pale mint green, yellow. Both axes are labelled from −4 to 4 in steps of 1 (tiny tick labels, readable in an enlarged crop); the cloud is centred near (0, 0) and extends to roughly ±3 on both axes. The colour bar has one tiny tick label per block, 0 at the bottom (teal); the higher labels are too small to resolve, but are consistent with 0 to 11. The figure shows latent encodings spread evenly around the origin with no per-colour clusters.

Footer credit: Kingma+ *ICLR* 2014.

*Figure: yes — expression with labels, and a scatter plot of one mixed round cloud of colour-coded latent points*


## Slide 29 — Priors on the latent distribution

![Slide 29 — Priors on the latent distribution](../images/04-deep-generative-modeling/slide-29.jpg)

Build step: adds the KL-divergence expansion and its label to slide 28.

Top equation (as slide 28):

$$D\left(q_{\phi}(\mathrm{z}|x) \Vert p(z)\right)$$

followed on a new line by

$$= -\frac{1}{2}\sum_{j=0}^{k-1}\left(\sigma_j + \mu_j^2 - 1 - \log \sigma_j\right)$$

A red arrow points from the right-hand label to this expansion. Red label at right: "**KL-divergence** between the two distributions". (The annotations "Inferred latent distribution" and "Fixed prior on latent distribution" and their arrows from slide 28 are no longer shown.)

Bold text: "Common choice of prior – Normal Gaussian:"

$$p(z) = \mathcal{N}(\mu = 0, \sigma^2 = 1)$$

Bullets:
- "Encourages encodings to distribute encodings evenly around the center of the latent space"
- "Penalize the network when it tries to "cheat" by clustering points in specific regions (i.e., by memorizing the data)"

At lower left, the scatter plot of slide 28: several thousand small dots on a light lavender background with white grid lines, both axes labelled −4 to 4. The dots, in the twelve pastel colours of the vertical colour bar at its right (bottom to top: teal, pale yellow, lavender, coral red, blue, orange, lime green, pink, grey, purple, pale mint green, yellow; 0 at the bottom), are heavily mixed and form one round, roughly circular cloud centred on the middle of the plot with no separate colour clusters. It illustrates encodings spread evenly around the centre of the latent space.

Footer credit: Kingma+ *ICLR* 2014.

*Figure: yes — scatter plot of multicoloured latent encodings forming one mixed round cloud around the centre*

## Slide 30 — Intuition on regularization and the Normal prior

![Slide 30 — Intuition on regularization and the Normal prior](../images/04-deep-generative-modeling/slide-30.jpg)

Subtitle: "What properties do we want to achieve from regularization?" followed by a thinking-face emoji.

1. "**Continuity:** points that are close in latent space → similar content after decoding"
2. "**Completeness:** sampling from latent space → "meaningful" content after decoding"

Two rounded square panels side by side, each a 2D latent space containing small coloured dots linked by faint dashed grey lines to outline shapes (a blue circle, an orange/red triangle, a purple scribble, a yellow-green square). Captions below: "Not regularized" (left panel) and "Regularized" (right panel).

Left panel (not regularized): a blue circle outline at upper left with a blue dot below it; an orange triangle outline at top with an orange dot below it; a purple dot at the centre with a dashed line to a purple scribbled loop shape at right; a yellow-green square outline at bottom left and a red triangle outline at bottom. A black circled pair of dots (a yellow-green dot and a red dot, close together) at the lower left. Red annotations: "Point in latent space not meaningfully decoded" with a black arrow pointing to the purple dot, and "Close in latent space, but not similarly decoded" with a black line to the circled pair of dots (whose shapes, a square and a triangle, are different).

Right panel (regularized): a blue circle outline at upper left with a blue dot; a red/orange triangle outline at top; a black circled pair of dots (red and orange, close together) near the top centre, dashed lines linking them to the triangles at top and at right (an orange triangle outline); a beige dot with a beige rounded-triangle outline at the right; a yellow-green dot and a yellow-green square outline at bottom left. A black line runs from the circled pair down to green text: "Points close in latent space, similarly and meaningfully decoded".

The figure contrasts a latent space where close points decode to different or meaningless content with a regularized one where close points decode to similar, meaningful content.

Footer credit: Joseph Rocca.

*Figure: yes — two latent-space diagrams, not regularized versus regularized, showing points linked to decoded shapes*

## Slide 31 — Intuition on regularization and the Normal prior

![Slide 31 — Intuition on regularization and the Normal prior](../images/04-deep-generative-modeling/slide-31.jpg)

Build step: a frame captured mid-transition. A not-regularized panel, with text that no other page of the deck shows in full, is fading out at left; the regularized case is fully visible at right.

Same numbered list as slide 30:

1. "**Continuity**: points that are close in latent space → similar content after decoding"
2. "**Completeness:** sampling from latent space → "meaningful" content after decoding"

Faded, barely visible text and shapes at left (a washed-out version of the not-regularized panel): "Encoding as a distribution does not guarantee these properties!", "Small variances → Pointed distributions", "Different means → Discontinuities", and the caption "Not regularized", with faint blurry orange, blue and yellow-green blobs and faint outlines of a triangle, a square, a scribble and a circle.

Fully visible at right: heading "Normal prior → continuity + completeness". Below it, three large soft blurry blobs (Gaussian-like clouds) that overlap in the middle: orange at top, blue at lower left, yellow-green at lower right. Each blob has a faint dashed grey line from its centre to an outline shape: orange blob to an orange triangle at upper left; blue blob to a blue circle at lower left; yellow-green blob to a yellow-green square at lower right. A further dashed line from the point where the three blobs meet leads to a beige rounded-triangle outline at upper right. Green bold text at right: "Center means Regularize variances". Caption below in bold: "Regularized".

Footer credit: Joseph Rocca.

*Figure: yes — three overlapping Gaussian blobs in latent space linked to decoded shapes, with the not-regularized panel fading out at left*

## Slide 32 — Intuition on regularization and the Normal prior

![Slide 32 — Intuition on regularization and the Normal prior](../images/04-deep-generative-modeling/slide-32.jpg)

Same numbered list as slide 30:

1. "**Continuity**: points that are close in latent space → similar content after decoding"
2. "**Completeness:** sampling from latent space → "meaningful" content after decoding"

Figure: the three overlapping blurry blobs of slide 31 (orange at top, blue at lower left, yellow-green at lower right), now larger and centred. Dashed grey lines run from points in the blobs to outline shapes arranged around them: at left, from the orange blob to an orange triangle and to an orange rounded triangle; from the boundary between orange and blue to a grey rounded triangle; from the blue blob to a light-blue rounded triangle and to a blue circle; at right, from the orange area to an orange trapezoid; from the yellow-green blob to a yellow square at lower right; from the meeting point of the blobs a line up to a beige rounded-triangle outline at top right and another line down to a green rounded square at the bottom. The shapes change gradually from triangle to circle as the position moves from the orange blob to the blue blob.

Bottom text: "Regularization with Normal prior helps enforce **continuity & completeness** in the latent space."

Footer credit: Joseph Rocca.

*Figure: yes — overlapping Gaussian blobs in latent space with dashed lines to gradually changing decoded shapes*

## Slide 33 — VAE computation graph

Diagram, left to right: a black-framed pixelated image of a handwritten digit (a "2") at left; a tall light-blue rounded bar labelled $x$; a green trapezoid narrowing to the right (the encoder); two small yellow rounded boxes stacked vertically, the upper labelled $\mu$ and the lower $\sigma$; orange arrows from each of these two boxes pointing to a salmon-red rounded box labelled $z$; a purple trapezoid widening to the right (the decoder); a tall blue-violet rounded bar labelled $\hat{x}$; and a black-framed blurry grey image of a digit "2" at right.

A black curly bracket beneath the left half (from the $x$ bar to the $\mu$ and $\sigma$ boxes) is labelled "Encoder computes: $q_{\phi}(\mathrm{z}|x)$". A bracket beneath the right half (from $z$ to the $\hat{x}$ bar) is labelled "Decoder computes: $p_{\theta}(\mathrm{x}|z)$".

Bottom equation:

$$\mathcal{L}(\phi, \theta, x) = (\text{reconstruction loss}) + (\text{regularization term})$$

Footer credit: Kingma+ *ICLR* 2014.

*Figure: yes — VAE diagram: input digit, encoder, mean and standard deviation boxes, sampled z, decoder, blurry reconstruction*

## Slide 34 — VAE computation graph

![Slide 34 — VAE computation graph](../images/04-deep-generative-modeling/slide-34.jpg)

Build step: adds a red problem statement above the diagram and outlines $z$ in black on slide 33.

Red text at top: "**Problem:** We cannot backpropagate gradients through sampling layers!" ("Problem:" is bold.)

The diagram and all labels are as slide 33, except that the salmon-red box $z$ now has a thick black outline (the sampling step). The bottom equation is unchanged:

$$\mathcal{L}(\phi, \theta, x) = (\text{reconstruction loss}) + (\text{regularization term})$$

Footer credit: Kingma+ *ICLR* 2014.

*Figure: yes — VAE diagram with the sampling node z outlined in black*

## Slide 35 — Reparametrizing the sampling layer

![Slide 35 — Reparametrizing the sampling layer](../images/04-deep-generative-modeling/slide-35.jpg)

At left, a cropped version of the VAE diagram: the green encoder trapezoid, the yellow boxes $\mu$ (upper) and $\sigma$ (lower) with orange arrows into the salmon-red box $z$ (outlined in black), and the purple decoder trapezoid.

At right, bold "Key Idea:" and below it the equation

$$z \sim \mathcal{N}(\mu, \sigma^2)$$

struck through by a red dashed horizontal line. Then the text:

"Consider the sampled latent vector $z$ as a sum of"
- "a fixed $\mu$ vector," ("a fixed $\mu$ vector," highlighted in yellow)
- "and fixed $\sigma$ vector, scaled by random constants drawn from the prior distribution" ("and fixed $\sigma$ vector," highlighted in yellow; "random constants" highlighted in light blue)

$$\Rightarrow z = \mu + \sigma \odot \varepsilon$$

with $\mu$ and $\sigma$ highlighted in yellow and $\varepsilon$ in light blue, and below it: "where $\varepsilon \sim \mathcal{N}(0,1)$".

Footer credit: Kingma+ *ICLR* 2014.

*Figure: yes — cropped VAE diagram showing the mean and standard-deviation boxes feeding the sampled z*

## Slide 36 — Reparametrizing the sampling layer

![Slide 36 — Reparametrizing the sampling layer](../images/04-deep-generative-modeling/slide-36.jpg)

A computation-graph diagram. A legend at left: a blue diamond labelled "Deterministic node" and an orange circle labelled "Stochastic node". The graph, captioned "Original form": blue diamonds $\phi$ (lower left) and $x$ (lower centre) each have a blue arrow pointing up into an orange circle $z$ labelled at its left $z \sim q_{\phi}(\mathrm{z}|x)$; a blue arrow goes from $z$ up to a blue diamond $f$ at the top. A red arrow labelled "Backprop" points down from above on the right of $z$ onto a red cross (X) beside the $z$ circle, showing that the gradient cannot flow back through the stochastic node.

Footer credit: Kingma+ *ICLR* 2014.

*Figure: yes — computation graph of the original form with a stochastic node z blocking backpropagation*

## Slide 37 — Reparametrizing the sampling layer

![Slide 37 — Reparametrizing the sampling layer](../images/04-deep-generative-modeling/slide-37.jpg)

Build step: adds the reparametrized form to the right of slide 36's original form.

Legend and the "Original form" graph at left as slide 36 (without the Backprop arrow and red cross). At right, captioned "Reparametrized form": blue diamonds $\phi$, $x$ and an orange circle $\varepsilon$, labelled at its right $\sim\mathcal{N}(0,1)$, each have a blue arrow up into a blue diamond $z$, labelled at its right $z = g(\phi, x, \varepsilon)$, which has an arrow up to a blue diamond $f$. A red arrow labelled "Backprop" points down from near $f$ to the label $\frac{\partial f}{\partial z}$ beside $z$, and a red arrow from there points down-left to the label $\frac{\partial f}{\partial \phi}$ beside $\phi$, showing the gradient flowing back through the now-deterministic $z$ to $\phi$; the randomness sits in the separate $\varepsilon$ node.

Footer credit: Kingma+ *ICLR* 2014.

*Figure: yes — original and reparametrized computation graphs, with gradients flowing through z to phi in the reparametrized form*

## Slide 38 — VAE computation graph

The VAE diagram as slide 33 (input digit image "2", bar $x$, green encoder, boxes $\mu$ and $\sigma$ with orange arrows into $z$, purple decoder, bar $\hat{x}$, blurry output digit; bracket "Encoder computes: $q_{\phi}(\mathrm{z}|x)$" and bracket "Decoder computes: $p_{\theta}(\mathrm{x}|z)$"). The $z$ box has no black outline. The bottom line is now bold: "Sample from latent space and decode to generate new samples".

Footer credit: Kingma+ *ICLR* 2014.

*Figure: yes — VAE diagram: input digit, encoder, mean and standard deviation boxes, sampled z, decoder, blurry reconstruction*

## Slide 39 — VAEs: Latent perturbation

![Slide 39 — VAEs: Latent perturbation](../images/04-deep-generative-modeling/slide-39.jpg)

Text: "Slowly increase or decrease a **single latent variable**" / "Keep all other variables fixed".

A horizontal strip of ten small, low-resolution grey-scale photographs of a face, side by side. Across the strip the head turns gradually (from facing slightly to one side at the left to a different angle at the right). Beneath the strip a blue double-headed horizontal arrow spans its full width, labelled "Head pose".

Bottom text: "Different dimensions of $z$ encodes **different interpretable latent features**"

Footer credit: Kingma+ *ICLR* 2014.

*Figure: yes — strip of ten grey-scale face images showing head pose changing along one latent dimension*

## Slide 40 — VAEs: Latent perturbation

![Slide 40 — VAEs: Latent perturbation](../images/04-deep-generative-modeling/slide-40.jpg)

At left, a square grid of small grey-scale face photographs (7 rows by 10 columns). A vertical blue double-headed arrow at its left, labelled "Smile", shows that the facial expression changes down the rows; a horizontal blue double-headed arrow below it, labelled "Head pose", shows that the head pose changes along the columns.

Text at right (centred): "Ideally, we want latent variables that are uncorrelated with each other"; "Enforce diagonal prior on the latent variables to encourage independence"; bold: "Disentanglement".

Footer credit: Kingma+ *ICLR* 2014; Chen+ *NeurIPS* 2018.

*Figure: yes — grid of grey-scale faces varying in smile along the vertical axis and head pose along the horizontal axis*

## Slide 41 — Latent space disentanglement with β-VAEs

![Slide 41 — Latent space disentanglement with β-VAEs](../images/04-deep-generative-modeling/slide-41.jpg)

Title: "Latent space disentanglement with β-VAEs". At the top left, two bold lines are printed on top of each other, so that the letters overlap and are hard to read: "Standard VAE loss:" and "β-VAE loss:" (read from an enlarged crop; the overlap is as printed).

Equation:

$$\mathcal{L}(\theta, \phi; \mathbf{x}, \mathbf{z}, \beta) = \mathbb{E}_ {q_{\phi}(\mathbf{z}|\mathbf{x})}\left[\log p_{\theta}(\mathbf{x}|\mathbf{z})\right] - D_{KL}\left(q_{\phi}(\mathbf{z}|\mathbf{x}) \Vert p(\mathbf{z})\right)$$

An empty red-outlined square box stands between the minus sign and $D_{KL}$ (the place where $\beta$ would multiply the term; nothing is printed in it). A red underline beneath the expectation term is labelled "Reconstruction term"; a red underline beneath the $D_{KL}$ term is labelled "Regularization term".

Text below: "β > 1: constrain latent bottleneck, encourage efficient latent encoding → disentanglement"

Bold heading: "Head rotation (azimuth)". Below it, two grids of small colour face images, each with 5 rows and 7 columns, in which the head rotates from left to right along each row. Left grid, captioned "Standard VAE (β = 1)", with red text at its left: "Smile also changing!". Right grid, captioned "β-VAE (β = 250)", with red text at its right: "Smile relatively constant!". The left rows show faces whose expression changes along with the rotation; the right-hand faces are blurrier and keep the same expression along each row.

Footer credit: Higgins+ *ICLR* 2017.

*Figure: yes — two grids of generated faces rotating in azimuth, standard VAE versus beta-VAE*

## Slide 42 — Why latent variable models? Debiasing

Text: "Capable of uncovering **underlying latent variables** in a dataset".

Two photograph grids (6 rows by 10 columns of small face photographs) separated by "vs". The left grid, captioned "Homogeneous skin color, pose", shows mostly light-skinned, front-facing, smiling faces in similar lighting. The right grid, captioned "Diverse skin color, pose, illumination", shows faces of varied skin tones, head poses, lighting and accessories (sunglasses, caps).

Bottom text: "How can we use latent distributions to create fair and representative datasets?" At the lower right, a gold five-pointed star with the bold label "Software Lab!".

Footer credit: Amini/Soleimany+ *AAAI/AIES* 2019.

*Figure: yes — two grids of face photographs contrasting a homogeneous and a diverse dataset*

## Slide 43 — VAE summary

1. Compress representation of world to something we can use to learn

A small horizontal VAE diagram near the bottom centre: a black-framed pixelated image of a handwritten digit "2", a tall light-blue bar $x$, a green trapezoid narrowing to the right (encoder), a small salmon-red box $z$, a purple trapezoid widening to the right (decoder), a tall blue-violet bar $\hat{x}$, and a black-framed blurry grey image of a "2". There are no brackets or other labels.

*Figure: yes — small VAE diagram: input digit, encoder, z, decoder, blurry reconstruction*

## Slide 44 — VAE summary

Build step: adds item 2 to the list of slide 43.

1. Compress representation of world to something we can use to learn
2. Reconstruction allows for unsupervised learning (no labels!)

A small horizontal VAE diagram near the bottom centre: a black-framed pixelated image of a handwritten digit "2", a tall light-blue bar $x$, a green trapezoid narrowing to the right (encoder), a small salmon-red box $z$, a purple trapezoid widening to the right (decoder), a tall blue-violet bar $\hat{x}$, and a black-framed blurry grey image of a "2". There are no brackets or other labels.

*Figure: yes — small VAE diagram: input digit, encoder, z, decoder, blurry reconstruction*

## Slide 45 — VAE summary

Build step: adds item 3 to the list of slide 44.

1. Compress representation of world to something we can use to learn
2. Reconstruction allows for unsupervised learning (no labels!)
3. Reparameterization trick to train end-to-end

A small horizontal VAE diagram near the bottom centre: a black-framed pixelated image of a handwritten digit "2", a tall light-blue bar $x$, a green trapezoid narrowing to the right (encoder), a small salmon-red box $z$, a purple trapezoid widening to the right (decoder), a tall blue-violet bar $\hat{x}$, and a black-framed blurry grey image of a "2". There are no brackets or other labels.

*Figure: yes — small VAE diagram: input digit, encoder, z, decoder, blurry reconstruction*

## Slide 46 — VAE summary

Build step: adds item 4 to the list of slide 45.

1. Compress representation of world to something we can use to learn
2. Reconstruction allows for unsupervised learning (no labels!)
3. Reparameterization trick to train end-to-end
4. Interpret hidden latent variables using perturbation

A small horizontal VAE diagram near the bottom centre: a black-framed pixelated image of a handwritten digit "2", a tall light-blue bar $x$, a green trapezoid narrowing to the right (encoder), a small salmon-red box $z$, a purple trapezoid widening to the right (decoder), a tall blue-violet bar $\hat{x}$, and a black-framed blurry grey image of a "2". There are no brackets or other labels.

*Figure: yes — small VAE diagram: input digit, encoder, z, decoder, blurry reconstruction*

## Slide 47 — VAE summary

Build step: adds item 5 to the list of slide 46.

1. Compress representation of world to something we can use to learn
2. Reconstruction allows for unsupervised learning (no labels!)
3. Reparameterization trick to train end-to-end
4. Interpret hidden latent variables using perturbation
5. Generating new examples

A small horizontal VAE diagram near the bottom centre, as slide 43: a black-framed pixelated image of a handwritten digit "2", a tall light-blue bar $x$, a green trapezoid narrowing to the right (encoder), a small salmon-red box $z$, a purple trapezoid widening to the right (decoder), a tall blue-violet bar $\hat{x}$, and a black-framed blurry grey image of a "2".

*Figure: yes — small VAE diagram: input digit, encoder, z, decoder, blurry reconstruction*

## Slide 48 — Generative Adversarial Networks (GANs)

Section-divider slide. Plain blue background with a faint diagonal "MIT 6.S191" watermark. Centred white text: "Generative Adversarial Networks (GANs)". No footer.

*Figure: no*

## Slide 49 — What if we just want to sample?

![Slide 49 — What if we just want to sample?](../images/04-deep-generative-modeling/slide-49.jpg)

"**Idea:** don't explicitly model density, and instead just sample to generate new instances."

"**Problem:** want to sample from complex distribution – can't do this directly!"

"**Solution:** sample from something simple (e.g., noise), learn a transformation to the data distribution."

Diagram, left to right: the label "noise" beside a salmon-red rounded box $z$; a purple trapezoid widening to the right labelled $G$ with the caption "Generator Network $G$" beneath it; a tall blue-violet bar with the rotated label $X_{fake}$; and at right a light-blue irregular blob (an odd, roughly triangular outline with a concave side) labelled "X" in bold, with the caption "“fake” sample from learned representation of data distribution". There are no arrows; the elements are placed in a row, showing noise passing through the generator to give a fake sample in the data space.

*Figure: yes — noise z fed to generator G, giving X_fake, a sample from the data distribution blob X*

## Slide 50 — Generative Adversarial Networks (GANs)

![Slide 50 — Generative Adversarial Networks (GANs)](../images/04-deep-generative-modeling/slide-50.jpg)

"**Generative Adversarial Networks (GANs)** are a way to make a generative model by having two neural networks compete with each other."

Diagram: at lower left the label "noise" beside a salmon-red box $z$ feeding a purple trapezoid $G$ (generator), which outputs a blue-violet vertical bar labelled $X_{fake}$. Above it a pale-blue vertical bar labelled $X_{real}$. A black curved line runs from each of the two bars into the left (wide) side of a green trapezoid $D$ that narrows to the right (the discriminator), whose output is a yellow circle labelled $y$.

Text at left, above the generator: "The **generator** turns noise into an imitation of the data to try to trick the discriminator." Text at upper right: "The **discriminator** tries to identify real data from fakes created by the generator."

Footer credit: Goodfellow+ *NeurIPS* 2014.

*Figure: yes — GAN diagram: generator G makes X_fake from noise z, discriminator D sees X_real and X_fake and outputs y*

## Slide 51 — Intuition behind GANs

"**Generator** starts from noise to try to create an imitation of the data."

At right, the heading "Generator" above a horizontal black number line with arrowheads at both ends, carrying three salmon-pink dots: two close together near the left end and one near the right end. At lower centre a legend: a salmon-pink circle labelled "Fake data". The left half of the slide is empty.

*Figure: yes — a one-dimensional line with three pink fake-data points under the heading Generator*

## Slide 52 — Intuition behind GANs

Build step: adds the discriminator's line at left of slide 51.

"**Discriminator** looks at both real data and fake data created by the generator."

Two headings and lines side by side: "Discriminator" at left and "Generator" at right, each above a horizontal black double-headed number line. Each line carries the same three salmon-pink dots (two close together near the left end, one near the right end). Legend at lower centre: a salmon-pink circle labelled "Fake data".

*Figure: yes — two one-dimensional lines (Discriminator and Generator) each with three pink fake-data points*

## Slide 53 — Intuition behind GANs

Build step: adds real data to the discriminator's line on slide 52.

Same text, headings and layout as slide 52. On the Discriminator's line, three green dots (real data) now sit close together in the middle, between the two left pink dots and the right pink dot, in the order pink, pink, green, green, green, pink from left to right. The Generator's line is unchanged (three pink dots). The legend now has two entries: a green circle labelled "Real data" and a salmon-pink circle labelled "Fake data".

*Figure: yes — Discriminator line with three green real points in the middle among pink fake points, and the Generator line with only pink points*

## Slide 54 — Intuition behind GANs

Build step: changes the sentence and adds a red frame and the $P(real)=1$ line around the discriminator on slide 53.

"**Discriminator** tries to predict what's real and what's fake."

The Discriminator part (heading and number line with the pink and green dots as slide 53) is enclosed in a red rounded rectangle. Inside it, above the number line, is the label $P(real) = 1$ with a horizontal black dashed line beneath it. The Generator line at right and the two-entry legend ("Real data" green, "Fake data" pink) are unchanged.

*Figure: yes — Discriminator frame with a dashed P(real)=1 level above the real and fake points*

## Slide 55 — Intuition behind GANs

![Slide 55 — Intuition behind GANs](../images/04-deep-generative-modeling/slide-55.jpg)

Build step: adds grey bars above the six points in the discriminator frame of slide 54.

Same text, frame, $P(real) = 1$ label with dashed line, number lines and legend as slide 54. In the Discriminator frame, a grey vertical bar now rises from each of the six dots (the dashed $P(real)=1$ line is the top of the scale; the bars are all well below it). Approximate heights, left to right (as a fraction of the distance from the number line to the dashed line, about 150 px): first pink dot, about 0.25; second pink dot, about 0.45; first green dot, about 0.65; second green dot, about 0.45; third green dot, about 0.7; right-hand pink dot, about 0.55. The bars are the discriminator's current probability of "real" at each point; no axis numbers are printed. The Generator line is unchanged.

*Figure: yes — discriminator's grey probability bars above real and fake points, all below the P(real)=1 line*

## Slide 56 — Intuition behind GANs

Build step: changes the bar heights of slide 55.

Same as slide 55 except for the grey bars, which now are low over the pink (fake) dots and higher over the green (real) dots. Approximate heights as a fraction of the distance to the dashed line: first pink dot about 0.15; second pink dot about 0.2; first green dot about 0.8; second green dot about 0.7; third green dot about 0.95; right-hand pink dot about 0.35. The bars still do not reach the dashed $P(real)=1$ line. The Generator line is unchanged.

*Figure: yes — discriminator's bars now taller over real points than over fake ones*


## Slide 57 — Intuition behind GANs

![Slide 57 — Intuition behind GANs](../images/04-deep-generative-modeling/slide-57.jpg)

Build step: re-shows slide 56's discriminator panel with the bars changed; the bars now show the discriminator's output.

Subtitle: "**Discriminator** tries to predict what's real and what's fake." (the word "Discriminator" in bold.)

Two panels side by side. The left panel, labelled "Discriminator", is enclosed in a dark red rounded rectangle (it is the highlighted panel). The right panel is labelled "Generator" and has no box. Each panel has a horizontal black double-headed arrow (a number line) near the bottom. At the top of the left panel is the label $P(real) = 1$ with a black dashed horizontal line beneath it, level with the tops of the tallest bars.

Left (discriminator) number line: two pink dots at the far left, three green dots clustered near the middle, and one pink dot to the right. Above the three green dots are three adjacent tall light-grey vertical bars, each reaching up to the dashed $P(real) = 1$ line. No bars stand above the pink dots in this step.

Right (generator) number line: two pink dots at the far left and one pink dot at the far right, with a large gap between them; no green dots and no bars.

Legend at the bottom: a green circle labelled "Real data" and a pink circle labelled "Fake data".

The figure shows a discriminator assigning probability of being real 1 to the real data (green) at this stage, while the fake (pink) points are shown without bars, and the generator has produced only fake points.

*Figure: yes — GAN intuition on number lines: discriminator bars at P(real)=1 over the green real points, generator showing only pink fake points*

## Slide 58 — Intuition behind GANs

Build step: the subtitle changes and the generator panel is highlighted; green real-data dots appear on the generator's number line.

Subtitle: "**Generator** tries to improve its imitation of the data." (the word "Generator" in bold.)

Two panels as on slide 57, but now the dark red rounded rectangle surrounds the right panel, "Generator", and the left panel, "Discriminator", is unboxed. The discriminator panel is unchanged from slide 57: the label $P(real) = 1$ with the dashed line, the number line with two pink dots, three green dots and one pink dot, and the three light-grey bars over the green dots reaching the dashed line.

Generator number line: two pink dots at the far left, three green dots in the middle, and one pink dot at the far right. This is the first time green dots appear on the generator line; they sit at the same relative positions as the green dots on the discriminator line.

Legend: green circle "Real data", pink circle "Fake data".

*Figure: yes — GAN intuition on number lines with the generator panel highlighted and the real data shown beside the fake pink points*

## Slide 59 — Intuition behind GANs

Build step: the generator's pink fake dots move toward the green real dots.

Subtitle: "**Generator** tries to improve its imitation of the data." Same layout as slide 58, with the generator panel boxed in dark red and the discriminator panel unchanged (three grey bars over the green dots, reaching the $P(real) = 1$ dashed line; pink dots at left and right).

Generator number line: the two left pink dots have moved a little to the right (closer to the green cluster), and the right pink dot has moved left (closer to the green cluster); the three green dots stay in the middle.

Legend: "Real data" (green), "Fake data" (pink).

*Figure: yes — generator number line where the pink fake points have shifted toward the green real points*

## Slide 60 — Intuition behind GANs

![Slide 60 — Intuition behind GANs](../images/04-deep-generative-modeling/slide-60.jpg)

Build step: the generator's fake dots move still closer to the real data.

Subtitle: "**Generator** tries to improve its imitation of the data." Same layout as slide 59.

Generator number line: the two pink dots on the left of the green cluster and the one pink dot on the right have moved further in and now sit just beside the green dots, so the six points form a close row: pink, pink, green, green, green, pink. The discriminator panel is unchanged (three grey bars reaching the dashed $P(real) = 1$ line over the green dots; pink dots at left and right with no bars).

Legend: "Real data" (green), "Fake data" (pink).

*Figure: yes — generator number line with the pink fake points now adjacent to the green real points*

## Slide 61 — Intuition behind GANs

Build step: the highlight returns to the discriminator, whose number line is updated with the generator's new fake points and the bars are removed.

Subtitle: "**Discriminator** tries to predict what's real and what's fake." The dark red rounded rectangle surrounds the left panel, "Discriminator".

Discriminator panel: label $P(real) = 1$ with the black dashed line, and a number line on which the points now read, left to right: two pink dots, three green dots, one pink dot, packed close together in the middle of the line. There are no bars.

Generator panel (unboxed): label "Generator" and a number line with the same six points in the same order (pink, pink, green, green, green, pink), as at the end of slide 60.

Legend: "Real data" (green), "Fake data" (pink).

*Figure: yes — discriminator and generator number lines both showing the pink fake points interleaved close to the green real points*

## Slide 62 — Intuition behind GANs

![Slide 62 — Intuition behind GANs](../images/04-deep-generative-modeling/slide-62.jpg)

Build step: grey bars reappear over the discriminator's number line.

Subtitle: "**Discriminator** tries to predict what's real and what's fake." Same layout as slide 61, with the discriminator panel boxed in dark red.

Discriminator panel: the number line has, left to right, two pink dots, three green dots, one pink dot. Six light-grey vertical bars stand over the six points. The three bars over the green dots are the tallest and reach the dashed $P(real) = 1$ line. The two bars over the left pink dots are shorter (the first shorter than the second, with the second about two thirds of the way to the line), and the bar over the right pink dot is of intermediate height, a little below the line. So the discriminator now gives the fake points fairly high probabilities of being real.

Generator panel (unboxed): the same six points as on slide 61, left to right pink, pink, green, green, green, pink.

Legend: "Real data" (green), "Fake data" (pink).

*Figure: yes — discriminator bars of varying height over fake and real points, fake points now rated as fairly likely real*

## Slide 63 — Intuition behind GANs

Build step: the discriminator's bars over the fake points are lowered.

Subtitle: "**Discriminator** tries to predict what's real and what's fake." The dark red rounded rectangle surrounds the left panel, "Discriminator".

Discriminator panel: label $P(real) = 1$ with the black dashed line; number line with two pink dots, three green dots, one pink dot (left to right). The three grey bars over the green dots still reach the dashed line. The grey bars over the three pink dots are lower than on slide 62: the first is the shortest, the second slightly taller, and the third (right-hand) taller again but still well below the dashed line.

Generator panel (unboxed): number line with pink, pink, green, green, green, pink points, as on slides 61 and 62.

Legend: "Real data" (green), "Fake data" (pink).

*Figure: yes — discriminator bars over fake points lowered while bars over real points stay at P(real)=1*

## Slide 64 — Intuition behind GANs

![Slide 64 — Intuition behind GANs](../images/04-deep-generative-modeling/slide-64.jpg)

Build step: the discriminator's bars over the fake points are lowered further.

Subtitle: "**Discriminator** tries to predict what's real and what's fake." Same layout as slide 63, with the discriminator panel boxed.

Discriminator panel: the three grey bars over the green dots still reach the dashed $P(real) = 1$ line; the bars over the three pink dots are now lower still (the two left ones are short, about a fifth to a quarter of the way to the dashed line, and the right-hand one is somewhat taller than them).

Generator panel (unboxed): the same six points (pink, pink, green, green, green, pink).

Legend: "Real data" (green), "Fake data" (pink).

*Figure: yes — discriminator bars over fake points lowered further, separating them from the real points*

## Slide 65 — Intuition behind GANs

Build step: the subtitle changes and the highlight moves to the generator, whose fake points move closer to the real ones.

Subtitle: "**Generator** tries to improve its imitation of the data." The dark red rounded rectangle surrounds the right panel, "Generator".

Discriminator panel (unboxed): unchanged from slide 64, with the three tall bars over the green dots at the dashed $P(real) = 1$ line and shorter bars over the three pink dots.

Generator panel: number line on which the points now read pink, pink, green, green, green, pink, with the pink points touching or nearly touching the neighbouring green points. The right-hand pink dot lies right next to the third green dot.

Legend: "Real data" (green), "Fake data" (pink).

*Figure: yes — generator number line with fake pink points moved right up against the green real points*

## Slide 66 — Intuition behind GANs

Build step: the generator's fake points move to overlap the real points.

Subtitle: "**Generator** tries to improve its imitation of the data." Same layout as slide 65, with the generator panel boxed.

Discriminator panel (unboxed): unchanged from slide 65.

Generator panel: the two left pink dots have moved right, so that the second pink dot partly overlaps the first green dot, and the right-hand pink dot partly overlaps the third green dot. The pink and green points now form a tight cluster in the middle of the line.

Legend: "Real data" (green), "Fake data" (pink).

*Figure: yes — generator number line with pink fake points partly overlapping the green real points*

## Slide 67 — Intuition behind GANs

Build step: the generator's fake points move further, overlapping the real points more.

Subtitle: "**Generator** tries to improve its imitation of the data." The dark red rounded rectangle surrounds the right panel, "Generator".

Discriminator panel (unboxed): unchanged from slide 66 (three tall grey bars over the green dots at the dashed $P(real) = 1$ line; shorter bars over the three pink dots).

Generator panel: the six points are now bunched tightly in the middle of the line. The first pink dot sits just left of the first green dot and overlaps it slightly, the second pink dot sits right of that and overlaps it, the middle green dot is alone, and the right-hand pink dot overlaps the third green dot. Pink and green dots are thus almost indistinguishable in position.

Legend: "Real data" (green), "Fake data" (pink).

*Figure: yes — generator number line with the pink fake points now bunched on top of the green real points*

## Slide 68 — Intuition behind GANs

![Slide 68 — Intuition behind GANs](../images/04-deep-generative-modeling/slide-68.jpg)

Build step: the red highlight boxes are removed and the subtitle becomes a two-line summary of both roles.

Subtitle, two centred lines: "**Discriminator** tries to identify real data from fakes created by the generator." and "**Generator** tries to create imitations of data to trick the discriminator." (the words "Discriminator" and "Generator" in bold.)

Two unboxed panels, "Discriminator" (left) and "Generator" (right). Discriminator panel: label $P(real) = 1$ with the black dashed line; number line with two pink dots, three green dots, one pink dot; three tall grey bars over the green dots reaching the dashed line, and three shorter grey bars over the pink dots (the left two shorter than the right one). Generator panel: the same tight cluster of six dots as on slide 67 (pink and green overlapping in the middle of the line).

Legend: "Real data" (green), "Fake data" (pink).

*Figure: yes — final state of the GAN number-line intuition, discriminator bars beside the generator's fake points overlapping the real points*

## Slide 69 — Training GANs

Diagram of a GAN, with text.

Top right text: "**D** tries to identify the synthesized instances" (the letter D bold). Left text: "**G** tries to synthesize fake instances that fool **D**" (G and D bold). Bottom text, two lines: "**Training:** adversarial objectives for **D** and **G**" and "**Global optimum: G** reproduces the true data distribution" (bold as marked).

Diagram, left to right. A small salmon-pink square labelled $z$ with the word "noise" to its left. To its right a purple trapezoid labelled $G$, wider on the right (an expanding shape, narrow at the $z$ end). It outputs to a tall narrow blue-violet vertical rectangle labelled $X_{fake}$ (text rotated). Above it is a similar tall narrow pale-blue vertical rectangle labelled $X_{real}$. A black curved line runs from each of $X_{real}$ and $X_{fake}$ into the wide left side of a green trapezoid labelled $D$, which narrows to the right. A black line from the narrow end of $D$ leads to a yellow circle labelled $y$.

The figure shows noise fed through the generator to produce fake data, and the discriminator taking both real and fake data and producing an output $y$.

*Figure: yes — GAN architecture: noise z into generator G producing X_fake, X_real and X_fake both into discriminator D, output y*

## Slide 70 — Training GANs: loss function

![Slide 70 — Training GANs: loss function](../images/04-deep-generative-modeling/slide-70.jpg)

Build step: the GAN diagram of slide 69 is re-shown with the generator faded out, and the discriminator's loss is added.

Text at top right: "**D** tries to identify the synthesized images" (D bold; note "images" here against "instances" on slide 69).

Diagram as on slide 69 but the noise $z$ (with the word "noise") and the generator $G$ are very faint, almost invisible, while $X_{real}$ (pale blue rectangle), $X_{fake}$ (blue-violet rectangle), the green trapezoid $D$ and the yellow circle $y$ are at full strength with their black connecting curves.

Below the diagram, the loss:

$$\arg\max_{D} \mathbb{E}_ {\mathbf{z},\mathbf{x}}\left[ \log D(G(\mathbf{z})) + \log \left(1 - D(\mathbf{x})\right) \right]$$

Under $\arg\max$ is $D$ with a short green underline beneath it. Under the term $\log D(G(\mathbf{z}))$ is a blue-violet underline labelled "Fake" (bold); under the term $\log (1 - D(\mathbf{x}))$ is a pale-blue underline labelled "Real" (bold). The underline colours match the $X_{fake}$ and $X_{real}$ boxes.

Note: as printed, the term $\log D(G(\mathbf{z}))$ is labelled "Fake" and $\log (1 - D(\mathbf{x}))$ is labelled "Real", that is, $D$ of the generated sample is not subtracted from 1 and $D$ of $\mathbf{x}$ is. This is reproduced as printed.

*Figure: yes — GAN diagram with generator faded, discriminator D highlighted, and the colour-coded loss terms for fake and real*

## Slide 71 — Training GANs: loss function

Build step: the discriminator side of slide 70 is faded out and the generator side is brought to full strength, with the generator's objective.

Text at left: "**G** tries to synthesize fake images that fool **D**" (G and D bold).

Diagram: the noise square $z$ (labelled "noise"), the purple trapezoid $G$ and the blue-violet rectangle $X_{fake}$ are at full strength. The pale-blue $X_{real}$ rectangle, the green trapezoid $D$, the yellow circle $y$ and the connecting curves are very faint. 

Below the diagram:

$$\arg\min_{G} \mathbb{E}_ {\mathbf{z},\mathbf{x}}\left[ \log D(G(\mathbf{z})) + \log \left(1 - D(\mathbf{x})\right) \right]$$

with $G$ under $\arg\min$ and a short purple underline beneath it. The Fake and Real labels and coloured underlines of slide 70 are no longer present.

*Figure: yes — GAN diagram with the generator highlighted and the discriminator faded, above the arg min over G loss*

## Slide 72 — Training GANs: loss function

![Slide 72 — Training GANs: loss function](../images/04-deep-generative-modeling/slide-72.jpg)

Build step: both networks are at full strength and the two objectives are combined into a min-max.

Title as printed: "Training GANs: loss function". The full GAN diagram: the noise square $z$ (labelled "noise") feeding the purple trapezoid $G$, which produces the blue-violet $X_{fake}$ rectangle; the pale-blue $X_{real}$ rectangle above it; curves from both into the green trapezoid $D$; and a yellow circle $y$ at the output of $D$.

Text at lower right, beneath $D$: "**G** tries to synthesize fake images that fool the *best* **D**" (G and D bold, "best" in italics).

Below the diagram:

$$\arg\min_{G} \max_{D} \mathbb{E}_ {\mathbf{z},\mathbf{x}}\left[ \log D(G(\mathbf{z})) + \log \left(1 - D(\mathbf{x})\right) \right]$$

with $G$ under $\arg\min$ and $D$ under $\max$. There are no coloured underlines or Fake/Real labels.

*Figure: yes — full GAN diagram (z, G, X_fake, X_real, D, y) above the min-max objective*

## Slide 73 — Generating new data with GANs

Text at the bottom: "After training, use generator network to create **new data** that's never been seen before." (the words "new data" in bold.)

Diagram: the same GAN diagram as slide 69, with the discriminator side faded out. The noise square $z$ (labelled "noise"), the purple trapezoid $G$ and the blue-violet rectangle $X_{fake}$ are at full strength; $X_{real}$, $D$ and $y$ and the connecting curves are very faint. Only the path from the noise through the generator to $X_{fake}$ is emphasized.

*Figure: yes — GAN diagram with only noise z, generator G and output X_fake shown at full strength*

## Slide 74 — GANs are distribution transformers

![Slide 74 — GANs are distribution transformers](../images/04-deep-generative-modeling/slide-74.jpg)

Text at upper left: "Gaussian noise" and below it $z \sim \mathrm{N}(0,1)$ (the N is upright, not calligraphic as on slide 28).

Diagram, left to right. A salmon-pink rounded square with a black outline contains the letter $z$ and a black dot in its upper right corner. A black curved arrow runs from that dot to the narrow (left) edge of a purple trapezoid labelled $G$, which widens to the right; below it is the caption "Trained generator". From the wide edge of $G$ a black curved arrow points up to a small square photograph of a black bird with a long curved neck and a red beak standing on green grass. From the photograph's right edge a black dashed arrow curves down and to the right, ending in a black dot inside a pale-blue irregular blob. The blob is labelled "X" (bold) and captioned "Learned target data distribution". The blob has an irregular shape with a wide left-hand base, a notch at its upper left, and a protruding point to the right.

The figure shows noise sampled from a Gaussian being mapped by the trained generator to an image that lies within the learned data distribution.

*Figure: yes — Gaussian noise z through trained generator G to a generated bird image that lands as a dot inside the learned data distribution X*

## Slide 75 — GANs are distribution transformers

Build step: a different noise sample is shown, mapping to a different generated image.

Same layout, labels and captions as slide 74 ("Gaussian noise", $z \sim \mathrm{N}(0,1)$, "Trained generator", "Learned target data distribution", blob labelled "X"). The black dot in the salmon-pink square $z$ is now at the lower right of the square, and a black curved arrow runs from it to the purple trapezoid $G$. The generated image is now a photograph of a small bird with a dark head, an orange-brown breast and a grey-brown back, perched among green foliage. A black dashed arrow runs straight to the right from the photograph and ends in a black dot in the upper part of the pale-blue blob $X$. (On slide 74 the sample was a black bird and the dot was low in the blob; here a different noise point maps to a different image and a different point in the distribution.)

*Figure: yes — a second noise sample through the generator gives a different bird image and a different point in the learned distribution*

## Slide 76 — GANs are distribution transformers

![Slide 76 — GANs are distribution transformers](../images/04-deep-generative-modeling/slide-76.jpg)

Build step: two noise points are joined by a dashed line, and a row of interpolated images is added beneath.

Same title, labels and captions as slides 74 and 75. In the salmon-pink square $z$ there are now two black dots, both near its right edge (one upper right, one lower and slightly to its left), joined by a near-vertical black dashed line. A dashed arrow runs from the square to the purple trapezoid $G$. A dashed arrow runs from $G$ to a faded, nearly white square image containing a black question mark "?", and another dashed arrow runs from the "?" to the pale-blue blob $X$. In the blob, two black dots (one near the top, one near the lower left) are joined by a black dashed line. So the line between two noise points is mapped by the generator to a path between two points in the learned distribution.

Along the bottom is a horizontal strip of eight photographs, side by side, mostly on a green grass background (the last has a blurred backdrop with a branch). From left to right they change gradually: the first two show a black bird with a long curved neck and a red beak, the next ones show it shrinking into a smaller dark bird, and the last ones show a small bird with a dark back and an orange breast, the same kind of bird as in the photograph on slide 75.

Footer credit: Brock+ *ICLR* 2019.

*Figure: yes — noise interpolation: two z points joined by a line map through G to a path in distribution X, with a strip of eight images morphing from a black long-necked bird to a small orange-breasted bird*

## Slide 77 — Distribution transformations

![Slide 77 — Distribution transformations](../images/04-deep-generative-modeling/slide-77.jpg)

Two labelled diagrams.

Top row, bold label "GANs:". Above a salmon-pink circle containing $z$ (bold italic) is the text "Gaussian noise" and $z \sim N(0,1)$. A thick black arrow points right from the circle to a pale-blue irregular blob labelled "Y" (bold). Beneath it the caption: "Gaussian noise → target data manifold".

Bottom row, bold label "CycleGANs:". A green irregular blob labelled "X" (bold) with a thick black arrow pointing right to the same pale-blue blob labelled "Y". Caption beneath: "data manifold X → data manifold Y".

The blobs have an irregular shape with a notch in the upper left and a protruding point to the right; the green "X" blob is a similar shape to the blue "Y" blob but not identical.

*Figure: yes — diagram of GANs mapping Gaussian noise to a target data manifold, and CycleGANs mapping data manifold X to data manifold Y*

## Slide 78 — CycleGAN: domain transformation

![Slide 78 — CycleGAN: domain transformation](../images/04-deep-generative-modeling/slide-78.jpg)

Subtitle: "CycleGAN learns transformations across domains with unpaired data."

Diagram, centred: two black-outlined squares, left labelled $X$ and right labelled $Y$. Above the left square is a short dotted black arrow pointing up to $D_X$; above the right square a dotted arrow pointing up to $D_Y$. Two curved black arrows connect the squares: an upper arrow from $X$ to $Y$ labelled $G$, and a lower arrow from $Y$ back to $X$ labelled $F$.

Below it is a wide image made of two photographs side by side, split down the middle: on the left a brown horse standing in a grass field beside a wire fence with trees behind; on the right the same scene with the animal's coat replaced by black and white zebra stripes. A white circle with a red border and a white right-pointing triangle (a play button) is centred on the join, showing it is a video thumbnail.

Footer credit: Zhu+ *ICCV* 2017.

*Figure: yes — CycleGAN schematic (X and Y domains, mappings G and F, discriminators D_X and D_Y) and a video thumbnail of a horse turned into a striped zebra-like animal*

## Slide 79 — CycleGAN: transforming speech

![Slide 79 — CycleGAN: transforming speech](../images/04-deep-generative-modeling/slide-79.jpg)

Four panels arranged in a loop, each with a bold caption.

Top left: "Audio waveform (A)", a black rectangle with a green waveform (a thin centre line with bursts of amplitude, four or five bursts across the width). A thick blue arrow points down from it to the bottom-left panel.

Bottom left: "Spectrogram image (A)", a wide rectangular heat-map image with a dark purple/black background and orange, red and yellow bright regions concentrated in the lower half and in vertical bands, with fine horizontal striations.

Between the two spectrograms are two thick blue curved arrows forming a cycle: the upper one points from left to right (A to B), the lower one points from right to left (B to A).

Bottom right: "Spectrogram image (B)", a similar heat-map image with a different pattern of orange/red/yellow bands.

Top right: "Audio waveform (B)", a black rectangle with a green waveform of different bursts. A thick blue arrow points up from the Spectrogram (B) panel to it.

The figure shows speech audio A converted to a spectrogram image, translated by a cycle of mappings to a spectrogram image B, and converted back to audio B.

*Figure: yes — speech CycleGAN loop: waveform A to spectrogram A, a two-way arrow cycle to spectrogram B, then up to waveform B*

## Slide 80 — [Video thumbnail: original and synthesized speakers with audio waveforms]

Black slide with no standard footer. Two white captions at the top: "Original (Amini)" above the left half and "Synthesized (Obama)" above the right half. At the upper right is a logo: a dark-red patterned mark above the spaced white letters "CANNYAI" (the A's printed without crossbars).

Two side-by-side video frames. Left: a young-looking man with dark hair in a striped collared shirt, seated in front of a beige wall with a window on the right showing a white building; a microphone on a boom arm is in front of him. Right: a man in a dark suit, white shirt, dark red tie and a small flag pin on the lapel, with an American flag and a dark wooden background behind him, mouth open as if speaking. A red circle with a white outline and a white right-pointing triangle (a play button) is centred on the join, between the two frames and about halfway down.

Beneath each frame is a screenshot of an audio editor showing a green waveform (a timeline running to about 50 on the axis, labelled "hms") and below it a spectrogram in purple, red and orange with a frequency axis labelled with values such as "10k", "4k", "2k", "1k" and "Hz"; each has a green level meter (the left one between the two screenshots, the right one at the far right) and a timecode at the bottom left, "0:02.560" on the left and "0:02.571" on the right. The waveforms and spectrograms of the two sides look similar in pattern.

*Figure: yes — video thumbnail comparing an original speaker (left) with a synthesized speech/video of another speaker (right), with matching audio waveforms and spectrograms*

## Slide 81 — Deep Generative Modeling: Summary

Two rounded-rectangle boxes side by side with black outlines.

Left box: bold heading "Autoencoders and Variational Autoencoders (VAEs)", then "Learn lower-dimensional **latent space** and **sample** to generate input reconstructions" ("latent space" and "sample" in bold). Beneath it is a diagram, left to right: a pale-blue tall rectangle, a green trapezoid narrowing to the right, a small salmon-pink square, a purple trapezoid widening to the right, and a blue-violet tall rectangle. No labels are printed on this diagram.

Right box: bold heading "Generative Adversarial Networks (GANs)", then "Competing **generator** and **discriminator** networks" ("generator" and "discriminator" in bold). Beneath it is a diagram without labels: at lower left a small salmon-pink square, then a purple trapezoid widening to the right, then a tall blue-violet rectangle; above that a tall pale-blue rectangle; curved black lines from the pale-blue and blue-violet rectangles go to a green trapezoid narrowing to the right, which points to a yellow circle. This is the GAN diagram of slide 69 without the letters.

*Figure: yes — side-by-side unlabelled architecture diagrams for autoencoders/VAEs (encoder, latent square, decoder) and for GANs (generator and discriminator)*

## Slide 82 — Diffusion Models

Full-slide image with white bold text over it: title "Diffusion Models" and below it "...more to come in Lectures 6 and 7!" (bold, smaller). 

The image is a painterly landscape at dusk or night: a teal and dark-blue starry sky with clouds and small bright specks, a conical dark mountain in the centre, other rocky mountains left and right, a river or lake in the foreground reflecting a glowing orange-and-white light near the horizon, dark rocky banks and grass on both sides, and tall grass silhouetted at lower left. A small red figure-like patch is at the centre of the water's edge on the right bank. There is no standard footer on this slide.

*Figure: yes — full-slide painterly landscape used as the background of the Diffusion Models teaser*

## Slide 83 — [Lab 2 announcement: Facial Detection Systems]

Black slide with white text, no standard footer. At left is a blurred, low-detail photograph of a face, roughly square, occupying the left 40% of the slide.

At right, text centred: "MIT" and "Introduction to Deep Learning" (large); "Lab 2: Facial Detection Systems"; "Link to download labs:" followed by two red underlined links on separate lines, "introtodeeplearning.com#schedule" and "github.com/MITDeepLearning/introtodeeplearning". Then a numbered list: "1. Open the lab in Google Colab", "2. Start executing code blocks and filling in the #TODOs", "3. Need help? Come to 32-123!"

*Figure: yes — blurred face image decorating the announcement slide*

## Slide 84 — [Announcements and Reminders]

Black slide with white text, no standard footer. The same blurred face photograph as slide 83 is at the left.

At right: "Introduction to Deep Learning" (bold); "Announcements and Reminders" (bold); "Lecture 4: Generative Modeling starting soon!"; then three lines "Lab 2 begins today!", "Prizes for participants!", "Enter for a chance to win" followed by three dollar signs and "!"; then "Lots of swag will be available after class tomorrow!"; then "Interested in cutting-edge AI jobs?" and an underlined white link "introtodeeplearning.com/jobs.html".

*Figure: yes — blurred face image decorating the announcement slide*
