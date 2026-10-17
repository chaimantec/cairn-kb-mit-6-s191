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
