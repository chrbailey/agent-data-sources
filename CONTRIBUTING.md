# Contributing

Thanks for looking.

## Before opening a PR

1. **Open an issue first** for anything larger than a typo.
2. **Verify the feed works.** Hit the URL with `curl` and confirm it returns parseable content. Include the command and output in the PR.
3. **Match the existing table format.** Name, format, frequency, description — keep the columns consistent.
4. **Include a working example.** Show a `curl` command or snippet that extracts useful data.

## What this project will not accept

This is a curated list. Quality matters more than breadth. The README makes explicit promises: every entry is verified, no paywalled APIs, no feeds requiring auth. Changes that violate those promises will be declined.

- Feeds that require an API key, OAuth, or any form of authentication to read.
- Feeds behind a paywall or subscription.
- Feeds with unclear or hostile terms-of-service for machine access.
- Feeds that are promoted but not verified to return parseable content — if the PR does not show `curl` output, it is not reviewable.
- PRs that reorganize sections without an issue discussion first.
- Link farms or SEO content disguised as data feeds.

## Reporting security issues

See [SECURITY.md](SECURITY.md). Do not file security issues in the public tracker.

## Author

[Christopher Bailey](https://github.com/chrbailey).
