# KB build — MIT 6.S191 (Introduction to Deep Learning, 2026)

Catalog id `ba3b8a5f-6666-4376-baec-be2232de643b`. Course site: <https://introtodeeplearning.com/>.
The catalog holds 90 lectures: positions 1–9 are the 2026 offering, 10–90 earlier offerings
(2018–2025), whose decks live in the site's per-year archives (`/2025/index.html` …). The 2026
decks are `slides/6S191_MIT_DeepLearning_LN.pdf`. Lectures 1–7 are built (see BUILD_LOG.md). No run is open: to add a lecture, append its
checklist here.

Images are opted in: every figure-bearing slide, rendered per Step 1c. The site licenses all
materials under the MIT license with a required attribution line (see LICENSE.md).

## Open outside any run

- [ ] Lecture 1: 9 `$$` blocks nested in list items render as inline math on github.com
  (`raw/slides/01-introduction.md` 380–400 and 587; `wiki/01-introduction.md` 327, 333, 467). Flagged
  by `verify_kb.py`'s GitHub check in run 3; move each out of its list.

## Run 8 — lecture 8 (AI for Science, 2026)

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
- [ ] Commit and push
- [ ] Move this section to BUILD_LOG.md
