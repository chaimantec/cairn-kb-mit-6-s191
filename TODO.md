# KB build — MIT 6.S191 (Introduction to Deep Learning, 2026)

Catalog id `ba3b8a5f-6666-4376-baec-be2232de643b`. Course site: <https://introtodeeplearning.com/>.
The catalog holds 90 lectures: positions 1–9 are the 2026 offering, 10–90 earlier offerings
(2018–2025), whose decks live in the site's per-year archives (`/2025/index.html` …). The 2026
decks are `slides/6S191_MIT_DeepLearning_LN.pdf`. Lectures 1–4 are built (see BUILD_LOG.md); run 5 (lecture 5) is open below.

Images are opted in: every figure-bearing slide, rendered per Step 1c. The site licenses all
materials under the MIT license with a required attribution line (see LICENSE.md).

## Open outside any run

- [ ] Lecture 1: 9 `$$` blocks nested in list items render as inline math on github.com
  (`raw/slides/01-introduction.md` 380–400 and 587; `wiki/01-introduction.md` 327, 333, 467). Flagged
  by `verify_kb.py`'s GitHub check in run 3; move each out of its list.

## Run 5 — lecture 5 (Reinforcement Learning, 2026)

Catalog position 5, video 1ij3dweHu-0 (59:19). Deck `slides/6S191_MIT_DeepLearning_L5.pdf`: 58 pages,
each one 1280×720 JPEG (DCTDecode), no text layer (macOS Quartz PDFContext, created 2026-01-07), footer
"1/7/26" with no slide number (checked on a strip of 10 footers; 50 is a blue page, 58 black): slide N = page N.

- [x] Verbatim captions → raw/transcripts/original/05-reinforcement-learning.md (77 marks)
- [x] raw/slides/05-reinforcement-learning.md — two Sonnet readers (1–29, 30–58), merged, header (47 figure slides)
- [x] Figure audit (Sonnet) of chart-, equation-, code- and diagram-heavy pages; parent checks two images (22 pages; fixes on 32, 33, 37, 38, 40, 48, plus 42 detail; parent: images of 33 and 46, crop of 33)
- [x] raw/transcripts/05-reinforcement-learning.md — Sonnet copy-edit; marks, numbers, ratios checked (77/77, identical, 0.90–1.00)
- [x] raw/images/05-reinforcement-learning/ — native page JPEGs of figure slides, embedded (19 of 58, 1.1 MB)
- [x] wiki/05-reinforcement-learning.md
- [x] Topic pages, new and extended (new: reinforcement-learning, q-learning, policy-gradients; extended: what-is-deep-learning, loss-functions, gradient-descent, computer-vision, convolutional-neural-networks, autoencoders-and-vaes; lecture 3 page)
- [x] INDEX.md, AGENTS.md image table, LICENSE.md, sources.md, kb.json, BUILD_LOG.md (sources.md already listed the deck)
- [x] verify_kb.py clean, and its review section read
- [ ] Commit and push
- [ ] Move this section to BUILD_LOG.md
