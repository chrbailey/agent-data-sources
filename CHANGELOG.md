# Changelog

All notable changes to this curated list.

Format loosely follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). For a curated list, "release" means "a new verification pass where every entry was checked to still return a parseable feed."

## [Unreleased]

### Added
- `CHANGELOG.md` (this file).
- "Last verified" banner and re-verification cadence (90 days) in `README.md`.

### Changed
- Verification pass 2026-04-16. Sampled 16 feeds spanning arXiv, HN/TechMeme/Lobsters, Simon Willison, Import AI, AlphaSignal, Last Week in AI, Google Research, BAIR, DeepMind, HuggingFace blog + daily_papers, Semantic Scholar, and GitHub Events. 15/16 returned 200; Semantic Scholar rate-limited (429) but endpoint is live.

### Removed
- **`api.gitterapp.com`** (Code & Repos section) — the host no longer resolves. It was cited as an unofficial GitHub Trending JSON API. Replaced with a scrape-based example and a note that hosted third-party trending APIs in this space are historically unreliable.

## 2026-02-17 — Initial publication

- Seven sections published: AI Trend Intelligence, AI Research, Developer News, AI Expert Commentary, Code & Repos, First-Party AI Labs, Standards & Specs.
- 30+ feeds total. All verified 200 at publication.
- License: CC0.
