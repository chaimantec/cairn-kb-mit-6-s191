# KB build — MIT 6.S191 (Introduction to Deep Learning, 2026)

Catalog id `ba3b8a5f-6666-4376-baec-be2232de643b`. Course site: <https://introtodeeplearning.com/>.
The catalog holds 90 lectures: positions 1–9 are the 2026 offering, 10–90 earlier offerings
(2018–2025), whose decks live in the site's per-year archives (`/2025/index.html` …). The 2026
decks are `slides/6S191_MIT_DeepLearning_LN.pdf`. Lectures 1–8 are built (see BUILD_LOG.md); run 9 (lecture 9) is open below.

Images are opted in: every figure-bearing slide, rendered per Step 1c. The site licenses all
materials under the MIT license with a required attribution line (see LICENSE.md).

## Open outside any run

- [ ] Lecture 1: 9 `$$` blocks nested in list items render as inline math on github.com
  (`raw/slides/01-introduction.md` 380–400 and 587; `wiki/01-introduction.md` 327, 333, 467). Flagged
  by `verify_kb.py`'s GitHub check in run 3; move each out of its list.

## Run 9 — lecture 9 (Secrets of Massively Parallel Training, 2026)

Catalog position 9, video UZZD9d9YqnQ (52:40), a guest lecture by Mathias Lechner (co-founder and CTO, Liquid
AI). Deck `slides/6S191_MIT_DeepLearning_L9.pdf`: 22 pages, image-only (no producer; PDF title "slides_only"),
each page one 3524×1984 JPEG with no text layer — the same kind as decks 1–6 but at 2.75× their resolution.
Slide N = PDF page N, check headings with a plain 1..N sequence check. Readers get 1600px downscales of the
page JPEGs; the auditor crops the native JPEGs; images are 1400px downscales (the native files average 316 KB).

- [x] Verbatim captions → raw/transcripts/original/09-massively-parallel-training.md (69 marks)
- [x] raw/slides/09-massively-parallel-training.md — Sonnet reader (1–22), merged, header (19 figure slides; 1–22 sequence checked)
- [x] Figure audit (Sonnet) of figure, chart and table pages; parent checks two images (slides 1–22; fixes on 3, 7, 11, 14, 17, 18, 19, 22; parent images below)
- [x] raw/transcripts/09-massively-parallel-training.md — Sonnet copy-edit; marks, numbers, ratios checked (69/69, five recorded removals, 0.80–1.00; 8 [Ed] notes)
- [x] raw/images/09-massively-parallel-training/ — figure slides, embedded (12 of 22, 1.13 MB: 5, 7–9, 11, 13–19; slide file by script, wiki by hand)
- [x] wiki/09-massively-parallel-training.md
- [x] Topic pages, new and extended (new: distributed-training; extended: large-language-models, attention-and-transformers, gradient-descent, backpropagation, what-is-deep-learning; lecture 6 links to lecture 9)
- [x] INDEX.md, AGENTS.md (deck-format bullet, image table), LICENSE.md, sources.md, kb.json, BUILD_LOG.md (sources.md already listed the deck; INDEX now covers the whole 2026 edition)
- [x] verify_kb.py clean, and its review section read (check_math --github: 0 errors; the 9 warnings are lecture 1's open item; 12 notation warnings in the new pages fixed)
- [ ] Commit and push
- [ ] Move this section to BUILD_LOG.md
