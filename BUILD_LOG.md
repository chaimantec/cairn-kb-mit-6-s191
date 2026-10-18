# Build log — MIT 6.S191 knowledge base

The per-lecture record of how this knowledge base was built and checked: each
deck's licence notices and lecture pointers, each transcript's edit and checks,
what each figure audit found, each deck's printed slips, and which slides were
rendered as images and why the others were not. It is a build record, **not
needed to answer questions**: every fact a learner needs is on the wiki page,
slide file or transcript it concerns. The rules every build follows are in
[`AGENTS.md`](AGENTS.md).

## Index

| Lecture | Run |
| --- | --- |
| 1 Introduction to Deep Learning (2026) | [Lecture 1](#lecture-1--introduction-to-deep-learning-2026--built-2026-10-11), 2026-10-11 |
| 2 Recurrent Neural Networks, Transformers, and Attention (2026) | [Lecture 2](#lecture-2--recurrent-neural-networks-transformers-and-attention-2026--built-2026-10-17), 2026-10-17 |
| 3 Convolutional Neural Networks (2026) | [Lecture 3](#lecture-3--convolutional-neural-networks-2026--built-2026-10-18), 2026-10-18 |
| 4 Deep Generative Modeling (2026) | [Lecture 4](#lecture-4--deep-generative-modeling-2026--built-2026-10-18), 2026-10-18 |
| 5 Reinforcement Learning (2026) | [Lecture 5](#lecture-5--reinforcement-learning-2026--built-2026-10-18), 2026-10-18 |
| 6 Language Models and New Frontiers (2026) | [Lecture 6](#lecture-6--language-models-and-new-frontiers-2026--built-2026-10-18), 2026-10-18 |
| 7 The Three Laws of AI (2026) | [Lecture 7](#lecture-7--the-three-laws-of-ai-2026--built-2026-10-18), 2026-10-18 |
| 8 AI for Science (2026) | [Lecture 8](#lecture-8--ai-for-science-2026--built-2026-10-18), 2026-10-18 |

## Lecture 1 — Introduction to Deep Learning (2026) — built 2026-10-11

**Pointers.** Catalog position 1, video `II4giR4vOOo` (56:16), delivered 5 January 2026 by Alexander
Amini. Deck <https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L1.pdf>, 108 pages, linked
from the 2026 schedule on the course index. The title slide reads "January 5, 2026" and every footer
"1/5/26", which confirms the deck belongs to this recording. The PDF metadata gives producer PyFPDF
1.7.2 and creation date 2026-01-10; the server's Last-Modified is 2026-08-17.

**Deck format and numbering.** Every page is a single 1280×720 JPEG covering the whole page, with no
text layer and no duplicate pages. `slide_number_map.py` found no numbers, as expected with no text.
A stacked strip of the bottom 10% of eight pages (2, 15, 30, 45, 60, 75, 90, 107) showed the footer:
MIT logo, "MIT Introduction to Deep Learning", introtodeeplearning.com, @MITDeepLearning, and "1/5/26"
at bottom right, which is a date, not a slide number. Slides 4–6 are full-bleed images with no footer.
Decision: slide N = PDF page N, checked with a plain 1..108 heading sequence.

**Licence.** The site's FAQ says all materials are under the MIT licence and asks for the attribution
"© Alexander Amini and Ava Amini / MIT 6.S191: Introduction to Deep Learning /
IntroToDeepLearning.com". The deck carries no per-slide licence notices. Third-party credits printed
on the slides: slide 2 ("Goodfellow et al.", 2015; "Karras, Laine, Aila.", 2018; "MIT Intro to Deep
Learning", 2020), slide 6 (an X post by Paul Couvert, @itsPaulAi, Dec 25, 2025), slide 72 ("Visualizing
the loss landscape of neural nets". Dec 2017), and slide 81's reference column (Kiefer & Wolfowitz
1952, Kingma et al. 2014, Zeiler et al. 2012, Duchi et al. 2011, and a ruder.io link).

**Slide transcription.** The 108 page JPEGs were extracted and read by three Sonnet agents in parallel
(1–36, 37–72, 73–108), each reading one page of overlap for build-step context and appending as it
went; the parent merged the parts and wrote the header and section table. 87 slides are tagged
`*Figure: yes*`. The parent replaced 14 `\\` matrix-row separators with `\cr` and fixed GitHub math
delimiters (quoted formulas, math inside italics, `}_` pairings) until `check_math.mjs` reported 0
errors and 0 warnings.

**Figure audit.** A separate Sonnet agent checked slides 2, 6, 19, 25, 31, 52, 53, 57, 75, 81, 82, 93, 97
and 98 against the page JPEGs, with enlarged crops, covering every table cell, worked number, axis,
series and code line. It found **0 discrepancies**. The parent then looked at the images of slides 106
(early-stopping chart) and 39 (single-hidden-layer diagram), which matched their descriptions, and at
a crop of slide 86 to confirm the printed slip below.

**Printed slips and as-printed oddities**, all reproduced as printed, with notes in the slide file:

- Slide 82: `tf.keras.optimizer.SGD()`, where slide 81 prints `tf.keras.optimizers.SGD`, and a final
  line `optimizer.apply_gradients(zip(grads, model.trainable_variables)))` with one parenthesis too many.
- Slides 86–87: step 4 computes $\frac{\partial J_i(\boldsymbol{W})}{\partial \boldsymbol{W}}$ but
  step 5 updates with $\frac{\partial J(\boldsymbol{W})}{\partial \boldsymbol{W}}$. The lecturer
  describes stepping against the one point's gradient (≈47:05). This is noted on the wiki page.
- Slide 52, titled binary cross-entropy, gives the TensorFlow line
  `tf.nn.softmax_cross_entropy_with_logits(y, predicted)`; slide 25 gives `torch.nn.ReLU(z)`; slide 97
  gives `Dropout(p=0.5)` for both frameworks. These are reproduced as printed, without comment.
- Slide 81 lists no reference for RMSProp.

**Spoken vs printed.** At 7:47 the lecturer says the Liquid AI model has "only 2 billion parameters",
while the post on slide 6 says 2.6B. The transcript keeps the spoken number with an `[Ed: …]` note, and
the wiki gives both. He does not name the model aloud; the slide's table names it LFM2-2.6B-Exp.

**Transcript.** YouTube auto-captions, already punctuated. Copy-edited by a Sonnet agent against the
slide file: filler and false starts removed, `>>` marks dropped, optimizer spellings set to slide 81's,
"Alva" restored to Ava (slide 15), student remarks marked at 4:43, 32:30 (inaudible, partly "the
four…") and 51:42, and the phone audio model's reply marked at 5:28. "John" at 10:09, the host offering
TEDxMIT talks, is kept without a surname: none is spoken or on the slides. The course site mentions a
John Werner only as host of a course social, so the surname was not restored. "ChatGPT-3" at 1:38 is
left as said, since it matches slide 3. Checks re-run by the parent: 73 of 73 `[MM:SS]` marks
identical, number inventory identical, per-paragraph word ratio 0.87–1.02.

**Coverage gap the deck cannot fill.** The live phone demo (≈3:58–7:01: the Z7 question and the audio
model) has no slide; the wiki carries it in prose only.

**Images.** 34 of 108 pages, copied byte for byte from the deck's own JPEGs (1.7 MB): 2, 7, 18, 19,
22, 23, 24, 25, 28, 31, 32, 35, 38, 39, 40, 41, 43, 47, 50, 51, 52, 53, 57, 59, 60, 61, 67, 70, 72, 75, 93,
97, 98, 106. All 34 are embedded in `wiki/01-introduction.md`, in the passage citing each, and under
their headings in the slide file; the eight topic pages reuse one to three each. Not rendered, and why:

- Logistics, logos, portraits and prize photos: 8–16.
- Title and lab-announcement slides, which are decorative: 1, 108.
- Stock or logo imagery that adds nothing to the text: 3, 4, 5.
- Slide 6: its content is a tweet and a benchmark table, both transcribed exactly. The image also
  reproduces a third party's social-media post.
- Section dividers and text-only slides: 17, 20, 33, 44, 45, 54, 55, 56, 62, 71, 73, 74, 78, 79, 80, 83,
  90, 91, 92, 94, 95.
- Code or tables transcribed exactly: 37 (dense layer from scratch), 63–64 (gradient-descent code),
  81 (optimizer table), 82 (training loop).
- Build steps wholly contained in an included slide: 21 (→22), 26–27 (→28), 29–30 (→31), 34 (repeats
  22), 36 (→38), 42 (→43), 46 (→47), 48–49 (→50), 58 (→59), 65–66 (→67), 68–69 (→70), 76–77 (same plot
  as 75, subtitle only), 96 (→97), 99–105 (→106).
- Repeats of an included figure: 84–89 (the slide 61 loss surface beside transcribed algorithm text),
  107 (a review of three earlier figures).

**Cost.** Measured with `measure_run_cost.py`: \$8.64 for the whole lecture. The Opus parent cost \$6.77 and the five Sonnet agents \$1.86 (22%): three slide readers at \$0.44–0.52 each, the copy-edit \$0.26 and the audit \$0.15. Another ~\$0.21 of output is logged incompletely and not counted. Reading native 1280×720 page JPEGs instead of PDF page renders is why the deck cost about \$1.45 to transcribe.

### Run checklist (moved verbatim from TODO.md)

#### Transcripts
- [x] 01 Introduction to Deep Learning — video II4giR4vOOo (auto-captions, already punctuated; light Sonnet copy-edit, verbatim in original/)

#### Crawl
- [x] Fetch course site index: https://introtodeeplearning.com/ (2026 index only; year archives deferred)
- [x] Download linked PDFs and slides (gitignored; 9 decks + the AAAI lab paper)
- [x] Write sources.md

#### Slides (raw/slides/)
- [x] 01 Introduction — 6S191_MIT_DeepLearning_L1.pdf (108 pages, no text layer, no printed numbers: slide N = page N; three Sonnet agents in parallel; Sonnet audit of 14 pages, 0 discrepancies)

#### Wiki
- [x] wiki/01-introduction.md
- [x] Topic pages (cross-lecture concepts) — what-is-deep-learning, perceptron, activation-functions, neural-network-layers, loss-functions, gradient-descent, backpropagation, regularization (lecture 1 only; extend as lectures land)
- [x] INDEX.md table of contents

#### Images
- [x] raw/images/01-introduction/ — 34 native page JPEGs extracted byte-for-byte; embedded in the wiki and slide files
- [x] INDEX.md — the chat's image rules; AGENTS.md — the Images conventions and table row; BUILD_LOG.md — what was rendered and why; LICENSE.md — attribution

#### Publish
- [x] kb.json — coverage, materials.method, provenance caveats
- [x] BUILD_LOG.md — lecture 1 record: notices, audit findings, printed slips, transcript edits
- [x] SEE_ALSO.md — MIT 6.7960 and MIT 15.773
- [x] verify_kb.py clean, and its review section read
- [x] Commit and push
- [x] PATCH kbUrl onto the catalog entry (https://github.com/chaimantec/cairn-kb-mit-6-s191)

## Lecture 2 — Recurrent Neural Networks, Transformers, and Attention (2026) — built 2026-10-17

**Pointers.** Catalog position 2, video `d02VkQ9MP44` (57:34), delivered 5 January 2026 by Ava Amini.
Deck <https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L2.pdf>, 83 pages, linked from the
2026 schedule on the course index (downloaded in the lecture 1 crawl). The title slide reads "Deep
Sequence Modeling", "Ava Amini", "January 5, 2026". The PDF metadata gives author "A. Amini, A.P. Amini.
MIT 6.S191", producer PyFPDF 1.7.2 and creation date 2026-01-04.

**Deck format and numbering.** As lecture 1: every page is a single 1280×720 JPEG with no text layer.
A stacked strip of the bottom 10% of pages 2, 10, 20, 30, 45, 60, 75 and 82 showed the standard footer
with "1/5/26" at bottom right and no slide number; slide 75's strip also showed "Vaswani+, NeurIPS
2017." beside the date. Slides 2–5 (the blue ball slides) have no footer. Decision: slide N = PDF page
N, checked with a plain 1..83 heading sequence.

**Licence.** No per-slide licence notices. Third-party credits printed on the slides: "H. Suresh, 6.S191
2018." (32–34, 38, 39, 58), "Mozer *Complex Systems* 1989." (44), "Huawei." (56), "Socher+, EMNLP 2013."
(57), "Vaswani+, NeurIPS 2017." (72, 75–78), and slide 80's citations (Devlin et al. NAACL 2019, Brown
et al. NeurIPS 2020, Jumper et al. Nature 2021, Lin et al. Science 2023, Dosovitskiy et al. ICLR 2020).
Uncredited third-party imagery: tweets (8, 58), Iron Man stills (66, 79), a YouTube results page with
third-party thumbnails (68–69), stock photographs (7, 67). LICENSE.md lists what is in the images.

**Slide transcription.** The 83 page JPEGs were extracted with `get_image_info(xrefs=True)` and read by
three Sonnet agents in parallel (1–28, 29–56, 57–83), the second and third reading one page of overlap
for build-step context and every agent appending as it went; the parent merged the parts and wrote the
header and section table. 67 slides are tagged `*Figure: yes*`. Parent edits: slide 7's "Build step"
line rewritten (it replaces slide 6's waveform rather than adding to it); `}_` subscripts spaced, math
moved out of the italic Figure lines, the fill-in blanks `___` on slides 51–53 escaped (they paired with
math underscores into italics on GitHub), `$x_0$/$x_1$` and `"$i$-th index"` reworded, until
`check_math.mjs` reported 0 errors and 0 warnings.

**Figure audit.** A separate Sonnet agent checked slides 7, 8, 24, 26, 27, 28, 36, 44, 53, 54, 56, 63,
72, 75, 76, 77, 79 and 80 against the page JPEGs with enlarged crops, including the build-step claims
(reading pages 6, 23, 25, 43, 52, 62) and a cell-by-cell 7×7 table of slide 75's attention heat map,
which matched the transcription exactly. It found **2 discrepancies**, both fixed: slide 28's note said
the second line of each snippet is indented, but in the PyTorch snippet it is the first (the code block
itself was right); slide 63's description put "…" in the output and input bars, which on the page are
empty gaps (only the yellow grid prints "···"). The parent then looked at the images of slides 77 (the
attention-head block diagram) and 79 (three attention heads on the Iron Man still); both matched.

**Printed slips and as-printed oddities**, all reproduced as printed:

- Slides 26, 43 and 44 label the last column's loss $L_3$ while its input and output are $x_t$ and
  $\hat{y}_ t$. The wiki notes it once.
- Slide 27 writes the RNN cell's matrix products with `*` (`self.W_hh * self.h + self.W_xh * x`).
- Slide 28 prints `from tf.keras.layers import SimpleRNN`, which is not a valid import path as written,
  with inconsistent indentation in both snippets.
- Slide 57 gives `tf.nn.softmax_cross_entropy_with_logits(y, predicted)` as the sentiment loss, the same
  line lecture 1's slide 52 gives for binary cross-entropy.
- Slide 69: "Return the values highest attention" (no "with").
- Slides 73–74: the scaled dot product is "Also known as the 'cosine similarity'", and the lecturer says
  the same (≈50:16); the denominator is printed only as "scaling". The wiki attributes both and adds no
  correction.
- Slide 77 prints the equation without slide 76's "= A(Q,K,V)".
- Slide 54's lead sentence ends "within each recurrent unit with", followed by the gate diagram.

**Spoken vs printed.** Aloud, Amini counts representing words as numbers as "design criteria number
one" (≈27:46); the slide list (30, 40) has four criteria without it, ending with "share parameters". She
says the state is initialized to "0000 0" (≈15:23), slide 18 prints `[0, 0, 0, 0]`. She describes slide
68's "MIT 6.S191 (2020)" result as a video "from six years ago". The wiki gives both where they differ.

**Transcript.** YouTube auto-captions, already punctuated. Copy-edited by a Sonnet agent against the
slide file: filler, stutters and `>>` marks removed; "6S191", "fet forward", "paralyzable", "attention
waiting", "soft max", "dotproduct" and run-together compounds restored; student turns marked at 23:56
(two, the second partly garbled, with an [Ed] note) and 33:57 ("Is H0 considered a parameter?").
Spoken-only proper nouns, not printed in the deck and restored from obvious stutters: "Jurgen Schmidhub
Schmidh Huber" → Jürgen Schmidhuber (36:15) and "France Schubert" → Franz Schubert, "unfinished
symphony" → Unfinished Symphony (37:02). "John" at 56:26 is kept without a surname, with an [Ed] note
that slide 83 thanks John Werner and Link Ventures; "as you meant earlier" is marked unclear. Checks
re-run by the parent: 75 of 75 `[MM:SS]` marks identical, number inventory identical, per-paragraph
word ratio 0.92–1.02.

**Coverage gaps the deck cannot fill, and slides not narrated.** The Schubert sample (≈37:02–37:50) is
audio only. Slides 50–53 (the clouds/France examples) and 57–58 (sentiment classification) are shown but
not discussed aloud; the wiki says so.

**Images.** 33 of 83 pages, copied byte for byte from the deck's own JPEGs (1.9 MB): 3, 5, 8, 10, 11, 13,
15, 17, 24, 26, 29, 36, 42, 44, 48, 53, 54, 56, 57, 61, 64, 66, 68, 69, 71, 72, 73, 74, 75, 76, 77, 79, 80.
All 33 are embedded in `wiki/02-rnns-transformers-attention.md`, in the passage citing each, and under
their headings in the slide file (by `embed_slide_images.py`); the new and extended topic pages reuse
one to three each. Not rendered, and why:

- Title, summary, lab and reception slides: 1, 81, 82, 83.
- Stock or decorative imagery that adds nothing to the text: 6 (an audio waveform), 7 (a stock-photo
  collage), 38 (clip-art hearts), 39 (burger icons), 67 (a wall of thumbnails).
- Section dividers and text-only slides: 9, 16, 31, 32, 33, 34, 37, 41, 49, 50, 55, 65.
- Code transcribed exactly, beside slide 17's recurrent-cell diagram: 18, 19, 20, 27, 28.
- The design-criteria list beside the same cell diagram: 30, 40.
- Build steps wholly contained in an included slide: 2 (→3), 4 (→5), 12 (→13), 14 (→15), 21–23 (→24),
  25 (→26), 35 (→36), 43 (→44), 45–47 (→48), 51–52 (→53), 59–60 (→61), 62 (61's diagram with a
  text list), 63 (→64), 70 (→71), 78 (77's diagram with a closing line).
- Slide 58: two tweets by individuals, transcribed in full, beside slide 57's diagram.

**Cost.** Measured with `measure_run_cost.py` after the push: \$7.11 for the whole lecture. The Opus parent cost \$5.22 (49 calls, ending at 176k context) and the five Sonnet agents \$1.89 (27%): three slide readers at \$0.41–0.46 each, the audit \$0.31 and the copy-edit \$0.26. Another ~\$0.12 of output is logged incompletely and not counted.

#### Run checklist (moved verbatim from TODO.md)

_Run 2 — lecture 2 (Recurrent Neural Networks, Transformers, and Attention, 2026)_

Catalog position 2, video d02VkQ9MP44 (57:34). Deck `slides/6S191_MIT_DeepLearning_L2.pdf`: 83 pages,
each one 1280×720 JPEG, no text layer, footer "1/5/26" with no slide number (checked on a strip of 8
footers): slide N = page N.

- [x] Verbatim captions → raw/transcripts/original/02-rnns-transformers-attention.md (75 marks)
- [x] raw/slides/02-rnns-transformers-attention.md — three Sonnet readers (1–28, 29–56, 57–83), merged, header (67 figure slides)
- [x] Figure audit (Sonnet) of chart-, table-, code- and equation-heavy pages; parent checks two images (18 pages, 2 small discrepancies fixed; parent checked 77 and 79)
- [x] raw/transcripts/02-rnns-transformers-attention.md — Sonnet copy-edit; marks, numbers, ratios checked (75/75, identical, 0.92–1.02)
- [x] raw/images/02-rnns-transformers-attention/ — native page JPEGs of figure slides, embedded (33 of 83, 1.9 MB)
- [x] wiki/02-rnns-transformers-attention.md
- [x] Topic pages: new (sequence modeling, RNNs, attention/transformers…) and extended (backpropagation, …)
- [x] INDEX.md, AGENTS.md image table, LICENSE.md, sources.md, kb.json, BUILD_LOG.md
- [x] verify_kb.py clean, and its review section read
- [x] Commit and push
- [x] Move this section to BUILD_LOG.md

## Lecture 3 — Convolutional Neural Networks (2026) — built 2026-10-18

**Pointers.** Catalog position 3, video `pqIcoskUuWs` (56:46), delivered 6 January 2026 by Alexander
Amini. Deck <https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L3.pdf>, 70 pages, linked from
the 2026 schedule on the course index (downloaded in the lecture 1 crawl; same size as on the server,
whose Last-Modified is 2026-08-17). The schedule lists it as Lecture 3, "Deep Computer Vision", showing
"Apr. 13, 2026" with "Jan. 6, 2026" commented out; the title slide reads "Deep Computer Vision",
"Alexander Amini", "January 6, 2026". The PDF metadata gives author "A. Amini, A.P. Amini. MIT 6.S191",
producer PyFPDF 1.7.2 and creation date 2026-01-04.

**Deck format and numbering.** As lectures 1–2: every page is a single 1280×720 JPEG with no text layer,
and no two pages are identical. A stacked strip of the bottom 10% of pages 2, 10, 20, 30, 40, 50, 60 and
69 showed the standard footer with "1/6/26" at bottom right and no slide number, with citations beside
the date on 10 (Levin), 30 (Rohrer), 40 (Karn) and 50 (Lee+ *ICML* 2009). Slide 2 has no footer and 69 is
black. Decision: slide N = PDF page N, checked with a plain 1..70 heading sequence.

**Licence.** No per-slide licence notices. Third-party credits printed on the slides: "Boston Dynamics; P.
Isola 6.869" (4), "Amini+ *ICRA* 2019." (6, 64–66), "Esteva+ *Nature* 2017, McKinney+ *Nature* 2020, Wang+
*Sci. Rep.* 2020." (7), "Google Project Guideline" (8), "Levin *Image Processing & Computer Vision*."
(10–12), "Li/Johnson/Yeung C231n." (16–17), "Lee+ *ICML* 2009." (18, 50), "Rohrer *How do CNNs work?*"
(27–30), "Karn *Intuitive CNNs*" (31–40, 48), "McKinney+ *Nature* 2020." (57), "Girshick+ *CVPR* 2014."
(61), "Ren+ *IEEE* 2016." (62), "Long+ *CVPR* 2015." (63). Uncredited third-party imagery: the street
photograph (3), the portrait photographs (14, 41), the taxi photographs (58–60), the collage (67).
LICENSE.md lists what is in the images.

**Slide transcription.** The 70 page JPEGs were extracted with `get_image_info(xrefs=True)` and read by
two Sonnet agents in parallel (1–35, 36–70, the second reading page 35 for build-step context), each
appending as it went; the parent merged the parts and wrote the header, section table and an Images
note. 64 slides are tagged `*Figure: yes*`. Parent edits: two identifications the slides do not print
were removed ("the 'Lenna' test image" on slide 14, "an Eames lounge chair" on slide 16); slide 10's
pixel-count estimate was replaced by a pointer to slide 12's 16×12 matrix; `\,` became `\thinspace`, an
inline `bmatrix` (whose `&` GitHub double-escapes) and a quoted `"$1$` became plain text, and the three
dollar signs on slide 70 were spelled out, until `check_math.mjs` reported 0 errors and 0 warnings.

**Figure audit.** A separate Sonnet agent checked slides 12, 13, 16, 27, 29, 30, 36, 40, 41, 46, 47, 49,
53, 54, 57, 61, 63, 65 and 68 against the page JPEGs with enlarged crops. Exact: all 192 cells of slide
12's matrix, both 9×9 grids of slide 27, the three kernels of slide 41, slide 46's formula, slide 49,
slide 63's five resolution labels and slide 65's equations; slide 47 does print "path connected". It
found discrepancies on **6 pages**, all fixed: slide 12's caveat about uncertain 5/6 digits was unfounded;
slide 29's X image is 9×9, not 8×8; the green box on slide 53 encloses three lines, not two, and the
mini-diagram boxes on 53–54 exclude the input; slide 53 opens each `'relu’` with a straight quote and
closes it with a curly one; slide 57 has five reader diamonds per panel, not four, and only panel b
labels its y-axis; slide 61 has no dots below its last box. The parent recomputed all nine entries of
the worked feature map (slides 31–40) from the transcribed image and filter, looked at a crop of slide 53
(the quotes), and at the images of slides 57 (chart) and 65 (diagram), which matched. A crop of slide
65's loss showed it printed "L = −log(P(θ|I, M)", with one closing parenthesis: the reader had balanced
it and the auditor reported it exact. The general lesson went into AGENTS.md.

**Printed slips and as-printed oddities**, all reproduced as printed:

- Slide 47: "Locations in input image that a node is path connected to" (presumably "patch").
- Slides 53–54 pass `filter_size=` where slide 47's code uses `kernel_size`; slide 54 imports only
  `torch` but calls `nn.Sequential`, and its comment "first and second convolutional layer" sits above
  the first block only; slide 53 mixes straight and typographic quotes (`'relu’`, `‘softmax’`).
- Slide 65's loss closes only one of its two parentheses.
- Slide 62 is the first build of the Faster R-CNN diagram; the deck does not continue it.
- Slide 68's summary lists ImageNet and image captioning, neither of which the lecture discusses.

**Spoken vs printed.** Amini gives pixel brightness as "ranging from zero to one" (≈4:43); slide 12
prints [0,255]. The captions have the 4×4 filter "defined by 14 numbers" twice (≈17:04); slide 25 prints
16 weights and he says "these 16 numbers" at 17:50. Aloud, region proposals come from heuristics such as
thresholding (≈50:15); slide 62 describes a learned region proposal network. He names neither R-CNN nor
Faster R-CNN; the slides do. Lecture 2 (≈54:54) says vision transformers will be covered in lecture 3;
neither this deck nor this talk mentions them, which INDEX.md, kb.json, the lecture 2 page and the
attention page now say. The wiki gives both sides wherever they differ.

**Transcript.** YouTube auto-captions, already punctuated. Copy-edited by a Sonnet agent against the
slide file: filler, stutters and `>>` marks removed; "non- linearity" to non-linearity, "down sampling" /
"up sampling" to downsampling / upsampling, "sub classification" to subclassification, "pull" to pool
(37:49). 55:36: "Albus' lecture" restored to Ava's, with an [Ed] note citing lecture 4's title slide
("Deep Generative Modeling", "Ava Amini", "January 6, 2026"), which the parent opened to confirm. "14
numbers" kept with an [Ed] note; "Steps are the building blocks" (7:46) kept with an [Ed] note, to which
the parent added slide 14's "Door, Windows, Steps"; "MIT Toyota collaboration" kept as captioned. Student
turns marked at 24:44 (one question not in the captions, with an [Ed] note, and the overlap question),
25:30, 35:29, 37:02, 38:35/39:23 (partly garbled, [Ed] note) and 42:29/43:15. Checks re-run by the
parent: 74 of 74 `[MM:SS]` marks identical, number inventory identical, per-paragraph word ratio
0.86–1.08.

**Coverage gaps the deck cannot fill, and slides not narrated.** The question-and-answer passages
(24:44–26:16, 35:29–37:02, 38:35–40:56, 42:29–43:15) have no slides. Slides 8 (accessibility), 66 (video)
and 67 (collage) are shown without being described, and slide 65's equations and slide 63's code are not
read aloud; the wiki says so where it uses them.

**Images.** 33 of 70 pages, copied byte for byte from the deck's own JPEGs (2.4 MB): 3, 6, 12, 13, 16, 20,
22, 24, 25, 27, 28, 29, 30, 32, 40, 41, 44, 47, 48, 49, 50, 51, 52, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65.
All 33 are embedded in `wiki/03-convolutional-neural-networks.md` by hand, in the passage citing each,
and under their headings in the slide file (by `embed_slide_images.py`); the two new topic pages reuse
six each. Not rendered, and why:

- Title, summary, lab and announcement slides: 1, 68, 69, 70.
- Photographs and collages that add nothing to the text: 2 (an eye, behind the quote), 4, 5, 7, 8, 14
  (three photographs whose feature lists are transcribed), 67.
- Section dividers: 9, 19, 26, 43, 55.
- Build steps wholly contained in an included slide: 10–11 (→12), 15 (→16), 17 (16 with one chevron
  highlighted), 21 (→22), 23 (→24), 31 (→32), 33–39 (the filter positions between 32 and 40; every
  number is transcribed), 45–46 (25's diagram, with text and a formula transcribed exactly).
- Repeats of an included figure: 18 (the feature grids of 50, which adds the layer labels), 42 (25's
  diagram and list).
- Code transcribed exactly, beside a small copy of slide 51's diagram: 53, 54.
- A video still of slide 6's car: 66.

**Left open.** With `gh` authenticated, `verify_kb.py`'s GitHub check now flags 9 `$$` blocks nested in
list items in lecture 1's files (`raw/slides/01-introduction.md` lines 380–400 and 587,
`wiki/01-introduction.md` lines 327, 333 and 467): GitHub renders them as inline math. They predate this
run; TODO.md carries the fix.

**Cost.** Measured with `measure_run_cost.py` after the lecture push: \$10.93 for the whole lecture. The Opus parent cost \$8.52 (84 calls, ending at 217k context) and the four Sonnet agents \$2.41 (22%): two slide readers at \$0.61 and \$0.64, the audit \$0.81 and the copy-edit \$0.35. Another ~\$0.25 of output is logged incompletely and not counted. The closing bookkeeping commit is not included.

#### Run checklist (moved verbatim from TODO.md)

_Run 3 — lecture 3 (Convolutional Neural Networks, 2026)_

Catalog position 3, video pqIcoskUuWs (56:46). Deck `slides/6S191_MIT_DeepLearning_L3.pdf`: 70 pages,
each one 1280×720 JPEG, no text layer, footer "1/6/26" with no slide number (checked on a strip of 8
footers; some footers carry citations at bottom right): slide N = page N.

- [x] Verbatim captions → raw/transcripts/original/03-convolutional-neural-networks.md (74 marks)
- [x] raw/slides/03-convolutional-neural-networks.md — two Sonnet readers (1–35, 35–70), merged, header (64 figure slides)
- [x] Figure audit (Sonnet) of chart-, table-, code- and equation-heavy pages; parent checks two images (19 pages; fixes on 29, 53–54, 57, 61, 10–12; parent: crop of 53, images of 57 and 65, crop of 65's loss)
- [x] raw/transcripts/03-convolutional-neural-networks.md — Sonnet copy-edit; marks, numbers, ratios checked (74/74, identical, 0.86–1.08)
- [x] raw/images/03-convolutional-neural-networks/ — native page JPEGs of figure slides, embedded (33 of 70, 2.4 MB)
- [x] wiki/03-convolutional-neural-networks.md
- [x] Topic pages: new (convolutional-neural-networks, computer-vision) and extended (neural-network-layers, activation-functions, what-is-deep-learning, sequence-modeling, loss-functions, attention-and-transformers; lecture 2 page)
- [x] INDEX.md, AGENTS.md image table, LICENSE.md, sources.md, kb.json, BUILD_LOG.md
- [x] verify_kb.py clean, and its review section read
- [x] Commit and push (4fe25bf)
- [x] Move this section to BUILD_LOG.md

## Lecture 4 — Deep Generative Modeling (2026) — built 2026-10-18

**Pointers.** Catalog position 4, video `R8V8CbuxryI` (49:36), delivered 6 January 2026 by Ava Amini.
Deck <https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L4.pdf>, 84 pages, downloaded in the
lecture 1 crawl (same size as on the server, 4,566,713 bytes; Last-Modified 2026-08-17). The title slide
reads "Deep Generative Modeling", "Ava Amini", "January 6, 2026". PDF metadata: author "A. Amini, A.P.
Amini. MIT 6.S191", producer PyFPDF 1.7.2, created 2026-01-04.

**Deck format and numbering.** As lectures 1–3: every page is one 1280×720 JPEG, no text layer, no two
pages identical. A strip of the bottom 10% of pages 2, 10, 20, 30, 40, 50, 60, 70, 80 and 84 showed the
standard footer with "1/6/26" and no slide number (credits beside it on 2, 10, 30, 40 and 50); 80 and 84
have no footer. Slide N = PDF page N, checked with a plain 1..84 heading sequence.

**Licence.** No per-slide licence notices. Footer credits: "Google Gemini" (2), "Amini/Soleimany+
*AAAI/AIES* 2019." (6, 42), "Amini+ *IROS* 2018." (7), "Plato, *Republic.*" (10–11), "Kingma+ *ICLR*
2014." (21–29, 33–39), "Joseph Rocca." (30–32), "Kingma+ *ICLR* 2014; Chen+ *NeurIPS* 2018." (40),
"Higgins+ *ICLR* 2017." (41), "Goodfellow+ *NeurIPS* 2014." (50), "Brock+ *ICLR* 2019." (76), "Zhu+ *ICCV*
2017." (78). Uncredited third-party imagery: slide 5's photographs, slide 8's ChatGPT screenshot,
paintings and molecules, the digits of 13–17, the face photograph C of slide 2, slide 74–76's birds,
slide 79's waveforms, slide 80's video still and logo, and the pictures of 82–84. LICENSE.md lists what
is in the images.

**Slide transcription.** The 84 page JPEGs were extracted with `get_image_info(xrefs=True)` and read by
three Sonnet agents in parallel (1–28, 29–56, 57–84; the second and third read the preceding page for
build-step context), each appending as it went; the parent merged the parts and wrote the header,
section table and Images note. 77 slides are tagged `*Figure: yes*`. Parent edits: slide 31's build-step
line, which spoke of "this agent's pages", rewritten; a stray `\ ` removed from slide 41's formula;
slide 84's three dollar signs spelled out; "generated-looking" removed from slide 82 and a skin-tone
description from slide 83's blurred face; 54 quoted inline formulas unquoted, four `\mathbb{E}_{`
spaced, and two "Data:" lines on slides 3–4 rephrased, until `check_math.mjs` reported 0 errors and 0
warnings.

**Figure audit.** A separate Sonnet agent checked slides 5, 7, 17, 23, 28, 29, 31, 35, 36, 37, 41, 55, 56,
57, 62, 70, 72, 74, 76, 79, 80 and 84 against the page JPEGs with enlarged crops. Nothing described was
absent from its page. Exact: slide 17's first and last ground-truth rows; slide 23's upright z and x;
slide 29's KL expansion; slides 35–37; slide 41's formula, β values and 5×7 grids; slides 70 and 72's
objective; slide 84's text; the bar heights of 55–57 (within about 0.05). Discrepancies on **6 pages**,
all fixed: the transcription's "too small to read" on the scatter-plot ticks of 28–29 was false (both
axes −4 to 4; 12 colour blocks, 0 at the bottom) and slide 29 said "ten" colours while listing twelve;
slide 62's generator-panel order made explicit; slide 74's N is upright, not italic; slide 76's two
noise points sit near the right edge, and the last strip image is not on grass; slide 80's play button
and logo. The parent looked at the images of slides 70 (the GAN objective, exactly as transcribed, with
the first term labelled "Fake") and 29 (the KL expansion, exactly as transcribed, leading minus and
unsquared $\sigma_j$ included), and at a crop of slide 77, whose N is italic (unlike 74's).

**Printed slips and as-printed oddities**, all reproduced as printed:

- Slide 29: the KL expansion $-\frac{1}{2}\sum_{j=0}^{k-1}(\sigma_j + \mu_j^2 - 1 - \log\sigma_j)$ is never
  positive (each bracket is at least zero); the wiki says so from the formula alone.
- Slide 31 is a frame caught mid-transition, its not-regularized panel half faded; slide 41 prints
  "Standard VAE loss:" and "β-VAE loss:" on top of each other and an empty red box before $D_{KL}$.
- Slides 70–72 print $\log D(G(\mathbf{z})) + \log(1 - D(\mathbf{x}))$, the first term labelled "Fake";
  read as the lecturer reads it, $D$ is the probability of fake, while slides 54–68 plot P(real).
- Slide 4 changes slide 3's "Learn some hidden" to "Learn the hidden"; slide 41's loss lists
  $(\theta, \phi; \ldots)$ where slide 24 has $(\phi, \theta, x)$; slides 69–71 alternate "instances"
  and "images"; slides 35–37 spell "Reparametrizing", slide 45 "Reparameterization".
- Slide 84 is lecture 3's closing announcement slide (its slide 70), "Lecture 4: Generative Modeling
  starting soon!".

**Spoken vs printed.** "90% of the distribution" (≈7:02) against slide 7's "95% of Driving Data"; "a mean
and a variance" (≈18:40) against slide 22's "standard deviation vector"; the KL-divergence is named only
on slide 29; diffusion models in "tomorrow's lecture six" (≈31:54) against slide 82's "Lectures 6 and 7".
Slides 40–41 (disentanglement, β-VAE) are not narrated. The wiki gives both sides and lists them in a
"Spoken versus printed" section.

**Transcript.** YouTube auto-captions, already punctuated. Copy-edited by a Sonnet agent against the
slide file: filler, stutters and `>>` marks removed; "slate and space" to latent space (20:59),
"reparameterization" to the slides' reparametrization (33:26), "cycle GAN" to CycleGAN (45:49). Student
question marked at 30:20; the 46:37 synthesized-voice clip bracketed with [Ed] notes. Kept with [Ed]
notes: "discriminative encoder" (35:46, citing slide 50), "the principle of adversarial in again"
(41:58), "you can and about" (43:29). The agent's note at 7:47 called the captions' "Dolly" "probably
DALL-E"; the parent rewrote it to say only that it is unclear and the slides name no image model (the
general lesson went into AGENTS.md). Checks re-run by the parent: 64 of 64 `[MM:SS]` marks identical,
number inventory identical, per-paragraph word ratio 0.91–1.01.

**Coverage gaps.** The student question (30:20–31:54) has no slide. Slides 40–41 are shown but not
narrated; slide 80's video is played, not described; slide 29's expansion is not read aloud.

**Images.** 39 of 84 pages, copied byte for byte from the deck's own JPEGs (2.3 MB): 2, 5, 6, 7, 8, 9,
10, 15, 16, 17, 22, 26, 27, 29, 30, 31, 32, 34, 35, 36, 37, 39, 40, 41, 49, 50, 55, 57, 60, 62, 64, 68,
70, 72, 74, 76, 77, 78, 79. All 39 are embedded in `wiki/04-deep-generative-modeling.md` by hand, in the
passage citing each, and under their headings in the slide file (by `embed_slide_images.py`); the three
new topic pages reuse 13. Not rendered, and why:

- Title, text-only, summary and section-divider slides: 1, 3, 4, 12, 18, 19, 48.
- Build steps wholly contained in an included slide: 13–14 (→15), 21 (→22), 23–25 (→26–27), 28 (→27's
  labels, 29's plot), 33 (→34), 51–54 and 56 (→55, 57), 58–59 (→60), 61 (→62), 63 (→64), 65–67 (→68),
  71 (→72's diagram; its formula is transcribed), 75 (a second noise sample; its bird is in 76's strip).
- Repeats of an included figure: 11 (10 with a line of text), 20 (16's diagram), 38 (34's), 42 (6's
  grids), 43–47 (the summary list over 16's diagram), 69 and 73 (50's diagram), 81 (9's diagrams).
- A video still: 80 (the synthesized-voice demo).
- Decorative and announcement slides: 82 (the diffusion teaser's landscape), 83, 84.

**AGENTS.md lessons** (general form): frames caught mid-animation are transcribed as they are; `[Ed]`
notes never propose a name the slides do not support; a suspect printed formula is questioned on the
wiki only from the course's own material.

**Cost.** Measured with `measure_run_cost.py` after the lecture push: \$8.78 for the whole lecture. The Opus parent cost \$6.60 (65 calls, ending at 189k context) and the five Sonnet agents \$2.18 (25%): three slide readers at \$0.52, \$0.53 and \$0.47, the audit \$0.48 and the copy-edit \$0.19. Another ~\$0.11 of output is logged incompletely and not counted. The closing bookkeeping commit is not included.

#### Run checklist (moved verbatim from TODO.md)

_Run 4 — lecture 4 (Deep Generative Modeling, 2026)_

Catalog position 4, video R8V8CbuxryI (49:36). Deck `slides/6S191_MIT_DeepLearning_L4.pdf`: 84 pages,
each one 1280×720 JPEG, no text layer (PyFPDF, created 2026-01-04), footer "1/6/26" with no slide number
(checked on a strip of 10 footers; 80 and 84 are black): slide N = page N.

- [x] Verbatim captions → raw/transcripts/original/04-deep-generative-modeling.md (64 marks)
- [x] raw/slides/04-deep-generative-modeling.md — three Sonnet readers (1–28, 28–56, 56–84), merged, header (77 figure slides)
- [x] Figure audit (Sonnet) of chart-, equation-, code- and diagram-heavy pages; parent checks two images (22 pages; fixes on 28, 29, 62, 74, 76, 80; parent: images of 70 and 29, crop of 77)
- [x] raw/transcripts/04-deep-generative-modeling.md — Sonnet copy-edit; marks, numbers, ratios checked (64/64, identical, 0.91–1.01)
- [x] raw/images/04-deep-generative-modeling/ — native page JPEGs of figure slides, embedded (39 of 84, 2.3 MB)
- [x] wiki/04-deep-generative-modeling.md
- [x] Topic pages, new and extended (new: generative-modeling, autoencoders-and-vaes, generative-adversarial-networks; extended: loss-functions, backpropagation, regularization, what-is-deep-learning; lecture 3 page)
- [x] INDEX.md, AGENTS.md image table, LICENSE.md, sources.md, kb.json, BUILD_LOG.md (sources.md already listed the deck)
- [x] verify_kb.py clean, and its review section read
- [x] Commit and push (3dbc42f)
- [x] Move this section to BUILD_LOG.md

## Lecture 5 — Reinforcement Learning (2026) — built 2026-10-18

**Pointers.** Catalog position 5, video `1ij3dweHu-0` (59:19), delivered 7 January 2026 by Alexander
Amini. Deck <https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L5.pdf>, 58 pages, downloaded in
the lecture 1 crawl (same size as on the server, 3,380,103 bytes; Last-Modified 2026-08-17). The title
slide reads "Deep Reinforcement Learning", "Alexander Amini", "January 7, 2026"; the catalog title is
"Reinforcement Learning", which the wiki and slide file use as their heading (as lecture 3 does). PDF
metadata: author "A. Amini, A.P. Amini. MIT 6.S191", producer "macOS Version 26.1 (Build 25B78) Quartz
PDFContext" — not PyFPDF, unlike lectures 1–4 — created 2026-01-07.

**Deck format and numbering.** Despite the different exporter, the same format: every page is one
1280×720 JPEG (DCTDecode, so the stream is the JPEG file), no text layer, no two pages identical. A strip
of the bottom 10% of pages 2, 8, 15, 22, 29, 36, 43, 50, 57 and 58 showed the standard footer with
"1/7/26" and no slide number (the credit "Mnih+ *Nature* 2015." beside it on 29); 50 is a blue section
divider and 58 black. Slide N = PDF page N, checked with a plain 1..58 heading sequence.

**Licence.** No per-slide licence notices. Footer credits: "Mnih+ *Nature* 2015." (25–30, 32, 33),
"Williams *Reinforcement Learning* 1992." (42, 46), "Amini+ *IEEE RA-L* 2020." (47–49), "Silver+ *Science*
2016; Silver+ *Nature* 2017." (51), "Source: Wikipedia." (52), "Silver+ *Science* 2016." (53–56).
Uncredited third-party imagery: slide 2's robotic hand, slide 3's pictures (a car scene, robotic arms, a
Go board, the StarCraft II logo, a chat illustration), the Atari Breakout frames of 22–31 and 36–40 and
the summary (57), slide 47's mountain-road video still, and 58's T-shirt photograph. LICENSE.md lists
what is in the images.

**Slide transcription.** The 58 page JPEGs were extracted with `get_image_info(xrefs=True)` and read by
two Sonnet agents in parallel (1–29 and 30–58; the second read page 29 for build-step context), each
appending as it went; the parent merged the parts and wrote the header, section table and Images note.
The second reader first numbered its entries one too high and renumbered them before finishing; the
1..58 heading check passed. 47 slides are tagged `*Figure: yes*`. Parent edits: slide 52's exponents
written as LaTeX; 42 formulas that stood alone inside quotes unquoted and five whole quoted lines that
began with a formula unquoted; ten `*Figure: yes*` lines split around their math; three
`\operatorname{argmax}_ {a}` subscripts spaced; slide 17's discount-factor line rephrased — until
`check_math.mjs` reported 0 errors and 0 warnings.

**Figure audit.** A separate Sonnet agent checked slides 7, 15, 17, 18, 19, 22, 26, 28, 30, 31, 32, 33, 37,
38, 39, 40, 42, 46, 48, 52, 53 and 56 against the page JPEGs with enlarged crops. Nothing described was
absent from its page. Exact: slide 7's faded captions; the formulas of 15, 17–19, 28 and 30 (norm bars,
square, primes); 31's values; slide 33's 49 game labels and their order, its axis, line and arrow;
slide 42's labels, including the $a_3$ of the third; 46's loss and update; every cell of slide 52's
table, with its "n x n" header. Discrepancies on **6 pages**, all fixed: slide 32's second convolution
block (two sub-columns of seven, not "five"); slide 33's "~" before Seaquest, Bowling and Private Eye
were error-bar caps, the grey bar exceeds the blue on four games (Double Dunk, Tennis, Kung-Fu Master,
Centipede), not "a few … most clearly Double Dunk", and the legend is two rotated rectangles; slides 37
and 40's braces sit below their expressions, and both titles have two spaces after the colon; slide
38's axis has arrowheads at both ends and the Stay bar is a quarter of Left's height; slide 48's frame
list had 17 descriptions for 18 frames. Also adopted: slide 42's trajectory bends right before left.
The auditor read Road Runner as "closer to 222%"; the parent's crop reads 232%, kept with a note that
the middle digit is blurred. The parent looked at the images of slides 33 (the chart, values as now
transcribed) and 46 (the policy-gradient loss and both update lines, exactly as transcribed, upright P
and bold **loss** included).

**Printed slips and as-printed oddities**, all reproduced as printed:

- Slide 42 labels its third trajectory point $(s_2, a_3, r_2)$; the wiki notes the break in pattern.
- Slides 17 and 18 write the discounted return two ways, $\gamma^{i} r_i$ summed from $i = t$ and
  $r_t + \gamma r_{t+1} + \cdots$; the wiki notes from the formulas alone that they differ by $\gamma^{t}$.
- Slide 33 puts 29 games on the "Surpass human-level" side of its line, seven of them under 100%
  (Enduro 97% to H.E.R.O. 76%), and states no threshold; the wiki says so from the chart's own numbers.
- Slide 7 is a frame caught mid-animation, its faded supervised caption reading "This is an apple."
  where slides 4–6 print "This thing is an apple."; slides 21 and 35 fade one panel each.
- Slide 10's second definition and slide 19's policy sentence have no full stop, and 19 prints a plain
  "s"; slide 52's header prints "n x n" where its rows print "×"; slides 22–24 print "Example:" with two
  spaces after the colon, and slides 37 and 40 their titles.
- Slide 51 credits "Silver+ *Science* 2016; Silver+ *Nature* 2017.", slides 53–56 "Silver+ *Science* 2016."

**Spoken vs printed.** The data as "triplets" of states, actions and rewards (≈3:56) against slide 6's
"state-action pairs"; the Q-loss as an "absolute value" (≈26:58) against slide 30's squared norm; the
captions' "23 or zero" (≈27:44) against slide 31's 20, 3 and 0; the target's $Q(s', a')$ called "the
actual reward" and "probably a misnomer" (≈33:52–34:39); human level surpassed "on over 50%" of the
games (≈31:35) against slide 33's 29 of 49; "the first time any autonomous vehicle was ever trained
end-to-end in simulation" (≈51:35) against slide 49's "First full-scale autonomous vehicle trained using
RL entirely in simulation"; and Breakout's "two actions" corrected aloud to three (≈20:03–20:48). The
wiki gives both sides and lists them in a "Spoken versus printed" section.

**Transcript.** YouTube auto-captions, already punctuated. Copy-edited by a Sonnet agent against the slide
file: 74 "uh"/"um", the `>>` marks, stutters and false starts removed ("You train this using policy grade
You train this using gradient descent"); "RFT" to R of T (45:26), "breakout" to Breakout (30:47). 38
`[Student: …]` marks: the lecture has about twenty questions and an audience poll. Kept with [Ed] notes:
"23 or zero" (27:44, citing slide 31's 20, 3 and 0) and "the last lecture that we saw with VAEs that I
have a gave" (38:31, unclear; lecture 4 was given by Ava Amini). The parent removed a third [Ed] note the
agent added unasked at 18:31, which proposed that "the Q function is what is being discussed" where the
captions say "R of T"; normalized the agent's "R of t" to the captions' "R of T"; and closed and reopened
four student turns that the agent had left open across a mark (21:35, 40:50, 55:25, 56:56), which went
into AGENTS.md as a general rule. Checks re-run by the parent: 77 of 77 `[MM:SS]` marks identical, number
inventory identical, per-paragraph word ratio 0.90–1.00.

**Coverage gaps.** The preference-alignment passage on language models (53:53–54:39) has no slide beyond
slide 3's panel. The learning-from-scratch slide shown in answer to a question (54:39–55:25), with its
green baselines and Stockfish, is not in the published deck. The Breakout, mountain-road, VISTA and
deployment videos (23, 24, 47–49) are played, not described; slide 33's chart and slide 52's table are
summarized aloud, not read.

**Images.** 19 of 58 pages, copied byte for byte from the deck's own JPEGs (1.1 MB): 6, 10, 17, 22, 26,
30, 31, 32, 33, 37, 38, 39, 40, 42, 43, 44, 45, 48, 56. All 19 are embedded in
`wiki/05-reinforcement-learning.md` by hand, in the passage citing each, and under their headings in the
slide file (by `embed_slide_images.py`); the three new topic pages reuse 6. Not rendered, and why:

- Title, text, equation and section-divider slides: 1, 18, 19, 20, 21, 34, 35, 46, 50.
- Build steps wholly contained in an included slide: 4–5 (→6), 8–9 (→10), 11–16 (→17; their
  equations are transcribed), 25 (→26), 27–29 (→30), 53–55 (→56).
- A frame caught mid-animation: 7 (slide 6 with two columns fading).
- Repeats of an included figure: 36 (31 without the return arrow), 41 (17's loop beside the case-study
  text).
- Video stills: 23 and 24 (the two Breakout policies), 47 (a car on a mountain road), 49 (the deployed
  car; its text is transcribed). Slide 48's still is kept: its grid of simulated frames is the content.
- Decorative, application and stock pictures: 2, 3, 51 (a Go photograph).
- A table transcribed cell by cell: 52 (its Go board diagram is generic).
- The summary (57) and announcements (58).

**AGENTS.md lessons** (general form): a student turn that runs across an `[MM:SS]` mark is closed before
it and reopened after it. The deck-format bullet now records that lecture 5's deck came from a different
exporter in the same image-only format.

**Cost.** Measured with `measure_run_cost.py` after the lecture push: \$9.38 for the whole lecture. The Opus parent cost \$7.17 (75 calls, ending at 195k context) and the four Sonnet agents \$2.21 (24%): two slide readers at \$0.43 and \$0.42, the audit \$0.73 and the copy-edit \$0.63. Another ~\$0.22 of output is logged incompletely and not counted. The closing bookkeeping commit is not included.

#### Run checklist (moved verbatim from TODO.md)

_Run 5 — lecture 5 (Reinforcement Learning, 2026)_

Catalog position 5, video 1ij3dweHu-0 (59:19). Deck `slides/6S191_MIT_DeepLearning_L5.pdf`: 58 pages,
each one 1280×720 JPEG (DCTDecode), no text layer (macOS Quartz PDFContext, created 2026-01-07), footer
"1/7/26" with no slide number (checked on a strip of 10 footers; 50 is a blue page, 58 black): slide N = page N.

- [x] Verbatim captions → raw/transcripts/original/05-reinforcement-learning.md (77 marks)
- [x] raw/slides/05-reinforcement-learning.md — two Sonnet readers (1–29, 30–58), merged, header (47 figure slides)
- [x] Figure audit (Sonnet) of chart-, equation-, code- and diagram-heavy pages; parent checks two images (22 pages; fixes on 32, 33, 37, 38, 40, 48, plus 42 detail; parent: images of 33 and 46, crop of 33)
- [x] raw/transcripts/05-reinforcement-learning.md — Sonnet copy-edit; marks, numbers, ratios checked (77/77, identical, 0.90–1.00)
- [x] raw/images/05-reinforcement-learning/ — native page JPEGs of figure slides, embedded (19 of 58, 1.1 MB)
- [x] wiki/05-reinforcement-learning.md
- [x] Topic pages, new and extended (new: reinforcement-learning, q-learning, policy-gradients; extended: what-is-deep-learning, loss-functions, gradient-descent, computer-vision, convolutional-neural-networks, autoencoders-and-vaes; lecture 3 page)
- [x] INDEX.md, AGENTS.md image table, LICENSE.md, sources.md, kb.json, BUILD_LOG.md (sources.md already listed the deck)
- [x] verify_kb.py clean, and its review section read
- [x] Commit and push (54ba1ea)
- [x] Move this section to BUILD_LOG.md

## Lecture 6 — Language Models and New Frontiers (2026) — built 2026-10-18

**Pointers.** Catalog position 6, video `ev7cLSd-ySE` (56:17), delivered 7 January 2026 by Ava Amini, the
last lecture by the two instructors before the guest lectures. Deck
<https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L6.pdf>, 81 pages, downloaded in the lecture 1
crawl (same size as on the server, 5,321,498 bytes; Last-Modified 2026-08-17). The title slide reads "Deep
Learning Limitations and New Frontiers", "Ava Amini", "January 7, 2026"; slide 3's schedule calls it "New
Frontiers"; the catalog title is "Language Models and New Frontiers", which the wiki and slide file use as
their heading. PDF metadata: author "A. Amini, A.P. Amini. MIT 6.S191", producer "PyFPDF 1.7.2", created
2026-01-10.

**Deck format and numbering.** Every page is one 1280×720 JPEG (DCTDecode), no text layer. A strip of the
bottom 10% of pages 2, 9, 17, 25, 33, 41, 49, 57, 65, 73, 80 and 81 showed the standard footer with "1/7/26"
and no slide number (credits "Zhang+ *ICLR* 2017." on 17 and "OpenAI. Ramesh+ *arXiv* 2022" on 65 beside
it); 9 is a blue divider, 80 a film still and 81 black. Pages 80 and 81 are byte-for-byte copies of 78 and
79 (MD5 of the page JPEGs). Slide N = PDF page N, checked with a plain 1..81 heading sequence.

**Licence.** No per-slide licence notices. Footer credits: "Hornik+ *Neural Networks* 1989." (12–13),
"Zhang+ *ICLR* 2017." (16–22), "U. Muller, 6.S191 2018." (29), "P. Isola 6.869." (30–31), "ABC News."
(32), "Despois "Adversarial examples" 2017." (34), "Goodfellow+ *NIPS* 2014." (39), "Athalye+ *ICML*
2018." (42), "Sohl-Dickstein+ *ICML* 2015; Ho+ *NeurIPS* 2020." (51), "Ho+ *NeurIPS* 2020." (54),
"Ramesh+ *arXiv* 2022" (64), "OpenAI. Ramesh+ *arXiv* 2022" (65), "Wei+ TMLR 2022." (75), "Google AI
blog." (76); in-slide citations on 66 and "Wang+ *arXiv* 2023." on 74. Uncredited third-party imagery: the
prize photographs (4–5), guest portraits and company logos (7), staff photographs (8), slide 10's news
collage, slide 11's brain image, slide 29's alchemist painting, slide 33's photographs, slide 43's
headlines, the domed-building photograph of 49–54, slide 49's generated cats, the dog of 55–61, slide 68's
ChatGPT screenshot and OpenAI logo, the Yoda film still (78, 80) and the T-shirt (2, 79, 81). LICENSE.md
lists what is in the images.

**Slide transcription.** The 81 page JPEGs were extracted with `get_image_info(xrefs=True)` and read by
three Sonnet agents in parallel (1–27, 28–54, 55–81; the second and third read the page before their range
for build-step context), each appending as it went; the parent merged the parts, wrote the header, section
table and Images note, and moved the watermark mention into the header. 61 slides are tagged
`*Figure: yes*`. No math changes were needed (`check_math.mjs` clean).

**Figure audit.** A separate Sonnet agent checked slides 5, 6, 12, 14, 21, 22, 23, 28, 33, 36, 38, 39, 41,
42, 50, 53, 54, 60, 61, 66, 70, 71, 74, 75 and 76 against the page JPEGs with enlarged crops. Nothing
described was absent from its page. Exact: slide 5's bullets and the "RTX 5080" card under the caption
"NVIDIA 5070 GPU"; slide 6's faded earlier text; slide 14's years and labels; slides 21–22's bars and
annotation; slide 33's tags; the formulas, highlights and callouts of 36–41; slide 42's 24 border colours
row by row (1 green, 17 red, 6 black); slide 53's table; slides 60–61's labels; slide 66's citations; slide
71's arrows; slide 74's garbled prompt; slide 75's three charts (ticks, baselines, series and values within
about 0.2 decade). Discrepancies on **4 pages**, all fixed: slide 12's node columns are 8, 9, 9, 9 and 4
(not 9, 10, 10, 10, 4); slides 23 and 28 have 17 dots (not 18 and "about 18"); slide 28's second subtitle
line is regular weight; slide 54's magenta underline includes "T,". The parent looked at the images of
slides 41 (the adversarial-image update and its callout, exactly as transcribed, bold θ against the
formula's $W$) and 75 (the charts, as transcribed), and at a crop of slide 30: the student's "Green on the
ear" (≈20:17) pointed at a detail the reader had not described, and slide 30's entry now gives the
green-tinted left ear and the pink patch below the nose.

**Printed slips and as-printed oddities**, all reproduced as printed:

- Slide 41's callout says "Fix your weights $\boldsymbol{\theta}$," while every formula on 36–41 writes $W$.
- Slides 60 and 61 label the same final sampled image "T0 (end)" and "T-5 (end)"; slide 53 numbers the
  forward process $T = 0$ (clean) to $T = 4$ (noise), and slide 54 prints "T-1" with a hyphen.
- Slide 5's photographed card reads "RTX 5080" under the caption "NVIDIA 5070 GPU".
- Slide 6 is a frame caught mid-animation: its faded Option 1 text is an earlier version ("3 minutes
  (strict)", "Friday, Jan 29", "Submit groups by Wednesday…") under the new Option 2.
- Slide 12's unlabelled network has five columns of nodes beside the statement "a single layer".
- Slides 79 and 81 print the deadline line without an item number.

**Spoken vs printed.** The pitch length "between three to five minutes" (≈2:27) against slide 5's "5
minutes (strict)" (an [Ed] note in the transcript); the theorem's "single hidden layer" (≈8:40) against
slide 12's "single layer"; "model collapse" (≈29:37) against slide 48's "Mode collapse"; and the
time-step labels above. The wiki lists them in a "Spoken versus printed" section, with the slides not
discussed aloud (12's drawing, 64–65, 68, 73, 76's "8 billion parameters").

**Transcript.** YouTube auto-captions, already punctuated. Copy-edited by a Sonnet agent against the slide
file: 29 "uh"/"um", the `>>` marks, stutters and false starts removed; "Matthias" to Mathias (4:47), "Jax"
to JAX (5:33; the captions already write JAX once), "web text" to WebText (44:52). Student turns marked at
20:17 ("Green on the ear", run into the lecturer's speech by the captions, and confirmed by slide 30's
image), 34:58 (two answers), 38:01–38:47 (closed and reopened across the mark), 39:34 (two questions) and
41:51. The agent added one [Ed] note (34:58: the student's "T3" and "T1" against slide 53's T = 0 for the
clean image). The parent added a second at 2:27 (the pitch length, which the agent had checked and
deliberately left without a note, contrary to the rule), removed a leftover "the the" at 41:51, and
corrected the header. Checks re-run by the parent: 73 of 73 `[MM:SS]` marks identical, number inventory
identical, per-paragraph word ratio 0.93–1.00. Every restored proper noun is printed in the deck (Mathias,
WebText); JAX, ImageNet, Gemini and Copilot are as captioned.

**Coverage gaps.** Slide 44's list is read only in part ("not comprehensive at all", ≈27:18); slides 64–65's
text-to-image examples, slide 68's ChatGPT screenshot, slide 73's capabilities and slide 76's tree are shown
without being discussed. The claim that well-calibrated language models will necessarily hallucinate
(≈51:43) and the tuning of base models into chatbots (≈49:25) have no slide. The lecture names no loss
formula for diffusion or next-token prediction, and does not discuss the architecture of LLMs; the wiki
writes none and says so.

**Images.** 24 of 81 pages, copied byte for byte from the deck's own JPEGs (1.6 MB): 14, 18, 22, 26, 28, 29,
30, 31, 34, 42, 49, 50, 51, 53, 54, 61, 64, 65, 66, 69, 71, 72, 75, 76. All 24 are embedded in
`wiki/06-language-models-new-frontiers.md` by hand, in the passage citing each, and under their headings in
the slide file (by `embed_slide_images.py`); the three new topic pages reuse three or four each. Not rendered, and
why:

- Title, logistics, prize, staff and guest-lecturer slides: 1–8; the closing lab and announcement slides
  78–81 (a film still and a T-shirt, 80–81 repeating 78–79).
- Section dividers: 9, 15, 47, 67.
- News, stock and product imagery whose text is transcribed: 10 (a news collage), 11 (a stock brain image
  between "Data" and "Decision"), 32 (ABC News coverage of the autopilot crash; its point is carried in the
  prose, as lecture 1's slide 6 was), 33 (example photographs), 43 (headlines), 68 (a ChatGPT screenshot and
  logo).
- Slide 12's unlabelled, generic network drawing (the theorem's statement is transcribed; the drawing's
  five columns are noted).
- Text, equations or generic icons transcribed exactly: 13, 36–41 (the two update rules and their
  highlights), 44–46, 73, 74, 77.
- Build steps contained in an included slide: 16–17 (→18), 19 (18's relabelling restyled, without the
  dice), 20–21 (→22), 23–25 (→26), 27 (→28), 35 (34 faded), 48 (→49; its lists are transcribed), 52 (→53),
  55–60 (→61; 57–60 caught mid-animation); and 70, which 72 repeats.
- Two full-frame noise frames: 62, 63.

**AGENTS.md lessons** (general form): send every count a transcription states to the audit; where the talk
points at a detail of a figure, check the slide file describes it. The deck-format bullet now covers
lecture 6.

**Cost.** Measured with `measure_run_cost.py` after the lecture push: \$9.90 for the whole lecture. The Opus parent cost \$7.55 (73 calls, ending at 206k context) and the five Sonnet agents \$2.34 (24%): three slide readers at \$0.37, \$0.43 and \$0.56, the audit \$0.50 and the copy-edit \$0.48. Another ~\$0.13 of output is logged incompletely and not counted. The closing bookkeeping commit is not included.

#### Run checklist (moved verbatim from TODO.md)

_Run 6 — lecture 6 (Language Models and New Frontiers, 2026)_

Catalog position 6, video ev7cLSd-ySE (56:17). Deck `slides/6S191_MIT_DeepLearning_L6.pdf`: 81 pages,
each one 1280×720 JPEG (DCTDecode), no text layer (PyFPDF 1.7.2, created 2026-01-10), footer "1/7/26"
with no slide number (checked on a strip of 12 footers; 9 is a blue page, 80 a film still, 81 black;
pages 80–81 repeat 78–79 byte for byte): slide N = page N.

- [x] Verbatim captions → raw/transcripts/original/06-language-models-new-frontiers.md (73 marks)
- [x] raw/slides/06-language-models-new-frontiers.md — three Sonnet readers (1–27, 28–54, 55–81), merged, header (61 figure slides)
- [x] Figure audit (Sonnet) of chart-, table-, equation-, code- and diagram-heavy pages; parent checks two images (25 pages; fixes on 12, 23, 28, 54; parent: images of 41 and 75, crop of 30, which added 30's green ear)
- [x] raw/transcripts/06-language-models-new-frontiers.md — Sonnet copy-edit; marks, numbers, ratios checked (73/73, identical, 0.93–1.00)
- [x] raw/images/06-language-models-new-frontiers/ — native page JPEGs of figure slides, embedded (24 of 81, 1.6 MB)
- [x] wiki/06-language-models-new-frontiers.md
- [x] Topic pages, new and extended (new: limitations-of-deep-learning, diffusion-models, large-language-models; extended: generative-modeling, sequence-modeling, loss-functions, gradient-descent, regularization, what-is-deep-learning, computer-vision, generative-adversarial-networks, autoencoders-and-vaes, attention-and-transformers, reinforcement-learning; lecture 2, 4 and 5 pages)
- [x] INDEX.md, AGENTS.md image table, LICENSE.md, sources.md, kb.json, BUILD_LOG.md (sources.md already listed the deck)
- [x] verify_kb.py clean, and its review section read (13 github math errors in new captions fixed first)
- [x] Commit and push (409b8bf)
- [x] Move this section to BUILD_LOG.md

## Lecture 7 — The Three Laws of AI (2026) — built 2026-10-18

**Pointers.** Catalog position 7, video `XKOpA7iaJvg` (51:49), delivered 9 January 2026 by Douglas Blank,
Head of Research at Comet ML. It is a guest lecture, introduced by Ava Amini. Deck
<https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L7.pdf>, 44 pages, downloaded in the lecture 1
crawl (same size as on the server, 1,546,665 bytes; Last-Modified 2026-08-17). The title slide reads "The Three
Laws of AI", "Douglas Blank, Ph.D.", "January 9, 2026, Boston, MA, USA". The course site's schedule lists it as
Lecture 7, 9 January 2026, with the abstract that slide 2 reproduces. PDF metadata: title "The Three Laws of
AI", creator "Google", no producer or dates.

**Deck format and numbering.** Unlike decks 1–6, a Google Slides export (720×405 pt) with vector pages and a
text layer (13,590 characters). Rasters sit on 12 pages only: 3, 4, 11, 12, 16, 19, 20, 21, 25, 35, 40 and 44.
`slide_number_map.py` reads the printed numbers 1:1 with the pages. Pages 1, 13 and 14 print none where it
looks; slide 14 prints "14" at top left, in the older template of slides 13–14. `--verify` passes. There are no
page JPEGs to extract, so the readers got 1280×720 renders and a text-layer dump per page.

**Licence.** The deck carries no licence notice. The site's FAQ says "All materials are open-sourced to the
world for free and are copyrighted under the MIT license". The deck was treated as covered, and LICENSE.md
credits it to Douglas Blank as well as to the course. Credits and sources printed on the slides:

- slide 3: "Atlas, Boston Dynamics";
- slide 4: "Tandy Color Computer advertisement from Personal Computing August 1982, featuring Isaac Asimov";
- slide 20: "star-history.com";
- slides 28–29: an SFGate article URL;
- slides 30–31: github.com/dsblank/developing-agentic-ai/blob/main/Recommendations.md;
- slide 33: "- Gemini" for the quoted definition;
- slides 36–37: the "Based on ideas from" list of frameworks.

Uncredited: slide 16's infographic, slide 40's screenshot of YouTube comments by individuals, and slide
44's QR code.

**Slide transcription.** Two Sonnet readers (1–22 and 23–44), each appending as it went. Each got the renders
and the per-page text layer, the latter for the spelling of printed prose only, with the page image as the
authority. They reported these layer-versus-page differences:

- slide 1's layer holds the footer line, which the page does not show;
- the layer puts slide 43's "-1." label and slide 44's caption last;
- the pictures on 4, 11–12, 16, 20–21, 25, 35 and 40 have no text in the layer.

The parent merged the parts and wrote the header: numbering, footer, Images note and contents. It also made
these fixes:

- moved slide 1's layer note out of its Text line;
- dropped a reader's guess that slide 16's infographic "looks AI-generated";
- fixed slide 22's doubled quote marks;
- relabelled the mislabelled "Build step" lines of slides 29 and 40;
- escaped the advertisement's three dollar signs (`\$399⁹⁵`, `\$98`), which would otherwise pair into inline
  math.

12 slides are tagged `*Figure: yes*`.

**Figure audit.** A separate Sonnet agent checked 18 pages against enlarged crops rendered from the vector
PDF: 4, 10, 11, 12, 14, 16, 20, 21, 22, 25, 26, 28, 29, 35, 40, 42, 43 and 44. Nothing described was absent
from its page. These were exact:

- slide 10's code;
- slide 11's six rows, and slide 12's box (the 1990s and 2000s rows);
- slide 14's columns and the position of its number;
- slide 21's eleven sidebar counts;
- slides 22 and 26;
- the quotations of slides 28–29, including the unmatched quote;
- slide 35's terminal text;
- the boxes of slides 42–43;
- slide 44.

Discrepancies on **5 pages**, all fixed:

- **Slide 4.** The advertisement's body copy, which the reader called too small, is legible in a crop and
  is now transcribed in full. The monitor screen is yellow-green, not green.
- **Slide 16.** The bottom row's chevron colours differ from the top row's at positions 5 and 8.
- **Slide 20.** The curve values: about 4K at the 2025 tick, 10K about 40% of the way through 2025, and 17K
  at 2026.
- **Slide 25.** "Variables" is a group header, not a column. The question wraps over five lines, and the
  variable names are underlined.
- **Slide 40.** The reply reads "Don't build it then", where the reader had reported a missing "it" as a
  printed slip. All three comments have a three-dot menu.

The parent looked at the rendered images of slide 16 (labels, dates and inconsistencies as transcribed) and
slide 20. On slide 20 it independently moved the 10K point from "late in 2025" to mid-2025, as the audit also
did.

**Printed slips and as-printed oddities**, all reproduced as printed:

- Slides 6–7 write "AI systems … given to it" and "protect its own existence". Law 0 on slide 7 and law
  −1 on slide 43 have no full stop.
- Slide 9: "Very influential the areas of". Slide 10: "the semantic of the laws".
- Slide 16's timeline:
  - "Breakthough";
  - "ChatGPT" garbled;
  - GPT-3 labelled "(2020)" but dated 2022;
  - the third and seventh stages labelled with years, the third dated 2020.
- Slide 17: "Shoulders Of Giants". Slide 20: lowercase "github".
- Slide 26: "a LLM" and "each which has been evaluated". Slide 27: "So, Can".
- Slide 28's quotation ends with an unmatched closing quote after "Xanax."
- Slide 40's reply "yaa, its correct". Slide 43's box cuts through "humanity".

**Spoken vs printed.** The wiki's "Spoken versus printed" section lists:

- slide 2's "Three New Laws" against versions with three laws plus one, and four plus two;
- "the last 10" (26:27) against "the last three" (27:14), an [Ed] note in the transcript;
- law 0 spoken as "don't build it. Don't deploy it" against slide 42's "don't deploy it";
- the live agent's "January 12th" for next Thursday, which the lecturer calls wrong;
- slide 35's screenshot, which is a different session from the live demonstration.

**Transcript.** YouTube auto-captions, already punctuated, copy-edited by a Sonnet agent against the slide
file. Restorations:

- "Opic", "OPIC" and "Opaque" to Opik; the lecturer spells it at 13:22.
- comet-ml/opik (14:07).
- "slides 28 and 29" (1:44).
- Tandy Color Computer, and A Tale of Two AIs.
- "the LLM" (23:22).
- "six bears" (24:56, 31:54).
- ChatGPT, and GPT-4o Mini (29:35).
- Ethically Aligned Design (46:45).
- Gemini and "agentic" at 35:47, where the captions read "Jim and I, what is a genic AI"; an [Ed] note.
- The 28:49 model list "4o Mini, 4o 5" to GPT-4o Mini, GPT-4o, GPT-5, which the captions name at 30:22; an
  [Ed] note.

Eight [Ed] notes in all: 8:44, 16:26, 17:14, 27:14, 28:49, 32:41, 35:47 and 43:41. Student turns are marked at
18:00–18:47 (closed and reopened across the mark), 19:32 (two students), 29:35, 38:59 and 39:44. The header
notes that 0:12–0:57 is Ava Amini's introduction.

The parent accepted the Gemini and model-list restorations, which slide 33 and the captions at 30:22 support.
It reverted a comma the agent had put into "the new Atlas Boston Dynamics robot" and a capital S in "slides 28
and 29". Checks re-run by the parent: 67 of 67 `[MM:SS]` marks identical, number inventory identical,
per-paragraph word ratio 0.83–0.99. Opik, comet-ml/opik, Tandy, Gemini, Ethically Aligned Design and
"six-bears" are printed in the deck. GPT-4o and GPT-5 are as captioned. "Ryan Hodges" and "Karan Lowe" are
kept as spoken (slide 40 prints the handles @RyanHodges-u3n and @KaranLo-fi4673).

**Coverage gaps.**

- The demonstrations' Python metric, four-model chart and tool code were shown on screen only. Gemini 2.5
  Flash's score is not stated aloud.
- The captions break off at ≈8:44 ("a very symbol") and ≈42:52, where part of the sentence on tools as an
  emergent layer is lost.
- Shown without discussion: slides 14, 16 and 19, and recommendations 1–4 and 6–8 of slide 30.
- The Q&A after 51:20 is not in the recording.

The wiki names the YouTube commenters only as "a commenter"; the slide file and transcript keep the handles
as printed and spoken.

**Images.** 4 of 44 pages: 16, 20, 21 and 25. They are 1400×788 renders by `extract_slide_images.py --format
auto`, all of which came out JPEG (0.39 MB). All four are embedded in `wiki/07-three-laws-of-ai.md` by hand,
and under their headings in the slide file by `embed_slide_images.py`. Not rendered, and why:

- Title and abstract: 1–2.
- Photographs and advertising whose text is transcribed: 3 (Atlas), 4 (the 1982 advertisement).
- Text and code slides, including the section-title slides and the old talk's slides 13–14: 5–10, 13–15,
  17–18, 22–24, 26–34, 36–39 and 41–43.
- The table pasted as a picture, transcribed exactly with slide 12's highlight: 11–12.
- The Opik logo: 19.
- Text screenshots transcribed exactly: 35 (a terminal) and 40 (YouTube comments by individuals).
- The contact slide's QR code: 44.

**Wiki.** New topic pages: ai-safety, llm-evaluation and ai-agents. Extended:

- large-language-models, with a new section "Prompts, jailbreaks and tools in practice";
- what-is-deep-learning, with lecture 7's history;
- limitations-of-deep-learning, with a link on jailbreaks;
- reinforcement-learning, with the other sense of "agent".

Lecture 6's list of guest lectures now links to lecture 7.

**AGENTS.md lessons** (general form):

- The deck-format bullet now describes two kinds of deck: image-only, and vector with a text layer.
- For a vector deck, readers get renders, and the text layer serves only for the spelling of prose.
  Audit crops are rendered from the PDF, and images are rendered at 1400px.
- Readers invent printed slips as well as normalise real ones, so every slip a reader claims goes to the
  audit.

**Cost.** Measured with `measure_run_cost.py` after the lecture push: \$8.61 for the whole lecture. The Opus
parent cost \$6.99 (68 calls, ending at 190k context) and the four Sonnet agents \$1.63 (19%): the two slide
readers at \$0.36 and \$0.39, the audit \$0.54 and the copy-edit \$0.34. Another ~\$0.21 of output is logged
incompletely and not counted. The closing bookkeeping commit is not included.

#### Run checklist (moved verbatim from TODO.md)

_Run 7 — lecture 7 (The Three Laws of AI, 2026)_

Catalog position 7, video XKOpA7iaJvg (51:49), a guest lecture by Douglas Blank (Comet ML), 9 January
2026. Deck `slides/6S191_MIT_DeepLearning_L7.pdf`: 44 pages, a Google Slides export (720×405 pt) with a
text layer and vector pages; rasters on 12 pages only (3, 4, 11, 12, 16, 19, 20, 21, 25, 35, 40, 44).
Printed slide numbers equal PDF pages (`slide_number_map.py`: 1:1; pages 1, 13, 14 print none), so
`--verify` applies. No native page JPEGs exist: readers get 1280×720 renders, images are rendered.

- [x] Verbatim captions → raw/transcripts/original/07-three-laws-of-ai.md (67 marks)
- [x] raw/slides/07-three-laws-of-ai.md — two Sonnet readers (1–22, 23–44), merged, header (12 figure slides)
- [x] Figure audit (Sonnet) of figure-, screenshot- and code pages; parent checks two images (18 pages; fixes on 4, 16, 20, 25, 40; parent: images of 16 and 20)
- [x] raw/transcripts/07-three-laws-of-ai.md — Sonnet copy-edit; marks, numbers, ratios checked (67/67, identical, 0.83–0.99)
- [x] raw/images/07-three-laws-of-ai/ — rendered figure slides, embedded (4 of 44, 0.39 MB: 16, 20, 21, 25)
- [x] wiki/07-three-laws-of-ai.md
- [x] Topic pages, new and extended (new: ai-safety, llm-evaluation, ai-agents; extended: large-language-models, what-is-deep-learning, limitations-of-deep-learning, reinforcement-learning)
- [x] INDEX.md, AGENTS.md (deck-format bullet, image table), LICENSE.md, sources.md, kb.json, BUILD_LOG.md (sources.md already listed the deck; lecture 6 page links to lecture 7)
- [x] verify_kb.py clean, and its review section read (check_math --github: 0 errors; the 9 warnings are lecture 1's open item)
- [x] Commit and push (c532791)
- [x] Move this section to BUILD_LOG.md

## Lecture 8 — AI for Science (2026) — built 2026-10-18

**Pointers.** Catalog position 8, video `rZACoZD8AG8` (59:10), a guest lecture by Chris Bishop, Technical
Fellow at Microsoft Research AI for Science, introduced by a member of the course staff (the captions have
Bishop thank "Alida"). The course site's page source dates it 8 January 2026 in a comment and displays "May
18, 2026" (lecture 7: 9 January, displayed "May 11, 2026"); the introduction calls Bishop the first guest
speaker, so it was delivered before lecture 7. Deck
<https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_L8.pdf>, 31 pages, downloaded in the lecture 1
crawl (same size as on the server, 8,445,006 bytes; Last-Modified 2026-08-17). PDF metadata: creator
"Acrobat PDFMaker 25 for PowerPoint", producer "Adobe PDF Library 25.1.5", author "Neeltje Berger", created
2026-01-20. The site's abstract: "how modern deep learning methods are being integrated into discovery
pipelines, focusing on concrete examples from atmospheric modelling, materials design, and drug discovery".

**Deck format and numbering.** A third kind of deck: a PowerPoint export (960×540 pt) with vector pages,
pasted pictures on 28 pages, and a sparse text layer (2,420 characters) holding the slide titles and the
deck's own labels but none of the pictures' text. `slide_number_map.py` finds no printed number on any page,
and the readers confirmed there is none and no footer, so slide N = PDF page N, checked as a plain 1..31
sequence. Readers got 1280×720 renders and a per-page text-layer dump.

**Licence.** The deck carries no licence notice. As for lecture 7, it was treated as covered by the site's
MIT licence, and LICENSE.md credits it to Chris Bishop as well as to the course. Credits and sources printed
on the slides:

- slide 4: "Paul Dirac, 1929" for the quotation (the portrait is uncaptioned);
- slide 8: the essay's own heading, "The Bitter Lesson", "Rich Sutton", "March 13, 2019";
- slides 12, 15 and 29: Nature article first pages with DOIs (Aurora, MatterGen, AI²BMD);
- slide 20: "Photo from the Nobel Foundation archive.", "Walter Kohn";
- slide 22: the Science web page of Mattsson (2002), with its DOI;
- slide 24: arXiv:2506.14665;
- slide 28: "Figure from “Cell Biology by the numbers”";
- slide 30: the Science cover of 14 August 2025; slide 31: the Springer book cover and BishopBook.com.

Uncredited: the renderings and illustrations, slide 14's photographs, slide 20's bar and pie charts, slide
21's photograph, slide 22's word cloud, and slides 23 and 25's charts.

**Slide transcription.** One Sonnet reader for all 31 pages, appending in chunks of 5–8. It tagged 27
slides `*Figure: yes*`. The parent tagged slide 4's portrait as a figure too (28), gave the untitled slides
(4, 8, 11, 12, 16, 17, 21, 25, 30) descriptive headings saying so, and wrote the header. The reader
reported no printed slips, and these layer-versus-page points:

- slide 23's layer holds "Weighted MAE (kcal/mol)", which the page does not show (confirmed by the audit);
- slide 20's layer garbles the cost formulas, which were read from the page;
- the pictures of slides 8, 12, 15, 22 and 29 have no text in the layer.

**Figure audit.** A separate Sonnet agent checked every slide from 2 to 31 against crops rendered from
the PDF at 600–800 dpi. Nothing described was absent from its page. These were exact:

- the equations of slides 2, 7, 9 and 27, character by character ($j\neq i$ and $i=1$ under the inner
  sums, $\epsilon_0$ against Maxwell's $\varepsilon_0$, the boxed $-\nabla_i U$);
- slide 3's digits and error bars;
- slide 8's essay text word for word, with its two-backtick opening quote before "brute force" and the cut-off;
- the Aurora and AI²BMD article pages of slides 12 and 29, all authors and superscripts;
- slide 17's 12 × 22 grid, slide 19's counts, and slide 25's eight points and legends.

Discrepancies on **8 pages**, all fixed:

- **Slide 9.** The input layer has 4 circles, not about 5.
- **Slide 14.** The energy-storage photograph shows "H₂", not "H"; the drug structure has three rings.
- **Slide 15.** Five author superscripts (Smith 3, Lu 6, Yang 4, Li 4, and envelopes after Tomioka and Xie)
  and one reference number (31, not 13).
- **Slide 20.** The bar values: first bar 1987, about 10,500 at 2015, 16,800 at 2020, 17,800 at the last
  bar (2022). The pie has 13 slices, seven of them unlabelled, not about eleven.
- **Slide 22.** The breadcrumb's quotes are straight. The word cloud's small words, "illegible at
  1280×720" according to the reader, were legible; the article text was legible too.
- **Slide 23.** No y-axis label confirmed; noted beside the layer's string.
- **Slide 28.** The "desired simulation timespan" banner runs from about the $10^{-9}$ tick to just past
  $10^0$.
- **Slide 31.** The book pages were legible: running heads "392  12. TRANSFORMERS" and "12.3. Transformer
  Language Models  393", Figures 12.20 and 12.21.

The parent then looked at the audit's crops of slide 22. The header was as reported, and the word cloud
held "MCY06", a mid-sized word that neither the reader (who listed the large words) nor the auditor (who
listed the small) had given. It also looked at the rendered images of slides 20 and 25: the bar heights,
the 13-slice pie and all eight scatter points matched. It did not adopt the auditor's "(sic)" reading of
the book's Figure 12.21 caption.

**Printed slips and as-printed oddities**, reproduced as printed: slide 23's "N³ ( larger prefactor)",
with a space after the parenthesis; slide 22's mix of straight quotes (web page) and curly quotes (scanned
article) around "Divine"; slide 8's two backticks opening "brute force" (the essay's own style). No other slip was found by reader or
audit.

**Spoken vs printed.** The wiki's "Spoken versus printed" section lists:

- "agree to 13 significant figures" (≈2:31), against slide 3's values, which share 12 and differ by 40 in
  the last two digits, inside the theory's ±86 (arithmetic on the printed numbers only);
- Aurora and AI²BMD, named only on the slides;
- slide 23's unlabelled y-axis, which Bishop calls the error in kcal/mol;
- slide 25's "Error on atomization energies", which Bishop calls "the total energy of the molecule";
- "up to about 10,000 atoms" aloud, against "more than 10,000 atoms" in slide 29's abstract;
- the book's year, captioned "2003", against slide 31's "best-selling book of 2024 and 2025".

**Transcript.** YouTube auto-captions, already punctuated, copy-edited by a Sonnet agent against the slide
file. Restorations:

- "Scala" to Skala (37:05, 38:36, 39:22; slide 24);
- "MatGen" and "Maturation" to MatterGen (23:16–25:35; slide 15);
- "Schrodinger" to Schrödinger (slide 22);
- "stitch signatures" to "stitched signatures" (46:15; slide 31);
- the parent added "complimentary" to "complementary" (7:07).

Ten [Ed] notes in nine paragraphs: 0:59 (the name "Alida"), 25:35 ("Matta Sim", not on the slides), 26:21,
38:36, 40:53, 45:29 (the book's year), 50:05 (the student's "no free lunch theorem"), 54:41 (two) and
55:27. The parent rewrote the 45:29 note to cite the lecturer's own "2 years running since this was
published" instead of only the slide, and corrected the header's sources for already-correct terms
(several it had attributed to slides are spoken only). Student turns at 47:00–47:47, 50:05–50:51,
53:55–55:27 and 56:58, closed and reopened across marks. The staff member's Q&A moderation (47:00, 53:55,
56:58, 58:31) is unmarked, as lecture 7's introducer was, and listed in the header. Checks re-run by the
parent: 77 of 77 `[MM:SS]` marks identical, number inventory identical, per-paragraph word ratio 0.84–1.01.
Skala, MatterGen, Schrödinger and "stitched signatures" are printed in the deck.

**Coverage gaps.**

- Aurora and AI²BMD are not named aloud, and the screening emulator is named only as captioned ("Matta
  Sim").
- The captions are garbled at 26:21 ("the service of magnet"), 38:36 (how much more data than before) and
  54:41.
- The denoising video (slide 16) and any other animation exist in the PDF as single frames.
- Shown without discussion: slide 11's storm, slide 14's application areas, the article pages of slides
  12, 15 and 29, and slide 31's book pages.

**Images.** 18 of 31 pages: 5–7, 9, 13, 15 and 17–28. They are 1400×788 renders by
`extract_slide_images.py --format auto`; 16 came out JPEG and two PNG (slides 5 and 6, flat diagrams),
1.7 MB in all. All 18 are embedded in `wiki/08-ai-for-science.md` by hand, and under their headings in the
slide file by `embed_slide_images.py`. Not rendered, and why:

- The title: 1.
- Equations reproduced in the slide file, and text or numbers transcribed exactly: 2, 3, 10.
- A portrait beside a quotation: 4.
- Screenshots of an essay and of journal articles whose text is transcribed: 8, 12, 29 (29's protein
  rendering is generic beside the article).
- An unlabelled picture of a storm, not discussed: 11.
- Photographs of application areas whose captions are transcribed: 14.
- A still from the MatterGen denoising video: 16.
- A journal cover and a book cover with an online reader: 30, 31.

**Math rendering.** `check_math.mjs` flagged 61 GitHub warnings in the slide file, none in the wiki: `$`
after a quote mark or a letter (labels such as `"$N^3$"`, `CO$_2$`, `r$^2$SCAN`) and `_` after `}`. Labels were
rewritten in Unicode or unquoted, and subscripts spaced (`\mathbf{x}_ i`); 0 warnings after.

**Wiki.** New topic page: ai-for-science. Extended: diffusion-models (MatterGen), large-language-models,
generative-modeling, attention-and-transformers and reinforcement-learning ("Where this comes up"). Lecture
6's list of guest lectures now links to lecture 8.

**AGENTS.md lessons** (general form):

- The deck-format bullet now describes three kinds of deck; the third is read like a vector deck and
  numbered like an image-only one.
- A list read off a picture needs the parent's own look at a crop, because reader and auditor split it by
  size and both can miss a middle item.
- A name printed on a slide but never spoken is attributed to the slide.
- A short printed label with a sub- or superscript beside a quote or a letter is written in Unicode.

**Cost.** Measured with `measure_run_cost.py` after the lecture push: \$10.34 for the whole lecture. The
Opus parent cost \$7.49 (77 calls, ending at 197k context) and the three Sonnet agents \$2.85 (28%): the
slide reader \$0.54, the figure audit \$1.84 (49 calls; it checked all 30 non-title pages) and the
copy-edit \$0.47. Another ~\$0.29 of output is logged incompletely and not counted. The closing
bookkeeping commit is not included.

#### Run checklist (moved verbatim from TODO.md)

_Run 8 — lecture 8 (AI for Science, 2026)_

Catalog position 8, video rZACoZD8AG8 (59:10), a guest lecture by Chris Bishop (Microsoft Research AI for
Science). Deck `slides/6S191_MIT_DeepLearning_L8.pdf`: 31 pages, a third kind of deck — a PowerPoint export
(Acrobat PDFMaker 25, 960×540 pt) with a sparse text layer (2,420 characters) and rasters on 28 pages.
`slide_number_map.py` finds no printed numbers: slide N = PDF page N, check headings with a plain 1..N
sequence check. Readers get 1280×720 renders plus the per-page text layer; images are rendered at 1400px.

- [x] Verbatim captions → raw/transcripts/original/08-ai-for-science.md (77 marks)
- [x] raw/slides/08-ai-for-science.md — Sonnet reader (1–31), merged, header (28 figure slides; 1–31 sequence checked)
- [x] Figure audit (Sonnet) of figure, chart and table pages; parent checks two images (slides 2–31; fixes on 9, 14, 15, 20, 22, 23, 28, 31; parent: crops of 22, images of 20 and 25 below)
- [x] raw/transcripts/08-ai-for-science.md — Sonnet copy-edit; marks, numbers, ratios checked (77/77, identical, 0.84–1.01; 10 [Ed] notes)
- [x] raw/images/08-ai-for-science/ — rendered figure slides, embedded (18 of 31, 1.71 MB: 5–7, 9, 13, 15, 17–28; slide file done, wiki by hand)
- [x] wiki/08-ai-for-science.md
- [x] Topic pages, new and extended (new: ai-for-science; extended: diffusion-models, large-language-models, generative-modeling, attention-and-transformers, reinforcement-learning; lecture 6 links to lecture 8)
- [x] INDEX.md, AGENTS.md (deck-format bullet, image table), LICENSE.md, sources.md, kb.json, BUILD_LOG.md (sources.md already listed the deck; lecture 6 page links to lecture 8)
- [x] verify_kb.py clean, and its review section read (check_math --github: 0 errors; the 9 warnings are lecture 1's open item)
- [x] Commit and push (40bc5dc)
- [x] Move this section to BUILD_LOG.md
