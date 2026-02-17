---
name: agent-data-sources
type: awesome-list
domain: ai-agent-infrastructure
format: markdown
maintained_by: chrbailey
repo: https://github.com/chrbailey/agent-data-sources
---

# Agent Data Sources

A curated list of structured, machine-readable data feeds designed for ingestion by AI agents, monitoring systems, and research pipelines.

Every entry has been verified to return a parseable feed. No paywalled APIs. No feeds that require authentication to read. If a feed goes dead, open an issue.

## Contents

- [AI Trend Intelligence](#ai-trend-intelligence)
- [AI Research](#ai-research)
- [Developer News](#developer-news)
- [AI Expert Commentary](#ai-expert-commentary)
- [Code & Repos](#code--repos)
- [First-Party AI Labs](#first-party-ai-labs)
- [Standards & Specs](#standards--specs)
- [Contributing](#contributing)

---

## AI Trend Intelligence

| Name | Format | Frequency | Description |
|------|--------|-----------|-------------|
| **[deeptrend](https://github.com/chrbailey/deeptrend)** | JSON Feed, RSS, llms.txt | Every 6 hours | Structured AI trend intelligence synthesized from 14+ sources via LLM Counsel. Publishes JSON Feed, RSS, hot.json, and llms.txt. [Live feed](https://chrbailey.github.io/deeptrend/feed.json) &#124; [Hot topics](https://chrbailey.github.io/deeptrend/hot.json) &#124; [RSS](https://chrbailey.github.io/deeptrend/feed.xml) &#124; [llms.txt](https://chrbailey.github.io/deeptrend/llms.txt) |

```bash
# Quick test
curl -s https://chrbailey.github.io/deeptrend/hot.json | jq '.topics[:3]'
```

## AI Research

| Name | Format | Frequency | Description |
|------|--------|-----------|-------------|
| **[arXiv cs.AI](https://arxiv.org/list/cs.AI/recent)** | RSS | Daily | New papers in Artificial Intelligence. Feed: `https://export.arxiv.org/rss/cs.AI` |
| **[arXiv cs.CL](https://arxiv.org/list/cs.CL/recent)** | RSS | Daily | New papers in Computation and Language (NLP/LLMs). Feed: `https://export.arxiv.org/rss/cs.CL` |
| **[arXiv cs.LG](https://arxiv.org/list/cs.LG/recent)** | RSS | Daily | New papers in Machine Learning. Feed: `https://export.arxiv.org/rss/cs.LG` |
| **[HuggingFace Daily Papers](https://huggingface.co/papers)** | Web (HTML) | Daily | Community-upvoted research papers with discussion threads. Scrape or use [HF API](https://huggingface.co/api/daily_papers). |
| **[HuggingFace Blog](https://huggingface.co/blog)** | RSS | Weekly | Technical posts on models, datasets, and tooling. Feed: `https://huggingface.co/blog/feed.xml` |
| **[Semantic Scholar API](https://api.semanticscholar.org/)** | JSON API | Real-time | Academic paper search with citation graphs, abstracts, and influence scores. Free tier: 100 req/5min. [Docs](https://api.semanticscholar.org/api-docs/) |

```bash
# arXiv — latest AI papers
curl -s "https://export.arxiv.org/rss/cs.AI" | head -50

# Semantic Scholar — search for recent transformer papers
curl -s "https://api.semanticscholar.org/graph/v1/paper/search?query=transformer+architecture&limit=5&fields=title,year,citationCount" | jq .
```

## Developer News

| Name | Format | Frequency | Description |
|------|--------|-----------|-------------|
| **[Hacker News — Front Page](https://news.ycombinator.com/)** | RSS | ~1 min | Top-ranked stories from HN front page. Feed: `https://hnrss.org/frontpage` |
| **[Hacker News — Newest](https://news.ycombinator.com/newest)** | RSS | ~1 min | All new HN submissions chronologically. Feed: `https://hnrss.org/newest` |
| **[Hacker News — Best Comments](https://news.ycombinator.com/bestcomments)** | RSS | ~1 min | Highest-rated HN comments. Feed: `https://hnrss.org/bestcomments` |
| **[TechMeme](https://www.techmeme.com/)** | RSS | ~15 min | Algorithmically curated top tech news with source clustering. Feed: `https://www.techmeme.com/feed.xml` |
| **[Lobsters](https://lobste.rs/)** | RSS | ~5 min | Invite-only tech link aggregator, strong signal-to-noise. Feed: `https://lobste.rs/rss` |

```bash
# HN front page — titles and links
curl -s "https://hnrss.org/frontpage" | grep -oP '(?<=<title>).*?(?=</title>)' | head -10

# TechMeme — current headlines
curl -s "https://www.techmeme.com/feed.xml" | grep -oP '(?<=<title>).*?(?=</title>)' | head -10
```

> **Tip:** hnrss.org supports query parameters for filtering: `https://hnrss.org/frontpage?q=LLM` returns only stories matching "LLM". See [hnrss.org](https://hnrss.org/) for full docs.

## AI Expert Commentary

| Name | Format | Frequency | Description |
|------|--------|-----------|-------------|
| **[Simon Willison's Weblog](https://simonwillison.net/)** | Atom | Daily | Prolific commentary on LLMs, developer tools, and AI policy from the Datasette creator. Feed: `https://simonwillison.net/atom/everything/` |
| **[Import AI](https://jack-clark.net/)** | RSS | Weekly | Weekly newsletter on AI policy, research, and capabilities by Jack Clark (Anthropic co-founder). Feed: `https://jack-clark.net/feed/` |
| **[AlphaSignal](https://alphasignal.ai/)** | RSS (Substack) | Weekly | Curated AI research and engineering newsletter. Feed: `https://alphasignal.substack.com/feed` |
| **[Last Week in AI](https://lastweekin.ai/)** | RSS | Weekly | Comprehensive weekly roundup of AI news, research, and industry developments. Feed: `https://lastweekin.ai/feed` |
| **[Machine Learning (Substack)](https://machinelearning.substack.com/)** | RSS | 2-3x/week | ML research highlights and analysis. Feed: `https://machinelearning.substack.com/feed` |

```bash
# Simon Willison — latest posts
curl -s "https://simonwillison.net/atom/everything/" | grep -oP '(?<=<title>).*?(?=</title>)' | head -5
```

> **Tip:** Most Substack newsletters expose an RSS feed at `https://<name>.substack.com/feed`. If you follow an AI author on Substack, try that pattern.

## Code & Repos

| Name | Format | Frequency | Description |
|------|--------|-----------|-------------|
| **[GitHub Trending](https://github.com/trending)** | Web (HTML) | Daily | Top trending repositories by language and time range. No official RSS — use the [GitHub Trending API](https://api.gitterapp.com/repositories) or scrape. |
| **[GitHub Events API](https://docs.github.com/en/rest/activity/events)** | JSON API | Real-time | Public events stream (pushes, stars, forks, issues). Free tier: 60 req/hr unauthenticated, 5000/hr with token. |
| **[GitLab Explore](https://gitlab.com/explore)** | Web (HTML) | Continuous | Trending and most-starred public GitLab projects. |

```bash
# GitHub — public events for a repo
curl -s "https://api.github.com/repos/anthropics/claude-code/events" | jq '.[0] | {type, created_at, actor: .actor.login}'

# GitHub Trending — unofficial API
curl -s "https://api.gitterapp.com/repositories?since=daily" | jq '.[0] | {name: .fullName, stars: .stars, description}'
```

## First-Party AI Labs

| Name | Format | Frequency | Description |
|------|--------|-----------|-------------|
| **[Google Research Blog](https://research.google/blog/)** | RSS | 1-2x/week | Research announcements from Google Research. Feed: `https://research.google/blog/rss/` |
| **[Google DeepMind Blog](https://deepmind.google/blog/)** | RSS | 1-2x/week | Research updates from DeepMind (Gemini, AlphaFold, etc). Feed: `https://deepmind.google/blog/rss.xml` |
| **[BAIR Blog](https://bair.berkeley.edu/blog/)** | RSS | 1-2x/month | Berkeley AI Research lab posts on robotics, NLP, vision, and RL. Feed: `https://bair.berkeley.edu/blog/feed.xml` |
| **[HuggingFace Blog](https://huggingface.co/blog)** | RSS | Weekly | Open-source model releases, training guides, and tooling updates. Feed: `https://huggingface.co/blog/feed.xml` |

```bash
# Google Research — latest blog posts
curl -s "https://research.google/blog/rss/" | grep -oP '(?<=<title>).*?(?=</title>)' | head -5

# BAIR — latest posts
curl -s "https://bair.berkeley.edu/blog/feed.xml" | grep -oP '(?<=<title>).*?(?=</title>)' | head -5
```

> **Note on OpenAI and Anthropic:** As of February 2026, neither OpenAI nor Anthropic publishes a public RSS feed for their blogs. For monitoring these, use a web-to-RSS bridge like [Feedless](https://feedless.org/) or check community-maintained feeds.

## Standards & Specs

These define the formats used by the feeds above. Useful for building parsers and validators.

| Name | URL | Description |
|------|-----|-------------|
| **[JSON Feed 1.1](https://www.jsonfeed.org/version/1.1/)** | `https://www.jsonfeed.org/version/1.1/` | Feed format using JSON instead of XML. Easier to parse programmatically. |
| **[RSS 2.0 Specification](https://www.rssboard.org/rss-specification)** | `https://www.rssboard.org/rss-specification` | The dominant feed syndication format. XML-based. |
| **[Atom 1.0 (RFC 4287)](https://www.rfc-editor.org/rfc/rfc4287)** | `https://www.rfc-editor.org/rfc/rfc4287` | IETF standard for web feeds. More rigorous than RSS. |
| **[llms.txt Specification](https://llmstxt.org/)** | `https://llmstxt.org/` | Proposed standard for providing LLM-readable site information, similar to robots.txt. |

---

## Contributing

Found a feed that belongs here? Open a PR. Requirements:

1. **Machine-readable** — must return structured data (RSS, Atom, JSON Feed, or JSON API), not just HTML
2. **Publicly accessible** — no API keys required to read (free-tier APIs with generous limits are OK)
3. **Actively maintained** — feed must have published content within the last 90 days
4. **Relevant to AI/ML practitioners** — research, tooling, industry news, or infrastructure

Please include: name, URL, format, update frequency, and a one-line description.

---

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, the author has waived all copyright and related rights to this work.
