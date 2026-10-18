# How this knowledge base is organized

This repo is the knowledge base for **MIT 6.S191 — Introduction to Deep Learning**. It is read
by Cairn's in-extension AI chat, which starts at `INDEX.md`, fetches files over
raw.githubusercontent.com and follows relative markdown links.

The chat never reads this file. It is for whoever builds the KB, and Claude Code
loads it into every step of every build agent, so keep it to the rules every
lecture's build follows. The per-lecture record (licence notices, audit findings,
printed slips, which slides were rendered and why) goes in
[`BUILD_LOG.md`](BUILD_LOG.md); anything the chat needs goes in `INDEX.md`.

## Layout

| Path                | Contents                                                      |
| ------------------- | ------------------------------------------------------------- |
| `INDEX.md`          | Entry point. Course summary + annotated table of contents.    |
| `wiki/`             | Durable pages: one per lecture, plus cross-lecture topics.    |
| `raw/slides/`       | Full text of every slide, numbered. Slide N = PDF page N.     |
| `raw/transcripts/`  | Copy-edited transcripts with `[MM:SS]` paragraph marks — the ones to read. |
| `raw/transcripts/original/` | Verbatim YouTube captions, for reference.             |
| `raw/pdfs/`         | Decks downloaded from the course site. **Gitignored**; cite the site URL. |
| `raw/images/`       | Slide images. Linked from the pages using them.               |
| `sources.md`        | Crawl inventory: source URL, fetch date.                      |
| `TODO.md`           | Build tracker. Unchecked boxes are outstanding work.          |
| `BUILD_LOG.md`      | Per-lecture build record. Not needed to answer questions.     |
| `LICENSE.md`        | The course's MIT licence, attribution, third-party figures, image list. |
| `kb.json`           | Machine-readable coverage and provenance.                     |
| `SEE_ALSO.md`       | Sibling KBs the chat may read.                                |

## This course

- **Catalog vs editions.** The Cairn catalog holds 90 recordings: positions 1–9 are the 2026 edition,
  10–90 the 2018–2025 editions (each year re-records the core lectures, so titles repeat). Name files by
  catalog position (`01-…`, `10-…`), and give each lecture's page its year. The 2026 decks are
  `https://introtodeeplearning.com/slides/6S191_MIT_DeepLearning_LN.pdf`; earlier editions' decks are
  linked from the per-year archive pages (`/2025/index.html`, …), which the crawl has not yet visited.
- **Three kinds of deck so far.** The decks of lectures 1–6 are image-only exports (PyFPDF for
  1–4 and 6, macOS Quartz for 5): every page is one 1280×720 JPEG, with **no text layer** and **no printed slide numbers** (the footer's "1/5/26" is
  the lecture date). So `slide_number_map.py` finds nothing and `--verify` does not apply: use slide N =
  PDF page N, and check headings with a plain `1..N` sequence check. Check each new deck's text layer
  and footer before assuming the same. No text layer also means agents cannot grep for URLs or
  citations, and the PDF raster test for "has a figure" is meaningless (every page is a raster).
  Some pages are frames caught mid-animation (two labels printed over each other, a panel half faded
  out); transcribe them as they are, saying so, rather than reconstructing either state.
  Lecture 7's deck (a guest lecture) is the other kind: a Google Slides export with vector pages, a text
  layer, and printed slide numbers equal to the pages, so `--verify` applies and the raster test means
  something again. Lecture 8's deck (also a guest lecture) is a third kind: a PowerPoint export (Acrobat
  PDFMaker) with vector pages and pasted pictures, a text layer holding the deck's own text but none of
  any picture's, and no printed slide numbers. It is read like a vector deck and numbered like an
  image-only one. Lecture 9's deck (a guest lecture) is image-only again, but its page JPEGs are
  3524×1984 and it has no footer at all, so even within a kind the resolution and furniture vary.
  Check each new deck's producer, text layer, image size and footer before assuming any kind.
- **For an image-only deck, read the native page JPEGs, not PDF page renders.** Extract each page's embedded JPEG
  (`page.get_image_info(xrefs=True)` — not `get_images()`, which lists the shared resource dictionary,
  i.e. every image in the deck, on every page). They are ~1.2k tokens each to an agent, and they are
  the highest resolution that exists; rendering at higher DPI only upscales. Where they are much larger
  than 1280×720, give the readers ~1600px downscales and let them and the auditor crop the native files,
  which there do add detail. **For a vector deck**, render
  pages at 1280×720 for the readers, and give them each page's text layer for the spelling of printed
  prose only: the page image is the authority, and a string the layer holds but the page does not show
  is reported, not transcribed. Pictures pasted into such a deck (tables, screenshots) are not in the
  layer. The auditor renders enlarged crops from the PDF, which here do add detail.
- **Licence.** The site licenses all materials under the MIT licence and asks for the attribution
  line quoted in `LICENSE.md`. Third-party figures on the slides stay their owners'; credit them in
  `LICENSE.md` as the slide credits them.

## Transcripts

The YouTube captions are auto-generated but already punctuated, so the copy-edit is light: filler and
false starts out, terms restored against the slide file, `[Student: …]` marks for students (a turn that runs across an `[MM:SS]` mark is closed before it and
reopened after it), and
`[Ed: …]` notes where the captions are unclear or a spoken number differs from a slide (the spoken
number is kept). An `[Ed: …]` note says what is unclear; it never proposes a name or term the slides do
not support. Every change is listed in the file's header. Verify by script against `original/`:
identical `[MM:SS]` sequence, identical number inventory once `[Ed: …]` notes are removed, and every
paragraph's word ratio within 0.72–1.10 (notes and marks removed).

## Slides

Each deck is transcribed from its page JPEGs by Sonnet agents, in parallel chunks of about 36 pages,
each appending as it goes; the parent merges the parts and writes the header (front matter, numbering
note, section table). Each slide entry ends with `*Figure: yes — …*` or `*Figure: no*`. Build steps
are transcribed individually with a "Build step:" line. Code is reproduced as printed, including the
slide's own typos, with a note when the deck contradicts itself. Fill-in blanks printed as `___` pair with math
subscripts into italics on github.com: write them `\_\_\_` in any paragraph that also holds math. Figure descriptions are audited by a
separate Sonnet agent against the page JPEGs (with enlarged crops), targeting tables, charts, worked
numbers, code and every count the file states; the parent then looks at two rendered images itself. Where
the talk points at a detail of a figure (a student's answer, "notice the…"), check that the slide file
describes that detail: readers give a figure's gist and miss the detail under discussion. A list read off a picture (a word
cloud, a diagram's labels) needs the parent's own look at a crop: the reader tends to list the large
items and the auditor the small ones, and both can miss one in between. Readers and auditors both tend
to normalize slips in printed formulas and code (an unclosed parenthesis, mixed straight and curly
quotes) and report "exact", and readers also invent slips that are not on the page, so send every slip a
reader claims to the audit, tell both to keep real ones, and read the formulas and code on the
parent's two images character by character. When a printed formula looks wrong, say so on the wiki only
from the course's own material — another slide, the lecturer's reading, or arithmetic on the formula
itself — never by quoting the standard form from outside the course.

### Images

Every slide with a distinct figure is included as `raw/images/NN-<slug>/slide-N.jpg`, N the PDF page:
the deck's own page JPEG, copied byte for byte (no re-render), or for a vector deck, or an image-only deck
whose page JPEGs are wider than 1400px, a 1400px render by
`extract_slide_images.py`. Not included: logistics, logos, staff
photos, prize and stock photographs, decorative title/lab slides, slides whose content is text, code or
a table the slide file reproduces exactly, and build steps wholly contained in a later included slide.
Run `embed_slide_images.py` for the slide file. In the wiki, place images by hand in the passage that
cites the slide, one per paragraph with a one-line italic caption, and check every referenced file
exists. Images are linked relatively; the chat gets a renderable URL by reading the path.
`grep -o 'raw/images/[^)]*' wiki/NN-*.md` lists a lecture's wiki images. What was included and why goes
in `BUILD_LOG.md`.

| Lecture | Images | Deck |
| --- | --- | --- |
| 1 Introduction to Deep Learning (2026) | 34 of 108 pages | page JPEGs of `6S191_MIT_DeepLearning_L1.pdf` |
| 2 Recurrent Neural Networks, Transformers, and Attention (2026) | 33 of 83 pages | page JPEGs of `6S191_MIT_DeepLearning_L2.pdf` |
| 3 Convolutional Neural Networks (2026) | 33 of 70 pages | page JPEGs of `6S191_MIT_DeepLearning_L3.pdf` |
| 4 Deep Generative Modeling (2026) | 39 of 84 pages | page JPEGs of `6S191_MIT_DeepLearning_L4.pdf` |
| 5 Reinforcement Learning (2026) | 19 of 58 pages | page JPEGs of `6S191_MIT_DeepLearning_L5.pdf` |
| 6 Language Models and New Frontiers (2026) | 24 of 81 pages | page JPEGs of `6S191_MIT_DeepLearning_L6.pdf` |
| 7 The Three Laws of AI (2026) | 4 of 44 pages | 1400px renders of `6S191_MIT_DeepLearning_L7.pdf` |
| 8 AI for Science (2026) | 18 of 31 pages | 1400px renders of `6S191_MIT_DeepLearning_L8.pdf` |
| 9 Secrets of Massively Parallel Training (2026) | 12 of 22 pages | 1400px renders of `6S191_MIT_DeepLearning_L9.pdf` |

## Conventions

- **INDEX.md is the front door.** The chat reads it first on every conversation.
  Every wiki page must appear there with a one-line description of what it holds.
  An unindexed page is effectively invisible.
- **Relative links only** (`[gradient descent](gradient-descent.md)`). Absolute GitHub URLs break when
  the repo is renamed or forked. Decks are linked at their course-site URL, never `raw/pdfs/`.
- **Cite everything.** Claims trace back to a transcript timestamp or a slide. A name the slides print
  but the lecturer never says (a model, a paper) is attributed to the slide, not put in the lecturer's mouth.
- **Never invent course content.** If the transcript is unclear at some point,
  say so on the page. Do not fill the gap from outside knowledge — the chat
  presents these pages as authoritative material from this course.
- **Prose over fragments.** The chat quotes these pages to learners; bullet
  fragments quote badly.
- **Math in LaTeX**: `$...$` inline, `$$...$$` displayed. Renders both in
  Cairn's chat and on github.com. Never inside a code fence — that shows the
  source instead of the formula. Define each symbol on first use, and follow the
  course's own notation ($\hat{y}$, $g$, $z$, $\boldsymbol{W}^{(k)}$, $J(\boldsymbol{W})$, $\eta$)
  rather than a tidier one. Matrices use `\cr` between rows, not `\\`. A short printed label with a sub-
  or superscript that sits against a quote mark or a letter (CO₂, r²SCAN, "N³") is written in Unicode,
  because `$` there does not open math on github.com.
- **Transcripts keep notation spoken.** Captions spell notation out as speech ("dJ dW2");
  reconstructing it as LaTeX belongs in `wiki/`, not in `raw/transcripts/`.

## Rebuilding

Built and updated by the `cairn-kb` skill. To add lectures, append entries to `TODO.md` and re-run the
skill — it only does unchecked work. Write each lecture's details into `BUILD_LOG.md`, and add here only
a lesson that applies to every lecture, stated in general form.
