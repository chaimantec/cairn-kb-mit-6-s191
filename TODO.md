# KB build — MIT 6.S191 (Introduction to Deep Learning, 2026)

Catalog id `ba3b8a5f-6666-4376-baec-be2232de643b`. Course site: <https://introtodeeplearning.com/>.
The catalog holds 90 lectures: positions 1–9 are the 2026 offering, 10–90 earlier offerings
(2018–2025), whose decks live in the site's per-year archives (`/2025/index.html` …). The 2026
decks are `slides/6S191_MIT_DeepLearning_LN.pdf`. Lectures 1 and 2 are built (see BUILD_LOG.md); run 3 below is open. To add a lecture, append its
checklist here.

Images are opted in: every figure-bearing slide, rendered per Step 1c. The site licenses all
materials under the MIT license with a required attribution line (see LICENSE.md).

## Open outside any run

- [ ] Lecture 1: 9 `$$` blocks nested in list items render as inline math on github.com
  (`raw/slides/01-introduction.md` 380–400 and 587; `wiki/01-introduction.md` 327, 333, 467). Flagged
  by `verify_kb.py`'s GitHub check in run 3; move each out of its list.

## Run 3 — lecture 3 (Convolutional Neural Networks, 2026)

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
- [ ] Commit and push
- [ ] Move this section to BUILD_LOG.md
