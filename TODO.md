# KB build — MIT 6.S191 (Introduction to Deep Learning, 2026)

Catalog id `ba3b8a5f-6666-4376-baec-be2232de643b`. Course site: <https://introtodeeplearning.com/>.
The catalog holds 90 lectures: positions 1–9 are the 2026 offering, 10–90 earlier offerings
(2018–2025), whose decks live in the site's per-year archives (`/2025/index.html` …). The 2026
decks are `slides/6S191_MIT_DeepLearning_LN.pdf`. Lectures 1–6 are built (see BUILD_LOG.md); run 7 (lecture 7) is open below.

Images are opted in: every figure-bearing slide, rendered per Step 1c. The site licenses all
materials under the MIT license with a required attribution line (see LICENSE.md).

## Open outside any run

- [ ] Lecture 1: 9 `$$` blocks nested in list items render as inline math on github.com
  (`raw/slides/01-introduction.md` 380–400 and 587; `wiki/01-introduction.md` 327, 333, 467). Flagged
  by `verify_kb.py`'s GitHub check in run 3; move each out of its list.

## Run 7 — lecture 7 (The Three Laws of AI, 2026)

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
- [ ] Commit and push
- [ ] Move this section to BUILD_LOG.md
