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
