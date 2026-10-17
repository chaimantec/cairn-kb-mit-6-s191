# KB build — MIT 6.S191 (Introduction to Deep Learning, 2026)

Catalog id `ba3b8a5f-6666-4376-baec-be2232de643b`. Course site: <https://introtodeeplearning.com/>.
The catalog holds 90 lectures: positions 1–9 are the 2026 offering, 10–90 earlier offerings
(2018–2025), whose decks live in the site's per-year archives (`/2025/index.html` …). The 2026
decks are `slides/6S191_MIT_DeepLearning_LN.pdf`. Lectures 1–5 are built (see BUILD_LOG.md); run 6 is open below.

Images are opted in: every figure-bearing slide, rendered per Step 1c. The site licenses all
materials under the MIT license with a required attribution line (see LICENSE.md).

## Open outside any run

- [ ] Lecture 1: 9 `$$` blocks nested in list items render as inline math on github.com
  (`raw/slides/01-introduction.md` 380–400 and 587; `wiki/01-introduction.md` 327, 333, 467). Flagged
  by `verify_kb.py`'s GitHub check in run 3; move each out of its list.

## Run 6 — lecture 6 (Language Models and New Frontiers, 2026)

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
- [ ] Commit and push
- [ ] Move this section to BUILD_LOG.md
