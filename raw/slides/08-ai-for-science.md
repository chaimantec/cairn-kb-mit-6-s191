---
title: Lecture 8 — AI for Science (slide deck)
lecture: 8
slides: 31
source_pdf: https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L8.pdf
note: Slide N = PDF page N (N = 1..31). The deck prints no slide numbers.
---

# Lecture 8 — AI for Science: slide-by-slide

Text and figures of all 31 slides of
[`6S191_MIT_DeepLearning_L8.pdf`](https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L8.pdf)
(MIT 6.S191 Introduction to Deep Learning, 2026 edition), a guest lecture by **Chris Bishop**, Technical
Fellow at Microsoft Research AI for Science, delivered 8 January 2026. Cite these as "slide N", where N
is the PDF page number. Diagrams, photographs, renderings, screenshots and charts are described in
prose, since the KB is read as text. What was said about each slide is in the
[transcript](../transcripts/08-ai-for-science.md).

## Numbering: slide numbers vs PDF pages

This deck is a PowerPoint export (Acrobat PDFMaker), unlike the image-only decks of lectures 1–6 and
the Google Slides export of lecture 7. It prints **no slide numbers and no footer**, so slide N is PDF
page N; the headings below were checked as a plain 1–31 sequence. Its pages mix vector text with
pasted pictures, and its text layer is sparse: it holds the slide titles and the deck's own labels, but
not the text inside the pictures (journal screenshots, charts, the timeline of slide 28), which was
read from the page. The text layer was used only for the spelling of printed prose; where it holds a
string the page does not show, that is said under the slide.

Several slides carry no title of their own: 4 (a quotation), 8 and 12 (screenshots of an essay and an
article), 11, 16, 17 and 21 (full-slide pictures), 25 (a chart) and 30 (a journal cover). Their headings
below describe them in the transcriber's words and say "(no printed title)" where none is printed.

## Images

18 slides carry their image under the heading: 5–7, 9, 13, 15, 17–28 — every slide with a distinct
figure. They are 1400×788 renders of the PDF pages. The other 13 are the title (1); the slide of
equations, which are reproduced below (2); slides of text or numbers that are transcribed exactly (3,
the electron's magnetic moment; 10, the benefits of emulators); slide 4's portrait beside the Dirac
quotation; screenshots of an essay and of journal articles whose text is transcribed (8, 12, 29); slide
11's unlabelled picture of a storm; slide 14's grid of photographs of application areas, whose captions
are transcribed; slide 16, a still from the video of MatterGen's denoising process; slide 30's journal
cover; and slide 31's book cover. Use only an image path that appears below; slides without one have no
image.

## Contents

| Slides | Section |
| ------ | ------- |
| 1 | Title |
| 2–4 | The greatest scientific discovery: the equations that describe the world, the electron's magnetic moment (theory against experiment) and Dirac's 1929 remark |
| 5–10 | AI in the scientific discovery loop; the no-free-lunch theorem (data against inductive bias); inductive bias in science; "The Bitter Lesson"; deep learning emulators and their benefits |
| 11–13 | The Earth system: a storm, the Aurora foundation model (Nature, 2025) |
| 14–17 | Molecules and materials: application areas, MatterGen (Nature, 2025), and its generated structures |
| 18–25 | The fundamental trilemma; the wavefunction and the curse of dimensionality; density functional theory (1965); the exchange-correlation functional; the DFT zoo; the Skala functional and its errors |
| 26–30 | Molecular biology: sequence, structure and function; molecular dynamics simulation; the curse of sequentiality; AI²BMD (Nature, 2024); a Science cover on emulating protein ensembles (2025) |
| 31 | The book *Deep Learning: Foundations and Concepts* (BishopBook.com) |

## Slide 1 — AI for Science

Text: "AI for Science"; "Prof Chris Bishop FREng FRSE FRS"; "Technical Fellow, *Microsoft Research AI for Science*" (the second part is italic).

Black title slide. At top left, the Microsoft logo (four-coloured squares: red, green, blue, yellow) with the word "Microsoft". At the right, a decorative cluster of outlined hexagons in teal, blue, purple and pink with thick edges, partly cut off by the right edge. No footer or slide number is printed on this slide.

*Figure: no*

## Slide 2 — The greatest scientific discovery ever made

Text: "The greatest scientific discovery ever made"

White equations on black, in three groups.

Top (the full-width equation):

$$\left(-\sum_{i=1}^{N}\frac{\hbar^2}{2m_e}\nabla_i^2+\frac{1}{2}\sum_{j\neq i}^{N}\sum_{i=1}^{N}\left(\frac{e^2}{4\pi\epsilon_0}\right)\frac{1}{|\mathbf{r}_ i-\mathbf{r}_ j|}-\sum_{i=1}^{N}\sum_{\alpha=1}^{K}\left(\frac{e^2}{4\pi\epsilon_0}\right)\frac{Z_\alpha}{|\mathbf{r}_ i-\mathbf{R}_ \alpha|}\right)\Psi=E\Psi$$

Bottom left (two equations):

$$\frac{d\mathbf{x}_ i}{dt}=\mathbf{v}_ i$$

$$m_i\frac{d\mathbf{v}_ i}{dt}=\mathbf{F}_ i$$

Bottom centre:

$$F=G\frac{m_1m_2}{r^2}$$

Bottom right (four equations, aligned at the equals signs):

$$\nabla\cdot\mathbf{E}=\frac{\rho}{\varepsilon_0}$$

$$\nabla\cdot\mathbf{B}=0$$

$$\nabla\times\mathbf{E}=-\frac{\partial\mathbf{B}}{\partial t}$$

$$\nabla\times\mathbf{B}=\mu_0\left(\mathbf{J}+\varepsilon_0\frac{\partial\mathbf{E}}{\partial t}\right)$$

No words other than the title are printed.

*Figure: no*

## Slide 3 — Magnetic dipole moment of the electron

Text: "Magnetic dipole moment of the electron"; "Theory:" (orange); "g/2 = 1.001 159 652 181 13 (±86)"; "Experiment:" (orange); "g/2 = 1.001 159 652 180 73 (±28)".

At the left, a small illustration: a light blue sphere with a blue outline, a thick blue arrow passing through it pointing up and to the right, and a red curved arrow circling around it.

*Figure: yes — illustration of a spinning sphere with an axis arrow beside the theory and experiment values of g/2*

## Slide 4 — Dirac quotation (no printed title)

Text (italic, orange): "The underlying physical laws necessary for the mathematical theory of a large part of physics and the whole of chemistry are thus completely known."

"The difficulty is only that the exact application of these laws leads to equations much too complicated to be soluble."

Attribution (white, lower right): "Paul Dirac, 1929"

The left 38% of the slide is a black-and-white photograph of a young man with dark hair and a moustache, in a dark jacket, white shirt and tie, looking to the right. No caption names him; the attribution is printed on the right.

*Figure: yes — a black-and-white portrait photograph beside the quotation; the slide does not caption it*

## Slide 5 — Scientific discovery

![Slide 5 — Scientific discovery](../images/08-ai-for-science/slide-5.png)

Text: "Scientific discovery"

Diagram on black with pale blue-grey ellipses (dark blue text), white arrows, orange "AI" labels, and one blue cloud. Nodes:
- A blue cloud at top left: "Other scientists & collective knowledge". Two white arrows between the cloud and "Scientist" (one pointing up toward the cloud, one pointing down toward Scientist).
- Ellipse "Scientist" (left); ellipse "Hypothesis" (top centre); ellipse "Observation" (bottom centre); ellipse "Experiment" (right of centre); ellipse "Simulator" (further right); an orange-filled ellipse "AI Emulator" (far right).
- Arrows: Scientist to Hypothesis (curved, upward); Hypothesis to Experiment, Hypothesis to Simulator, and Hypothesis to AI Emulator (three curved arrows from Hypothesis ending at the top of each); Experiment, Simulator and AI Emulator each to Observation (three curved arrows converging on the right of Observation); Observation to Scientist (curved, upward).
- Four orange bold "AI" labels: below Hypothesis, below-left of Scientist (left of the Scientist/Observation arrow), left of the Experiment-to-Observation arrow, and below Observation.

The figure shows the scientific discovery loop with AI marked at several points, and the AI emulator as a third route beside experiment and simulator.

*Figure: yes — scientific discovery loop (scientist, hypothesis, experiment/simulator/AI emulator, observation) with "AI" labels at several places*

## Slide 6 — The 'no-free-lunch' theorem

![Slide 6 — The 'no-free-lunch' theorem](../images/08-ai-for-science/slide-6.png)

Text: "The 'no-free-lunch' theorem" (curly single quotes as printed)

Two balance-scale drawings. Each has a thin white beam resting on a blue triangular fulcrum, a grey triangle at each end of the beam, and orange bold labels under the triangles.
- Left scale, caption "Large language models" (teal): the beam is tilted so its right end is higher. The left (lower) grey triangle is labelled "Data"; the right (higher) grey triangle is labelled "Inductive bias".
- Right scale, caption "Scientific AI models" (teal): the beam is tilted so its left end is higher. The left (higher) grey triangle is labelled "Data"; the right (lower) grey triangle is labelled "Inductive bias".

The figure shows the balance tipped toward data for large language models and toward inductive bias for scientific AI models.

*Figure: yes — two tilted balance scales: data outweighs inductive bias for LLMs, inductive bias outweighs data for scientific AI models*

## Slide 7 — Inductive bias

![Slide 7 — Inductive bias](../images/08-ai-for-science/slide-7.jpg)

Text: "Inductive bias"

Top: the Schrödinger-type equation, as on slide 2:

$$\left(-\sum_{i=1}^{N}\frac{\hbar^2}{2m_e}\nabla_i^2+\frac{1}{2}\sum_{j\neq i}^{N}\sum_{i=1}^{N}\left(\frac{e^2}{4\pi\epsilon_0}\right)\frac{1}{|\mathbf{r}_ i-\mathbf{r}_ j|}-\sum_{i=1}^{N}\sum_{\alpha=1}^{K}\left(\frac{e^2}{4\pi\epsilon_0}\right)\frac{Z_\alpha}{|\mathbf{r}_ i-\mathbf{R}_ \alpha|}\right)\Psi=E\Psi$$

Bottom left: orange heading "Invariance, equivariance". Below it a ball-and-stick molecule (dark grey, white and one red atom; a six-membered ring with a red atom and a white atom attached at the top), a teal curved arrow arching over it from left to right, a teal straight arrow pointing right, and then the same molecule rotated (the red atom now at the right side). Beneath, in orange italic: "Geometrical deep learning".

Bottom right: orange heading "Conservation laws:" followed by white lines "Energy", "Mass", "Momentum", "Electric charge", "…".

*Figure: yes — a ball-and-stick molecule and its rotated copy joined by arrows, illustrating invariance/equivariance*

## Slide 8 — The Bitter Lesson

(No slide title of its own: the page is a screenshot of Rich Sutton's essay.)

Text: a screenshot of a web page, black serif text on a white column centred on a black slide, cut off at the bottom of the slide. Visible text:

"The Bitter Lesson" (largest heading)

"Rich Sutton"

"March 13, 2019"

"The biggest lesson that can be read from 70 years of AI research is that general methods that leverage computation are ultimately the most effective, and by a large margin. The ultimate reason for this is Moore's law, or rather its generalization of continued exponentially falling cost per unit of computation. Most AI research has been conducted as if the computation available to the agent were constant (in which case leveraging human knowledge would be one of the only ways to improve performance) but, over a slightly longer time than a typical research project, massively more computation inevitably becomes available. Seeking an improvement that makes a difference in the shorter term, researchers seek to leverage their human knowledge of the domain, but the only thing that matters in the long run is the leveraging of computation. These two need not run counter to each other, but in practice they tend to. Time spent on one is time not spent on the other. There are psychological commitments to investment in one approach or the other. And the human-knowledge approach tends to complicate methods in ways that make them less suited to taking advantage of general methods leveraging computation. There were many examples of AI researchers' belated learning of this bitter lesson, and it is instructive to review some of the most prominent."

"In computer chess, the methods that defeated the world champion, Kasparov, in 1997, were based on massive, deep search. At the time, this was looked upon with dismay by the majority of computer-chess researchers who had pursued methods that leveraged human understanding of the special structure of chess. When a simpler, search-based approach with special hardware and software proved vastly more effective, these human-knowledge-based chess researchers were not good losers. They said that ``brute force" search may have won this time, but it was not a general strategy, and anyway it was not how people played chess. These researchers wanted methods based on human input to win and were disappointed when they did not." (the opening quotation mark is printed as two backticks and the closing one as a straight double quote, as in the source essay)

"A similar pattern of research progress was seen in computer Go, only delayed by a further 20 years. Enormous initial efforts went into avoiding search by taking advantage of human knowledge, or of the special features of the game, but all those efforts proved irrelevant, or worse, once search was applied effectively at scale. Also important" (the next line is cut off at the bottom edge of the slide; only the tops of the letters of "was the use of learning by self play to learn a value function (as it was in many other games and even in chess" are visible and the rest is not shown)

*Figure: yes — screenshot of the first part of Rich Sutton's "The Bitter Lesson" essay (March 13, 2019), cropped at the bottom*

## Slide 9 — Deep learning emulators

![Slide 9 — Deep learning emulators](../images/08-ai-for-science/slide-9.jpg)

Text: "Deep learning emulators"

Top: the same Schrödinger-type equation as on slide 2:

$$\left(-\sum_{i=1}^{N}\frac{\hbar^2}{2m_e}\nabla_i^2+\frac{1}{2}\sum_{j\neq i}^{N}\sum_{i=1}^{N}\left(\frac{e^2}{4\pi\epsilon_0}\right)\frac{1}{|\mathbf{r}_ i-\mathbf{r}_ j|}-\sum_{i=1}^{N}\sum_{\alpha=1}^{K}\left(\frac{e^2}{4\pi\epsilon_0}\right)\frac{Z_\alpha}{|\mathbf{r}_ i-\mathbf{R}_ \alpha|}\right)\Psi=E\Psi$$

Below it, a thick teal arrow points down from the equation to a rounded grey box labelled "Training data". A thick teal arrow points right from that box to a drawn fully connected neural network: a purple input layer (4 circles, two above and two below a column of vertical dots), then a tall teal layer, a shorter teal layer, a "…" gap, another teal layer, and a small green output layer of 2 circles with dots; thin white lines connect adjacent layers. White text to the right of the network: "deep learning *emulator*" ("emulator" in italics).

*Figure: yes — equation, arrow to "Training data", arrow to a neural network labelled "deep learning emulator"*

## Slide 10 — Benefits of emulators

Text: "Benefits of emulators". Six lines of white text, without bullets:

"Train on *synthetic* data generated by simulation"
"Data is richly and perfectly labelled"
"No GDPR or privacy issues"
"Quantity limited “only” by compute budget"
"Exploitation of under-utilized compute resources"
"*Massive acceleration* compared to simulation ≈ $10^3 - 10^{4+}$"

*Figure: no*

## Slide 11 — Spiral storm over the ocean (no printed title)

No text is printed on this slide. A full-slide satellite-style image: a hurricane-like spiral of white cloud over a dark blue ocean, with land at the upper left (part of North America and Central America, green and tan) and a strip of coast at the lower left.

*Figure: yes — full-slide satellite-style image of a large spiral storm over an ocean beside the Americas*

## Slide 12 — A foundation model for the Earth system

(No slide title of its own: the page is a screenshot of a Nature article.)

Text: a screenshot of the first page of a journal article on a white page, centred on black and cut off at the bottom. Printed text:

"nature"
"Article"
"A foundation model for the Earth system"

Left column: "https://doi.org/10.1038/s41586-025-09005-y"; "Received: 28 May 2024"; "Accepted: 9 April 2025"; "Published online: 21 May 2025"; "Open access"; "Check for updates" (with a small icon).

Authors: "Cristian Bodnar^{1,2,11}, Wessel P. Bruinsma^{1,11}, Ana Lucic^{1,3,11}, Megan Stanley^{1,11}, Anna Allen^{4,11}, Johannes Brandstetter^{1,5}, Patrick Garvan^{1}, Maik Riechert^{1}, Jonathan A. Weyn^{6}, Haiyu Dong^{6}, Jayesh K. Gupta^{2,7}, Kit Thambiratnam^{6}, Alexander T. Archibald^{4}, Chun-Chieh Wu^{8}, Elizabeth Heider^{1}, Max Welling^{1,3}, Richard E. Turner^{1,4,9} & Paris Perdikaris^{1,10}" followed by an envelope symbol (superscripts checked in an enlarged crop).

Abstract: "Reliable forecasting of the Earth system is essential for mitigating natural disasters and supporting human progress. Traditional numerical models, although powerful, are extremely computationally expensive^1. Recent advances in artificial intelligence (AI) have shown promise in improving both predictive performance and efficiency^{2,3}, yet their potential remains underexplored in many Earth system domains. Here we introduce Aurora, a large-scale foundation model trained on more than one million hours of diverse geophysical data. Aurora outperforms operational forecasts in predicting air quality, ocean waves, tropical cyclone tracks and high-resolution weather, all at orders of magnitude lower computational cost. With the ability to be fine-tuned for diverse applications at modest expense, Aurora represents a notable step towards democratizing accurate and efficient Earth system predictions. These results highlight the transformative potential of AI in environmental forecasting and pave the way for broader accessibility to high-quality climate and weather information."

Start of the body, two columns, cut off at the bottom: left column "Earth system forecasts are indispensable tools for human societies, as evidenced by recent natural events such as the floods in Valencia, the air quality crisis in New Delhi and hurricanes Helene and Milton in the eastern United States. Such systems not only provide crucial early warnings for extreme events but are also important for diverse applications ranging from agriculture to healthcare to global commerce. Modern Earth system predictions rely on complex models developed using centuries of accumulated physical knowledge, providing global forecasts of diverse variables for weather, air quality, ocean currents, sea ice and hurricanes." Right column: "medium-range weather forecasting at 0.25° resolution, leaving substantial gaps in other essential areas, including ocean dynamics, wave modelling and atmospheric chemistry. Furthermore, the potential for machine learning to outperform complex extreme weather prediction systems, which at present rely on human analysis of a wide range of models, remains underexplored." and "In this paper, we introduce Aurora, a foundation model for the Earth system, capable of tackling a variety of forecasting tasks. Taking inspiration from recent successes of foundation models in other fields^{4,5}, we first pretrain Aurora on more than one million hours of diverse Earth" (the last line is cut off at the slide's bottom edge).

*Figure: yes — screenshot of the first page of the Nature article "A foundation model for the Earth system", cropped at the bottom*

## Slide 13 — Aurora

![Slide 13 — Aurora](../images/08-ai-for-science/slide-13.jpg)

Text: "Aurora"

A rendering of the globe on black, seen from above the Pacific: the ocean is dark grey, Australia and New Zealand are shaded tan and green with black outlines, white at the poles, and an orange-red patch over East Asia at the upper left. The globe has no printed labels, legend or colour scale.

*Figure: yes — a globe centred on the Pacific with Australia, New Zealand and part of East Asia shaded by colour, no labels*

## Slide 14 — Molecules and materials

Text: "Molecules and materials"

A grid of eight pictures, 4 across and 2 down, each with a white caption beneath it.

Top row:
- "Semiconductors": a photograph of a silicon wafer being handled by robotic arms, with a blue network-of-dots graphic.
- "Drugs": a blue skeletal chemical structure on white (three rings: a benzene ring fused to a seven-membered ring, and a separate ring carrying the "Cl"; an NO₂ group, "NH", "N" and a carbonyl "O" are printed within it).
- "CO₂ capture" (printed with a subscript 2): a photograph of a large industrial structure with rows of round fans and two people standing in front of it.
- "Superconductors": a render of a small disc floating above a glowing ring with a light beam above it.

Bottom row:
- "Energy storage": a photograph of a machine with blue hoses and metal parts, with "H₂" (subscript 2) on a white plate on its cover.
- "Catalysts": a dark image of a sphere made of scattered tiny dots, mostly white with some orange.
- "Proteins": a rainbow-coloured ribbon-diagram of a protein on a white background.
- "Batteries": a photograph of four glass test tubes holding white powder.

*Figure: yes — eight-picture grid of application areas: semiconductors, drugs, CO2 capture, superconductors, energy storage, catalysts, proteins, batteries*

## Slide 15 — MatterGen

![Slide 15 — MatterGen](../images/08-ai-for-science/slide-15.jpg)

Text: "MatterGen" (title, teal). At the right, a screenshot of a journal article first page (white page, cut off at the bottom and on the right edge of the slide). Printed text on it:

"nature"
"Article"
"A generative model for inorganic materials design"

Left column: "https://doi.org/10.1038/s41586-025-08628-5"; "Received: 17 January 2024"; "Accepted: 10 January 2025"; "Published online: 16 January 2025"; "Open access"; "Check for updates".

Authors: "Claudio Zeni^{1,8}, Robert Pinsler^{1,8}, Daniel Zügner^{2,8}, Andrew Fowler^{1,8}, Matthew Horton^{3,8}, Xiang Fu^{1}, Zilong Wang^{4}, Aliaksandra Shysheya^{1}, Jonathan Crabbé^{1}, Shoko Ueda^{1}, Roberto Sordillo^{1}, Lixin Sun^{1}, Jake Smith^{3}, Bichlien Nguyen^{3}, Hannes Schulz^{2}, Sarah Lewis^{1}, Chin-Wei Huang^{5}, Ziheng Lu^{6}, Yichi Zhou^{7}, Han Yang^{6}, Hongxia Hao^{6}, Jielan Li^{6}, Chunlei Yang^{4}, Wenjie Li^{4}, Ryota Tomioka^{1,8} & Tian Xie^{1,8}", each of the last two followed by an envelope symbol (superscripts checked in an enlarged crop; the text layer holds none of the article text). The title wraps after "materials".

Abstract: "The design of functional materials with desired properties is essential in driving technological advances in areas such as energy storage, catalysis and carbon capture^{1–3}. Generative models accelerate materials design by directly generating new materials given desired property constraints, but current methods have a low success rate in proposing stable crystals or can satisfy only a limited set of property constraints^{4–11}. Here we present MatterGen, a model that generates stable, diverse inorganic materials across the periodic table and can further be fine-tuned to steer the generation towards a broad range of property constraints. Compared with previous generative models^{4,12}, structures produced by MatterGen are more than twice as likely to be new and stable, and more than ten times closer to the local energy minimum. After fine-tuning, MatterGen successfully generates stable, new materials with desired chemistry, symmetry and mechanical, electronic and magnetic properties. As a proof of concept, we synthesize one of the generated structures and measure its property value to be within 20% of our target. We believe that the quality of generated materials and the breadth of abilities of MatterGen represent an important advancement towards creating a foundational generative model for materials design."

Start of body, cut off at the bottom: "The rate at which we can discover better materials has a substantial impact on the pace of technological innovation in areas such as carbon capture, semiconductor design and energy storage^{1–3}. Traditionally, most materials have been discovered through experi-" (continues, partly cropped); right column: "fall short of producing stable materials according to density functional theory (DFT) calculations^{4,5,31}, are constrained by a narrow subset of elements^{7,9} and/or can only optimize a very limited set of properties, mainly formation energy^{4,5,8,11,31,32}." (cropped at the bottom edge).

At the left, a 3D rendering of a crystal unit cell drawn as a thin white-lined box (two cells deep along each side, so a 2×2×2 block), filled with large salmon/orange-pink spheres, medium green spheres and small red spheres; no labels.

*Figure: yes — rendering of a crystal cell with orange, green and red spheres, beside a screenshot of the Nature article "A generative model for inorganic materials design"*

## Slide 16 — Hazy blobs in a crystal cell (no printed title)

No text is printed. On black, a blurred, translucent grey-teal cloud of roughly spherical blobs inside a thin white-lined parallelepiped box (a skewed box divided into two layers and about 2×2 cells), seen at an angle.

*Figure: yes — a hazy cloud of blobs inside a skewed wireframe box, no labels*

## Slide 17 — Grid of crystal structures (no printed title)

![Slide 17 — Grid of crystal structures (no printed title)](../images/08-ai-for-science/slide-17.jpg)

No text is printed. On black, a grid of 12 rows by 22 columns of small 3D ball-and-stick crystal-structure renderings, each in its own colours (green, orange, red, blue, purple, pink, grey, yellow and others) and each a different shape and size of cluster. There are no labels, captions or axes.

*Figure: yes — grid of about 264 small, differently coloured crystal-structure renderings (12 rows by 22 columns)*

## Slide 18 — Fundamental trilemma

![Slide 18 — Fundamental trilemma](../images/08-ai-for-science/slide-18.jpg)

Text: "Fundamental trilemma"; "Accuracy"; "Speed"; "Generality"; "Chemical accuracy: 1kcal/mol" (orange).

At the left, three white arrows from a common origin: one pointing up labelled "Accuracy", one pointing right labelled "Speed", and one pointing down-left labelled "Generality" (a 3D-axes drawing). At the right, a flat cartoon illustration of a pirate ship (red hull with cannons and an anchor, black sail with a skull and crossbones, black flag, a small figure on the deck) on green waves under a blue sky with clouds. The orange caption "Chemical accuracy: 1kcal/mol" is below the illustration.

*Figure: yes — three-axis diagram (Accuracy, Speed, Generality) next to a cartoon pirate ship captioned "Chemical accuracy: 1kcal/mol"*

## Slide 19 — Wavefunction

![Slide 19 — Wavefunction](../images/08-ai-for-science/slide-19.jpg)

Text: "Wavefunction"

$$\Psi(\mathbf{x}_ 1,\ \ldots,\ \mathbf{x}_ N)$$

At the lower left, a diagram on a white panel, in red, with three parts drawn left to right:
- $D=1$: a horizontal line with an arrow axis labelled $x_1$ and four red tick marks.
- $D=2$: a pair of axes labelled $x_2$ (vertical) and $x_1$ (horizontal) with a red 3×3 grid of squares.
- $D=3$: a 3D axis system with $x_2$ up, $x_1$ to the right and $x_3$ toward the lower left, with a stepped stack of red cubes (dashed hidden edges) filling the corner.
The diagram shows the number of grid cells growing as the dimension $D$ increases.

At the lower right, a rendering of a ball-and-stick molecule on black: grey, blue, red and white balls joined by grey sticks, containing a six-membered ring fused to a five-membered ring, with white balls on the outside. No labels.

*Figure: yes — grids of red cells for D=1, 2, 3 (growth with dimension) and a ball-and-stick molecule*

## Slide 20 — DFT: density functional theory (1965)

![Slide 20 — DFT: density functional theory (1965)](../images/08-ai-for-science/slide-20.jpg)

Text: "DFT: density functional theory (1965)"

$$\Psi(\mathbf{x}_ 1,\ \ldots,\ \mathbf{x}_ N)\rightarrow\rho(\mathbf{x})$$

Two white rounded boxes joined by a blue arrow pointing right: left box "Computational cost $\mathbf{exp}(N)$" and right box "Computational cost $N^3$" (the formula parts are bold red, the words grey-teal). Below the arrow, in orange: "Exact!"

Bottom row, three images:
1. A black-and-white photograph of an older man with glasses wearing a jacket and tie; caption inside the picture: "Photo from the Nobel Foundation archive." and "Walter Kohn". Next to it, a small image of a gold medal showing a bearded profile (no text readable).
2. A bar chart (teal bars) of citations per year. Y axis (on the right side), label "citations / year", ticks 0, 5,000, 10,000, 15,000, 20,000. X axis label "year", ticks 1990, 2000, 2010, 2020. One series: a bar per year from 1987 (about 200) to 2022, rising slowly through the 1990s to about 1,600 in 2000, then about 6,300 in 2010, 10,500 in 2015, 15,500 in 2019 and 16,800 in 2020, and ending at about 17,800 in 2022 (values read by eye from an enlarged crop).
3. A pie chart in teal shades with the largest slice pulled out. Labelled slices, with approximate shares read by eye: "Density Functional Theory" (the largest, bright teal, about 30%, pulled out), "Lattice QCD" (grey-teal, about 20%), "Climate" (dark teal, about 15%), "Fusion PIC" (about 10%), "Scalable Solvers" (about 9%), "N-Body (MD)" (about 8%). Seven thin unlabelled slices follow, 13 slices in all (counted in an enlarged crop; going on from "N-Body (MD)": medium teal about 5%, dark teal about 3%, pale grey about 2%, pale cyan about 1%, near-white about 1%, dark teal about 1%, near-black about 0.5%). The pie prints no percentages and no title or source.

*Figure: yes — exp(N) to N^3 cost boxes, photo of Walter Kohn with a medal, bar chart of DFT citations per year to about 17,800, and a pie chart in which Density Functional Theory is the largest slice*

## Slide 21 — Ball-and-stick model and its shadow (no printed title)

![Slide 21 — Ball-and-stick model and its shadow (no printed title)](../images/08-ai-for-science/slide-21.jpg)

No text is printed. A full-slide photograph of a large model made of coloured balls (black, grey, white, orange, red, blue, purple, yellow, green) and sticks, standing on a white surface against a black and white background; its dark shadow on the wall at the right forms large blotchy shapes that read as the letters "D", "F" and "T" (a reading of the picture, confirmed in an enlarged crop; not printed as text). Loose balls lie on the surface in front.

*Figure: yes — photograph of a large ball-and-stick molecular model whose shadow on a wall spells out DFT*

## Slide 22 — What is the catch?

![Slide 22 — What is the catch?](../images/08-ai-for-science/slide-22.jpg)

Text: "What is the catch?"; "Exchange-correlation functional $E_{\mathrm{XC}}[\rho]$" (printed as $E_{XC}[ρ]$, with the "ρ" in upright type and the brackets upright); under the left images "It's universal!"; under the middle image "Handcrafted functionals with limited accuracy – “Jacob’s ladder”".

Left: four hexagonal tiles (light grey) each holding a ball-and-stick molecule or crystal rendering (the top-left one has an orange atom, a teal atom and several grey and red atoms; the top-right one is a small ring with a red atom and a white atom; the bottom-left one is a grid-like arrangement of black, green and lilac spheres; the bottom-right one has grey, blue, red, yellow and white atoms).

Middle: a word cloud on a white rectangle, in grey and black, of density-functional names in many sizes. The larger readable words: "B3LYP", "PBE", "LYP", "EXX", "LSDA", "BP86", "PZ81", "VWN5", "B88", "TPSS", "RPA", "EB08", "LM81", "PW91", "PBEsol", "PBE0", "LC-wPBE", "AM05", "G96", "CAM-B3LYP", "HSE", "revPBE", "rPBE", "wigner", "BJ06", "MCY06". The smaller words, legible in an enlarged crop: "wB97", "OBPW", "X3LYP", "PW92", "SAOP", "BNL05", "M06-L", "KMLYP", "TLYP", "V5LYP", "LB9483", "VP86", "WC06", "wB97XD", "wB97X", "B2PLYP", "BMK04", "BOP", "B97", "FT97", "GL76", "WI", "B97-2", "PBEOP", "CS1", "Bh3LYP", "rB86", "GV09", "TPSSh", "WL", "KT2", "xPBE", "muB88", "M06-2X", "M06-HF", "HCTH", "HL71", "PKZB99", "OPTX", "DK87", "vBH", "M05-2X", "BR89", "mPW", "muPBE", "LRC-wPBE0", "PL81", "LG93", "KCIS", "KT1", "lhf", "O3LYP", "SOGGA", "BRC89", "B95", "B97-D", "B86-mgc", "VS98", "B94", "PK06", "EDF1", "GG99", "PW86", "B97-1", "EDF2", "mPBE", "wPBE", "VWN1", "KT3", and a word cut off at the right edge after "M0".

Right: a screenshot of a web page of a journal article (cropped at the bottom and right). Header: "Science", "Current Issue", "First release papers", "Archive", "About ∨". Breadcrumb: "HOME > SCIENCE > VOL. 298, NO. 5594 > IN PURSUIT OF THE "DIVINE" FUNCTIONAL" (straight quotes). Tag "PERSPECTIVES"; title "In Pursuit of the "Divine" Functional"; author line "ANN E. MATTSSON" and a link "Authors Info & Affiliations"; "SCIENCE • 25 Oct 2002 • Vol 298, Issue 5594 • pp. 759-760 • DOI: 10.1126/science.1077710"; a download count "187". Below, the start of the article in a "SCIENCE'S COMPASS • PERSPECTIVES" banner: "PERSPECTIVES: DENSITY FUNCTIONAL THEORY"; "In Pursuit of the “Divine” Functional"; "Ann E. Mattsson"; a drop-cap paragraph beginning "Paul Dirac reputedly said that the Schrödinger equation (SE) marked the end of chemistry: All answers could be calculated from the SE. ..." The rest of the article (three narrow columns and a figure at the bottom labelled "Water/CH3OH" and "Pt") is legible only in an enlarged crop. The drop-cap paragraph continues: "The SE can indeed be solved exactly for some systems, such as the hydrogen atom, and numerically to arbitrary precision for systems with a small number of electrons. However, the many-body character of the SE sets a fundamental limit on the size of solvable systems (1). In a seminal paper, Hohenberg and Kohn (2) showed in 1964 that the SE, formulated as an equation of an N-electron wave function of 3N variables, could be reformulated as an equation of the electron …" (cut off). The other columns discuss the local density approximation and note that "Walter Kohn was awarded half of the 1998 Nobel Prize in Chemistry (the other half was awarded to John Pople)". The web page also shows share icons (f, a bird, in), bell, bookmark and quotation-mark icons, and a red button with a lock, cut off after "CH".

*Figure: yes — four molecule tiles, a word cloud of density functional names, and a screenshot of Science's "In Pursuit of the "Divine" Functional" (2002)*

## Slide 23 — The DFT zoo

![Slide 23 — The DFT zoo](../images/08-ai-for-science/slide-23.jpg)

Text: "The DFT zoo"

A chart pasted as a white panel. A scatter plot with a red curve. Axes: the y axis has ticks 0, 2, 4, 6, 8, 10, 12; no y-axis label is visible on the page (checked in an enlarged crop), although the text layer holds the string "Weighted MAE (kcal/mol)". The x axis has four labelled positions: $N^3$, $N^3$ (larger prefactor) (printed "N³ ( larger prefactor)", with a space after the parenthesis), $N^4$, $N^5$. A blue band across the bottom from y = 0 to about 1 is labelled "Chemical accuracy" (white text). Legend (top right): dark blue dot "2 features"; brown dot "3 features"; light blue dot "4 features"; pink dot "5 features".

Four data points (one series per feature count; values read by eye):
- dark blue "2 features", labelled "revPBE-D3": at $N^3$, y about 8.7.
- brown "3 features", labelled "B97M-rV": at $N^3$ (larger prefactor), y about 6.7.
- light blue "4 features", labelled "wB97M-V": at $N^4$, y about 3.7.
- pink "5 features", labelled "wB97M(2)": at $N^5$, y about 2.0.

A red curve (not a data series) starts at the left near y about 8.2 above $N^3$, falls steeply and then roughly linearly down to about y 1.8 just left of the pink point. Near the lower left, a gold Nobel-medal image and, in red, the label "Universal functional" above the blue band.

*Figure: yes — chart of error versus computational scaling for four DFT functionals, with a falling red curve and a "Universal functional" label near the chemical-accuracy band*

## Slide 24 — Skala functional

![Slide 24 — Skala functional](../images/08-ai-for-science/slide-24.jpg)

Text: "*Skala* functional" ("Skala" in italics); "arXiv:2506.14665" (white, underlined link, top right); "Electron density"; "Non-locality through message-passing"; $E_{XC}$ (printed "E" italic with subscript "XC"); "Energy"; "Hartree energy, KS kinetic energy, electron-nucleus Coulomb potential".

Top left: a small cream-coloured cartoon of a ladder with a face, arms and legs, running, with a red "S" on its front.

Flow diagram: a picture labelled "Electron density" (a translucent plane and grey translucent blobs with pink, orange and blue colour clouds) points via a white arrow to a picture labelled "Non-locality through message-passing" (purple dot clusters with green-yellow centres arranged around a translucent plane); a white arrow leads to $E_{XC}$; a white arrow leads to "Energy". A separate white line starts under "Electron density", runs along the bottom of the slide, and turns up with an arrow into "Energy"; it is labelled "Hartree energy, KS kinetic energy, electron-nucleus Coulomb potential".

*Figure: yes — Skala pipeline: electron density, message-passing non-locality, E_XC, energy, plus a bypass path for Hartree, KS kinetic and electron-nucleus terms*

## Slide 25 — Errors of eight functionals (no printed title)

![Slide 25 — Errors of eight functionals (no printed title)](../images/08-ai-for-science/slide-25.jpg)

No text is printed outside the chart, which sits on a white panel.

Scatter plot. X axis: "Error on general main-group chemistry [kcal/mol]", ticks 0 to 8. Y axis: "Error on atomization energies [kcal/mol]", ticks 0 to 8. Grey grid. Dashed black lines at x = 1 and at y = 1; light green shading for x < 1 and for y < 1; the label "Chemical accuracy" sits in the lower right inside the shaded band. Legend "Functional class": grey-brown swatch "GGA"; orange swatch "meta-GGA"; purple swatch "Non-local meta-GGA"; teal swatch "Hybrid". Legend "Nominal complexity": circle $O(N^3)$; triangle $O(N^4)$. Eight labelled points (x, y read by eye):
- "revPBE": grey-brown circle (GGA), about (8.3, 8.05).
- "r²SCAN": orange circle (meta-GGA), about (7.25, 4.45).
- "B3LYP": teal triangle (hybrid), about (6.4, 3.8).
- "B97M-V": orange circle (meta-GGA), about (5.55, 2.85).
- "M06-2X": teal triangle (hybrid), about (4.85, 3.0).
- "ωB97X-V": teal triangle (hybrid), about (3.95, 2.6).
- "ωB97M-V": teal triangle (hybrid), about (3.2, 2.05).
- "Skala" (bold purple): purple circle (non-local meta-GGA), about (3.9, 1.05), just above the y = 1 dashed line.

*Figure: yes — scatter plot of errors for eight functionals; Skala is the lowest, near the 1 kcal/mol chemical accuracy line on the atomization energies axis*

## Slide 26 — Molecular biology

![Slide 26 — Molecular biology](../images/08-ai-for-science/slide-26.jpg)

Text: "Molecular biology"; "Sequence"; "Structure"; "Function".

Three pictures left to right joined by white arrows pointing right, each with a white caption below:
- "Sequence": a small white panel of rows of coloured letters (a genetic-sequence listing) with line numbers on the left (such as "12853800"); the letters are illegible at 1280×720.
- "Structure": a blue ribbon rendering of a folded protein with a small grey molecule and a red patch at its centre and a small orange stick.
- "Function": a pale blue rounded panel containing a cycle diagram of red and green space-filling protein shapes. Printed labels: "ADP" (red, with a red arrow up), "ATP" (green, with a green arrow), "Opening", "Closing", "Dissociation", "Binding" (blue text along arrows), a blue rounded box "Net cycle due to energy input", and below the panel, in red: "Net entropy production", "Phosphate", "Heat" (the last two with red arrows pointing down). The figure shows a cycle that goes from open to closed protein forms and back, with ATP going in and ADP leaving.

*Figure: yes — sequence, structure and function pictures joined by arrows, the last a protein cycle diagram labelled with ATP, ADP, opening, closing, dissociation and binding*

## Slide 27 — Molecular dynamics (MD) simulation

![Slide 27 — Molecular dynamics (MD) simulation](../images/08-ai-for-science/slide-27.jpg)

Text: "Molecular dynamics (MD) simulation"

Left: a white panel with a rendering of a small molecular cluster of larger red balls and smaller blue balls joined by grey sticks. One blue ball has a black arrow from it pointing up and to the right; the label $\mathbf{x}_ i$ is placed beside the start of the arrow and $\mathbf{v}_ i$ at its tip.

Right: a white panel with two equations, the second one's right-hand side boxed in red:

$$\frac{d\mathbf{x}_ i}{dt}=\mathbf{v}_ i$$

$$m_i\frac{d\mathbf{v}_ i}{dt}=\boxed{-\nabla_i U(\mathbf{x}_ 1,\ \ldots,\ \mathbf{x}_ N)}$$

*Figure: yes — ball-and-stick cluster with position and velocity labelled for one atom, beside the equations of motion with the force term −∇_i U boxed in red*

## Slide 28 — Curse of sequentiality

![Slide 28 — Curse of sequentiality](../images/08-ai-for-science/slide-28.jpg)

Text: "Curse of sequentiality"; "Integration step"; "desired simulation timespan"; "Simulations with current MD technology require $10^6$ to $10^{15}$ sequential steps"; "But: chips no longer become faster for sequential computation".

Footer: at the lower right, small white text "Figure from “Cell Biology by the numbers”" (the title in quotes is underlined, a link). It appears only on this slide.

Figure: a pasted timeline on a white panel. A green arrow runs left to right along the bottom, labelled with ticks "10⁻¹⁵ (fs)", "10⁻¹² (ps)", "10⁻⁹ (ns)", "10⁻⁶ (µs)", "10⁻³ (ms)", "10⁰", and the label "time (seconds)" at the lower right. Dots on the arrow are joined by bracket lines to text labels for biological processes, in rough left-to-right order of time: "bond vibrations"; "exciton migration"; "photosynthetic charge separation"; "photosynthetic electron transfer"; "signal transduction in vision"; "helix-coil transitions"; "ion channel gating; diffusion across synapse"; "protein folding →" (arrow pointing right); "ligand binding →" (arrow pointing right); "rotation of flagella; ATP synthase"; "average enzyme catalytic turnover".

Added on top of the figure: a red arrow pointing up at the $10^{-15}$ (fs) end of the axis labelled "Integration step" (below it), and a double-headed teal arrow banner labelled "desired simulation timespan" below the axis, starting at about the $10^{-9}$ tick and ending just past the $10^0$ tick, so that it passes over $10^{-6}$ and $10^{-3}$.

*Figure: yes — timescales of biological processes from femtoseconds to seconds, with the MD integration step at the femtosecond end and the desired simulation timespan far longer*

## Slide 29 — AI²BMD

Text: "AI²BMD" (printed AI with a superscript 2, then BMD). At the right, a screenshot of a journal article first page, cropped at the bottom:

"nature"
"Article"
"Ab initio characterization of protein molecular dynamics with AI²BMD"

Left column: "https://doi.org/10.1038/s41586-024-08127-z"; "Received: 31 March 2023"; "Accepted: 26 September 2024"; "Published online: 6 November 2024"; "Open access"; "Check for updates".

Authors: "Tong Wang^{1,2,3}, Xinheng He^{1,2}, Mingyu Li^{1,2}, Yatao Li^{1,2}, Ran Bi^{1}, Yusong Wang^{1}, Chaoran Cheng^{1}, Xiangzhen Shen^{1}, Jiawei Meng^{1}, He Zhang^{1}, Haiguang Liu^{1}, Zun Wang^{1}, Shaoning Li^{1}, Bin Shao^{1,3} & Tie-Yan Liu^{1}" (superscripts tiny; envelope symbols follow the first author and Bin Shao).

Abstract: "Biomolecular dynamics simulation is a fundamental technology for life sciences research, and its usefulness depends on its accuracy and efficiency^{1–3}. Classical molecular dynamics simulation is fast but lacks chemical accuracy^{4,5}. Quantum chemistry methods such as density functional theory can reach chemical accuracy but cannot scale to support large biomolecules^{6}. Here we introduce an artificial intelligence-based ab initio biomolecular dynamics system (AI²BMD) that can efficiently simulate full-atom large biomolecules with ab initio accuracy. AI²BMD uses a protein fragmentation scheme and a machine learning force field^{7} to achieve generalizable ab initio accuracy for energy and force calculations for various proteins comprising more than 10,000 atoms. Compared to density functional theory, it reduces the computational time by several orders of magnitude. With several hundred nanoseconds of dynamics simulations, AI²BMD demonstrated its ability to efficiently explore the conformational space of peptides and proteins, deriving accurate ³J couplings that match nuclear magnetic resonance experiments, and showing protein folding and unfolding processes. Furthermore, AI²BMD enables precise free-energy calculations for protein folding, and the estimated thermodynamic properties are well aligned with experiments. AI²BMD could potentially complement wet-lab" (the next line is cut off at the bottom edge and unreadable).

At the left, on black, a ribbon rendering of a protein: an orange domain on top, a green domain below, and a red helix between them. No labels.

*Figure: yes — protein ribbon rendering (orange, green, red) beside a screenshot of the Nature article "Ab initio characterization of protein molecular dynamics with AI2BMD"*

## Slide 30 — Science cover, "PROTEIN SHAKE" (no printed title)

Text printed within the picture (a magazine cover centred on black, thin white outline): "AAAS" (small logo); "Science"; "PROTEIN" over "SHAKE"; "Generative deep learning powers emulation of protein ensembles p. 700"; bottom left: "14 AUGUST 2025"; "Can synthetic organs and AI replace animal testing? p. 676"; "Plant volatiles enhance pathogen defense through soil feedback pp. 680 & 698"; "Diamond is not the only carbon allotrope in rings p. 708".

The cover art is a swirl of red and pale-pink protein ribbon (helices) with motion blur, forming a ball-like cluster against black.

*Figure: yes — cover of Science, 14 August 2025, titled "PROTEIN SHAKE", with a blurred swirl of red and pink protein ribbons*

## Slide 31 — BishopBook.com

Text: "BishopBook.com" (blue, underlined link, top right); "Hardback: ‘stitched signatures’" (curly single quotes); "Springer-Nature’s best-selling book of 2024 and 2025!" (orange italic, curly apostrophe).

Left: a book cover image with a swirl of coloured light patterns (green, red, yellow, blue, orange); a white label "Christopher M. Bishop" and "with Hugh Bishop"; a dark blue band with the title "Deep Learning"; a white label "Foundations and Concepts"; the "Springer" logo with a horse-head symbol at lower right.

Right: a screenshot of an online document viewer (issuu-style) showing two pages of the book side by side: pages 392 and 393 of the book, legible in an enlarged crop. Running heads: "392  12. TRANSFORMERS" and "12.3. Transformer Language Models  393". The left page has Figure 12.20, captioned "Schematic illustration of a sequence-to-sequence transformer. To keep the diagram uncluttered the input tokens are collectively shown as a single box, …": an encoder (an "embedding" box for input x, a "positional encoding" sine-wave box joined at a + node, and stacked "self-attention transformer layer" boxes) and a decoder (an "embedding" box for "{<start>, Y_{1:N-1}}", a positional box, stacked "cross-attention transformer layer" boxes fed by z from the encoder, and an "LSM" box on top giving Y_N, with a dotted feedback line), each under a bracket labelled "encoder" or "decoder". Its body text begins "This use of self-supervised learning led to a paradigm shift in which a large model is first pre-trained …". The right page has Figure 12.21, "Schematic illustration low-rank adaptation showing a weight matrix W0 from one of the attention layers in a pre-trained transformer. …", with matrices X (N×D), W0 (D×D), A (D×R) and B (R×D) and the output XW0 + XAB (N×D), and equation (12.36), W-hat = W0 + AB. Viewer bar: "408-409 / 656", a progress slider, "issuu" logo and icons for search, share and full screen, with left and right arrow buttons at the sides of the pages.

*Figure: yes — cover of "Deep Learning: Foundations and Concepts" and a screenshot of an online reader showing pages 408-409 of 656*
