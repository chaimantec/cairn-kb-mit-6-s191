# Build log — MIT 6.S191 knowledge base

The per-lecture record of how this knowledge base was built and checked: each
deck's licence notices and lecture pointers, each transcript's edit and checks,
what each figure audit found, each deck's printed slips, and which slides were
rendered as images and why the others were not. It is a build record, **not
needed to answer questions**: every fact a learner needs is on the wiki page,
slide file or transcript it concerns. The rules every build follows are in
[`AGENTS.md`](AGENTS.md).

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

**Cost.** Measured with `measure_run_cost.py`: $8.64 for the whole lecture. The Opus parent cost $6.77 and the five Sonnet agents $1.86 (22%): three slide readers at $0.44–0.52 each, the copy-edit $0.26 and the audit $0.15. Another ~$0.21 of output is logged incompletely and not counted. Reading native 1280×720 page JPEGs instead of PDF page renders is why the deck cost about $1.45 to transcribe.
