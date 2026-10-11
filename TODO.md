# KB build — MIT 6.S191 (Introduction to Deep Learning, 2026)

Catalog id `ba3b8a5f-6666-4376-baec-be2232de643b`. Course site: <https://introtodeeplearning.com/>.
The catalog holds 90 lectures: positions 1–9 are the 2026 offering, 10–90 earlier offerings
(2018–2025), whose decks live in the site's per-year archives (`/2025/index.html` …). The 2026
decks are `slides/6S191_MIT_DeepLearning_LN.pdf`. Scope of this build: lecture 1 only.

Images are opted in: every figure-bearing slide, rendered per Step 1c. The site licenses all
materials under the MIT license with a required attribution line (see LICENSE.md).

## Transcripts
- [x] 01 Introduction to Deep Learning — video II4giR4vOOo (auto-captions, already punctuated; light Sonnet copy-edit, verbatim in original/)

## Crawl
- [x] Fetch course site index: https://introtodeeplearning.com/ (2026 index only; year archives deferred)
- [x] Download linked PDFs and slides (gitignored; 9 decks + the AAAI lab paper)
- [x] Write sources.md

## Slides (raw/slides/)
- [x] 01 Introduction — 6S191_MIT_DeepLearning_L1.pdf (108 pages, no text layer, no printed numbers: slide N = page N; three Sonnet agents in parallel; Sonnet audit of 14 pages, 0 discrepancies)

## Wiki
- [x] wiki/01-introduction.md
- [x] Topic pages (cross-lecture concepts) — what-is-deep-learning, perceptron, activation-functions, neural-network-layers, loss-functions, gradient-descent, backpropagation, regularization (lecture 1 only; extend as lectures land)
- [x] INDEX.md table of contents

## Images
- [x] raw/images/01-introduction/ — 34 native page JPEGs extracted byte-for-byte; embedded in the wiki and slide files
- [x] INDEX.md — the chat's image rules; AGENTS.md — the Images conventions and table row; BUILD_LOG.md — what was rendered and why; LICENSE.md — attribution

## Publish
- [x] kb.json — coverage, materials.method, provenance caveats
- [x] BUILD_LOG.md — lecture 1 record: notices, audit findings, printed slips, transcript edits
- [x] SEE_ALSO.md — MIT 6.7960 and MIT 15.773
- [x] verify_kb.py clean, and its review section read
- [x] Commit and push
- [ ] PATCH kbUrl onto the catalog entry
