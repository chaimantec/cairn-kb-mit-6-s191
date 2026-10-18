# Licence and attribution

This repository is a study aid compiled from **MIT 6.S191 Introduction to Deep Learning**, 2026
edition, <https://introtodeeplearning.com/>, taught by Alexander Amini and Ava Amini.

## The course's terms

The course website states that "all materials are copyrighted and licensed under the MIT license",
linking to the licence in the course's lab repository
(<https://github.com/MITDeepLearning/introtodeeplearning/blob/master/LICENSE.md>). It asks that anyone
reusing its slides add this reference:

> © Alexander Amini and Ava Amini
> MIT 6.S191: Introduction to Deep Learning
> IntroToDeepLearning.com

That attribution applies to everything in this repository derived from the course: the slide
transcriptions in `raw/slides/`, the slide images in `raw/images/`, and the wiki in `wiki/`, which
summarises and cites them. The transcripts in `raw/transcripts/` are adapted from the YouTube captions
of the course's lecture recordings on the channel the course site links
(<https://www.youtube.com/channel/UCtslD4DGH6PKyG_1gFAX7sg>).

The course's MIT licence, as published, reads:

```
MIT License

Copyright (c) 2025 [MIT Introduction to Deep Learning](http://introtodeeplearning.com/)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:
The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

Lecture 7 is a guest lecture. Its deck, "The Three Laws of AI", is by Douglas Blank (Comet ML). It is
hosted on the course site and linked from its 2026 schedule, and carries no licence notice of its own;
material derived from it is credited to him as well as to the course.

Lecture 8 is also a guest lecture. Its deck, "AI for Science", is by Chris Bishop (Microsoft Research AI
for Science). It is hosted on the course site and linked from its 2026 schedule, and carries no licence
notice of its own; material derived from it is credited to him as well as to the course.

Lecture 9 is also a guest lecture. Its deck, "Massively Parallel Training", is by Mathias Lechner (Liquid
AI). It is hosted on the course site and linked from its 2026 schedule, and carries no licence notice of
its own; material derived from it is credited to him as well as to the course.

The original writing in this repository (the wiki prose, the slide descriptions, and the transcript
copy-edits) is offered under the same MIT licence, with the attribution above retained.

## Third-party material on the slides

The decks reproduce some figures, photographs, screenshots and logos that belong to others. The
course's licence covers the course's own material; those items remain their owners', and are
reproduced here only as they appear on the course's slides, with the credit the slide gives.

## Rendered images

Each image in `raw/images/01-introduction/`, named `slide-N.jpg`, is page N of the lecture 1 deck,
[`6S191_MIT_DeepLearning_L1.pdf`](https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L1.pdf),
extracted unmodified: the deck is a sequence of 1280×720 JPEG page images, and these are those JPEGs
byte for byte. 34 of the deck's 108 pages are included: slides 2, 7, 18, 19, 22–25, 28, 31, 32, 35,
38–41, 43, 47, 50–53, 57, 59–61, 67, 70, 72, 75, 93, 97, 98 and 106. Attribution for every one is the
course line above. Third-party material on them, as credited on the slides:

- **Slide 2** shows generated faces credited on the slide to "Goodfellow et al." (2015) and to "Karras,
  Laine, Aila." (2018); the third image is a still from the course's own 2020 introduction video.
- **Slide 72** reproduces a loss-landscape rendering captioned "Visualizing the loss landscape of
  neural nets", Dec 2017. The slide names no authors.
- **Slide 18**'s grids of learned features, and the 3D loss surfaces on slides 57–61, carry no credit
  on the slide.
- **Slide 19** shows logos (ImageNet, Wikipedia, TensorFlow, PyTorch, Keras, JAX) and a photograph of a
  graphics card, without credit; the logos are trademarks of their owners.

Not included, among others: the slides of course logistics, sponsor logos, staff portraits and prize
photographs (8–16), the stock photographs on slides 4–5, and slide 6's screenshot of an X post by Paul
Couvert (@itsPaulAi), whose text and benchmark table are transcribed in `raw/slides/` instead.

Each image in `raw/images/02-rnns-transformers-attention/`, named `slide-N.jpg`, is page N of the
lecture 2 deck,
[`6S191_MIT_DeepLearning_L2.pdf`](https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L2.pdf),
extracted unmodified in the same way. 33 of the deck's 83 pages are included: slides 3, 5, 8, 10, 11,
13, 15, 17, 24, 26, 29, 36, 42, 44, 48, 53, 54, 56, 57, 61, 64, 66, 68, 69, 71–77, 79 and 80.
Attribution for every one is the course line above. Third-party material on them, as credited on the
slides:

- **Slide 8** includes a screenshot of a 2018 tweet about the course by Ivar Hagendoorn
  (@IvarHagendoorn), a photograph of a baseball pitcher and a translation icon, without further credit.
- **Slide 44** credits "Mozer *Complex Systems* 1989." for backpropagation through time.
- **Slide 56** carries the credit "Huawei." beside its video thumbnail.
- **Slide 57** credits "Socher+, EMNLP 2013."
- **Slides 66 and 79** use a still of the Marvel character Iron Man, uncredited on the slides; the
  character and image belong to their owners.
- **Slides 68 and 69** show a YouTube search results page with third-party video thumbnails (a sea
  turtle video and a Kobe Bryant video) beside the course's own 2020 lecture.
- **Slides 72 and 75–77** credit "Vaswani+, NeurIPS 2017."
- **Slide 80** shows an image of an avocado-shaped armchair, a protein-structure rendering and a
  patch-gridded photograph of a puppy, with these citations printed under the three panels: Devlin et
  al., NAACL 2019; Brown et al., NeurIPS 2020; Jumper et al., Nature 2021; Lin et al., Science 2023;
  Dosovitskiy et al., ICLR 2020. The slide does not say who made each image.

Not included from lecture 2, among others: the stock-photo collage of slide 7, slide 58's screenshots
of two tweets by individuals (their text is transcribed in `raw/slides/`), and the thumbnail wall of
slide 67. The "H. Suresh, 6.S191 2018." credit on slides 32–34, 38, 39 and 58 is on slides that are not
included.

Each image in `raw/images/03-convolutional-neural-networks/`, named `slide-N.jpg`, is page N of the
lecture 3 deck,
[`6S191_MIT_DeepLearning_L3.pdf`](https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L3.pdf),
extracted unmodified in the same way. 33 of the deck's 70 pages are included: slides 3, 6, 12, 13, 16,
20, 22, 24, 25, 27–30, 32, 40, 41, 44, 47–52 and 56–65. Attribution for every one is the course line
above. Third-party material on them, as credited on the slides:

- **Slide 12** credits "Levin *Image Processing & Computer Vision*." for its pixel-grid portrait (the
  same portrait, uncredited, is on slide 13).
- **Slide 16** credits "Li/Johnson/Yeung C231n." for its grid of example photographs.
- **Slides 27–30** credit "Rohrer *How do CNNs work?*" for the X example.
- **Slides 32, 40 and 48** credit "Karn *Intuitive CNNs*" for the worked convolution and the ReLU
  feature maps.
- **Slide 50** credits "Lee+ *ICML* 2009." for its learned-feature visualizations.
- **Slide 57** reproduces two plots and two mammograms from "International evaluation of an AI system for
  breast cancer screening", credited "McKinney+ *Nature* 2020."
- **Slide 61** credits "Girshick+ *CVPR* 2014." (R-CNN), **slide 62** "Ren+ *IEEE* 2016." (Faster
  R-CNN), and **slide 63** "Long+ *CVPR* 2015." (fully convolutional networks).
- **Slides 6, 64 and 65** credit "Amini+ *ICRA* 2019.", the lecturer's own work on the self-driving car.
- **Slide 3**'s street photograph, **slide 41**'s portrait photograph and the taxi photographs of
  **slides 58–60** carry no credit on the slides.

Not included from lecture 3, among others: the photographs and collages of slides 2, 4, 5, 7, 8 and
67 (credited on the slides to Boston Dynamics and P. Isola 6.869; Esteva+ *Nature* 2017,
McKinney+ *Nature* 2020 and Wang+ *Sci. Rep.* 2020; and Google Project Guideline), and slide 66's video
still.

Each image in `raw/images/04-deep-generative-modeling/`, named `slide-N.jpg`, is page N of the
lecture 4 deck,
[`6S191_MIT_DeepLearning_L4.pdf`](https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L4.pdf),
extracted unmodified in the same way. 39 of the deck's 84 pages are included: slides 2, 5–10, 15–17,
22, 26, 27, 29–32, 34–37, 39–41, 49, 50, 55, 57, 60, 62, 64, 68, 70, 72, 74 and 76–79. Attribution for
every one is the course line above. Third-party material on them, as credited on the slides:

- **Slide 2** credits "Google Gemini": in the lecture, faces A and B were generated by Gemini; face C,
  the real photograph, carries no credit.
- **Slide 6** credits "Amini/Soleimany+ *AAAI/AIES* 2019." for its two grids of face photographs.
- **Slide 7** credits "Amini+ *IROS* 2018." for its driving photographs.
- **Slide 10** credits "Plato, *Republic.*" for the Myth of the Cave; the illustration itself carries no
  further credit.
- **Slides 22, 26, 27, 29, 34–37 and 39** credit "Kingma+ *ICLR* 2014."; **slide 40** credits
  "Kingma+ *ICLR* 2014; Chen+ *NeurIPS* 2018." for its grid of generated faces.
- **Slides 30–32** credit "Joseph Rocca." for the latent-space regularization diagrams.
- **Slide 41** credits "Higgins+ *ICLR* 2017." for its β-VAE face grids.
- **Slide 50** credits "Goodfellow+ *NeurIPS* 2014."
- **Slide 76** credits "Brock+ *ICLR* 2019." for its interpolated bird images.
- **Slide 78** credits "Zhu+ *ICCV* 2017." for CycleGAN and its horse-to-zebra video still.
- **Slide 5**'s photographs, **slide 8**'s ChatGPT screenshot, paintings and molecular structures,
  **slide 17**'s handwritten digits, **slide 74**'s bird photograph and **slide 79**'s waveforms and
  spectrograms carry no credit on the slides.

Not included from lecture 4, among others: slide 42 (a repeat of slide 6's face grids, with the same
credit), slide 80's video still of the course's synthesized-voice demo (captioned "Original (Amini)"
and "Synthesized (Obama)", with a "CANNYAI" logo), and the full-slide pictures of slides 82–84.

Each image in `raw/images/05-reinforcement-learning/`, named `slide-N.jpg`, is page N of the lecture 5
deck,
[`6S191_MIT_DeepLearning_L5.pdf`](https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L5.pdf),
extracted unmodified in the same way. 19 of the deck's 58 pages are included: slides 6, 10, 17, 22, 26,
30–33, 37–40, 42–45, 48 and 56. Attribution for every one is the course line above. Third-party material
on them, as credited on the slides:

- **Slides 26, 30, 32 and 33** credit "Mnih+ *Nature* 2015.": slide 32's network diagram and slide 33's
  chart of Atari results are reproduced from that work.
- **Slide 42** credits "Williams *Reinforcement Learning* 1992." for the training algorithm beside its
  trajectory drawing (slides 43–45 repeat the algorithm without the credit).
- **Slide 48** credits "Amini+ *IEEE RA-L* 2020.", the lecturer's own work on the VISTA simulator, for its
  grid of simulated driving frames.
- **Slide 56** credits "Silver+ *Science* 2016." for the AlphaGo pipeline.
- The Atari Breakout game frames on **slides 22, 26, 30, 31 and 37–40** show a game that belongs to its
  owners; only slides 26 and 30 among them carry a credit (the Mnih+ line). Slide 6's apple drawings carry
  no credit.

Not included from lecture 5, among others: the robotic-hand picture of slide 2 and slide 3's images for
robotics, game play (a Go board and the StarCraft II logo) and language modeling; the Breakout video
stills of slides 23–24; the video stills of slides 47 and 49 (credited "Amini+ *IEEE RA-L* 2020."); slide
51's Go photograph (credited "Silver+ *Science* 2016; Silver+ *Nature* 2017."); slide 52's Go board and
table (credited "Source: Wikipedia.", the table transcribed in `raw/slides/`); and slide 58's T-shirt
photograph.

Each image in `raw/images/06-language-models-new-frontiers/`, named `slide-N.jpg`, is page N of the
lecture 6 deck,
[`6S191_MIT_DeepLearning_L6.pdf`](https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L6.pdf),
extracted unmodified in the same way. 24 of the deck's 81 pages are included: slides 14, 18, 22, 26,
28–31, 34, 42, 49–51, 53, 54, 61, 64–66, 69, 71, 72, 75 and 76. Attribution for every one is the course
line above. Third-party material on them, as credited on the slides:

- **Slides 18 and 22** credit "Zhang+ *ICLR* 2017.": the randomized-label experiment and its accuracy
  chart. Slide 18's four photographs (two dogs, bananas, a tree) carry no other credit.
- **Slide 29** credits "U. Muller, 6.S191 2018." for the crossed-out cartoon; the alchemist painting beside
  it carries no credit.
- **Slides 30 and 31** credit "P. Isola 6.869." for the colorization example and the dog photographs.
- **Slide 34** credits "Despois "Adversarial examples" 2017." for the temple images and the perturbation.
- **Slide 42** credits "Athalye+ *ICML* 2018." for the 24 photographs of the 3D-printed turtle.
- **Slides 51 and 54** credit "Sohl-Dickstein+ *ICML* 2015; Ho+ *NeurIPS* 2020." and "Ho+ *NeurIPS*
  2020." for the diffusion process. The photograph of a domed building that slides 49, 51, 53 and 54 noise
  step by step, the dog of slide 61 and the generated "Two cats doing research" of slide 49 carry no credit.
- **Slide 64** credits "Ramesh+ *arXiv* 2022" and **slide 65** "OpenAI. Ramesh+ *arXiv* 2022" for their
  generated images.
- **Slide 66** cites "Hoogeboom+ *ICML* 2022, Jing+ *NeurIPS* 2022, and more…" for its molecules and
  "Anand+ *arXiv* 2022, Watson+ *Nature* 2023, Ingraham+ *Nature* 2023, Wu+ *Nature Comm.* 2024, Alamdari+
  *bioRxiv* 2024, and more …" for its protein structures.
- **Slide 75** credits "Wei+ TMLR 2022." for its three charts of emergent abilities, and **slide 76**
  "Google AI blog." for its tree illustration.

Not included from lecture 6, among others: the prize photographs of slides 4–5, the guest lecturers'
portraits and company logos of slide 7, the staff photographs of slide 8, slide 10's collage of news
articles, slide 11's brain image, slide 32's ABC News coverage of an autopilot crash (credited "ABC
News.", with photographs marked "COURTESY OF TESLA" and "GOOGLE STREET VIEW"), slide 33's photographs,
slide 43's news headlines, slide 68's ChatGPT screenshot and OpenAI logo, the film still of slides 78 and
80, and the T-shirt photographs of slides 2, 79 and 81.

Each image in `raw/images/07-three-laws-of-ai/`, named `slide-N.jpg`, is page N of the lecture 7 deck,
[`6S191_MIT_DeepLearning_L7.pdf`](https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L7.pdf),
the guest lecture by Douglas Blank. That deck has vector pages rather than page images, so each image is
the whole page rendered at 1400×788 by `extract_slide_images.py`, not modified otherwise. 4 of the deck's
44 pages are included: slides 16, 20, 21 and 25. Attribution for every one is the course line above,
with "Douglas Blank, The Three Laws of AI". Third-party material on them:

- **Slide 16**'s timeline infographic carries no credit.
- **Slide 20**'s star-history chart is credited on the slide to "star-history.com". Its contributors strip
  shows the GitHub avatars of contributors to Comet's open-source Opik project, no names legible, and the
  GitHub logo.
- **Slides 21 and 25** are screenshots of Comet's Opik web interface; the Opik name and logo are Comet
  ML's.

Not included from lecture 7, among others: slide 3's photograph of the Atlas robot (captioned "Atlas,
Boston Dynamics"); slide 4's 1982 Radio Shack advertisement featuring Isaac Asimov (captioned "Tandy Color
Computer advertisement from Personal Computing August 1982, featuring Isaac Asimov"); the table picture
of slides 11–12; slide 19's Opik logo; slide 35's terminal screenshot; slide 40's screenshot of three
YouTube comments by individuals; and slide 44's QR code. Their text is transcribed in `raw/slides/`, as is
the news article quoted on slides 28–29 (SFGate, whose URL the slides print) and the Gemini answer quoted
on slide 33.

Each image in `raw/images/08-ai-for-science/`, named `slide-N.jpg` or `slide-N.png`, is page N of the
lecture 8 deck,
[`6S191_MIT_DeepLearning_L8.pdf`](https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L8.pdf),
the guest lecture by Chris Bishop. That deck has vector pages with pasted pictures, so each image is the
whole page rendered at 1400×788 by `extract_slide_images.py`, not modified otherwise. 18 of the deck's 31
pages are included: slides 5–7, 9, 13, 15 and 17–28. Attribution for every one is the course line above,
with "Chris Bishop, AI for Science". Third-party material on them, as the slides credit it (most carry no
credit):

- **Slides 7, 15, 17, 19, 22, 24, 26 and 27**'s molecule, crystal and protein renderings and
  illustrations carry no credit. Slide 18's cartoon ship and slide 24's ladder cartoon carry none either.
- **Slide 13**'s globe rendering, titled "Aurora", carries no credit.
- **Slide 15** shows the first page of the Nature article "A generative model for inorganic materials
  design" (Zeni et al.; https://doi.org/10.1038/s41586-025-08628-5, marked "Open access" on the page).
- **Slide 20**'s photograph of Walter Kohn is captioned "Photo from the Nobel Foundation archive."; the
  Nobel medal image, the citations-per-year bar chart and the supercomputer-workload pie chart carry no
  credit.
- **Slide 21**'s photograph of a ball-and-stick model and its shadow carries no credit.
- **Slide 22** shows a word cloud of density-functional names (no credit) and a screenshot of the Science
  web page of Ann E. Mattsson, "In Pursuit of the "Divine" Functional", Science 298 (2002), pp. 759–760,
  DOI 10.1126/science.1077710.
- **Slides 23 and 25**'s charts carry no credit; slide 24 cites arXiv:2506.14665 for the Skala functional.
- **Slide 28**'s timeline is credited on the slide "Figure from “Cell Biology by the numbers”".

Not included from lecture 8, among others: slide 4's portrait beside the Dirac quotation; slide 8's
screenshot of Rich Sutton's essay "The Bitter Lesson"; slide 11's picture of a storm; slide 12's
screenshot of the Nature article "A foundation model for the Earth system"; slide 14's photographs of
application areas; slide 16, a still from a video; slide 29's protein rendering and screenshot of the
Nature article "Ab initio characterization of protein molecular dynamics with AI²BMD"; slide 30's cover of
Science (14 August 2025); and slide 31's cover of *Deep Learning: Foundations and Concepts* (Springer) and
its screenshot of an online reader. Their text is transcribed in `raw/slides/`.

Each image in `raw/images/09-massively-parallel-training/`, named `slide-N.jpg`, is page N of the lecture 9
deck,
[`6S191_MIT_DeepLearning_L9.pdf`](https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L9.pdf),
the guest lecture by Mathias Lechner. That deck's pages are single 3524×1984 images, so each image is the
whole page rendered at 1400×789 by `extract_slide_images.py`, not modified otherwise. 12 of the deck's 22
pages are included: slides 5, 7–9, 11 and 13–19. Attribution for every one is the course line above, with
"Mathias Lechner, Massively Parallel Training". Third-party material on them, as the slides credit it:

- **Slide 5**'s chart plots the training perplexity of Meta's Llama 2 models (7B, 13B, 34B, 70B); the
  slide names "Llama 2" and cites "Kaplan et al. (2020)" for the power law, and gives no other credit for
  the chart.
- The other included slides are diagrams drawn for the deck, with no third-party credit.

Not included from lecture 9, among others: slide 2's Liquid AI logo, and slide 4, a build step of slide 5
showing the same Llama 2 chart with three curves faded. Their text is transcribed in `raw/slides/`.
