# KB build — MIT 6.S191 (Introduction to Deep Learning, 2026)

Catalog id `ba3b8a5f-6666-4376-baec-be2232de643b`. Course site: <https://introtodeeplearning.com/>.
The catalog holds 90 lectures: positions 1–9 are the 2026 offering, 10–90 earlier offerings
(2018–2025), whose decks live in the site's per-year archives (`/2025/index.html` …). The 2026
decks are `slides/6S191_MIT_DeepLearning_LN.pdf`. Lectures 1–3 are built (see BUILD_LOG.md). Run 4 (lecture 4) is open below.

Images are opted in: every figure-bearing slide, rendered per Step 1c. The site licenses all
materials under the MIT license with a required attribution line (see LICENSE.md).

## Open outside any run

- [ ] Lecture 1: 9 `$$` blocks nested in list items render as inline math on github.com
  (`raw/slides/01-introduction.md` 380–400 and 587; `wiki/01-introduction.md` 327, 333, 467). Flagged
  by `verify_kb.py`'s GitHub check in run 3; move each out of its list.

## Run 4 — lecture 4 (Deep Generative Modeling, 2026)

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
- [ ] Commit and push
- [ ] Move this section to BUILD_LOG.md
