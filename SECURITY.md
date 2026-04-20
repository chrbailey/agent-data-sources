# Security

## Responsible Disclosure

If you find a security issue, please do **not** file a public GitHub issue.

Email: chris.bailey@erp-access.com — include "SECURITY: agent-data-sources" in the subject line.

Expect an acknowledgment within 72 hours.

## What this tool does

This repository is a curated markdown directory of structured, machine-readable data feeds. It is documentation only. It does not ship code, execute anything, or make network calls.

## What this tool does NOT do

- It does not include or endorse feeds that require authentication.
- It does not include feeds from sources it has not verified.
- It does not collect analytics about who reads the list.
- It does not host or proxy any of the listed feeds — consumers hit the upstream sources directly.
- It does not vouch for the security or content of third-party feeds beyond verifying that they return parseable data.

## Known Considerations

- Consumers of feeds in this list are ultimately hitting third-party services. Treat responses as untrusted input — parse defensively, validate schemas, handle rate limits, respect robots.txt.
- A feed verified today may change its terms tomorrow. If you operate an agent that pulls from this list, cache upstream terms and monitor for changes.
- Some feeds go through aggregators (e.g., rss2json.com, hnrss.org). If those intermediaries are compromised, feed contents could be manipulated. Consider validating against a second source for anything consequential.
- If an entry here goes dead or changes its access model (e.g., adds auth), open an issue — the list makes promises about accessibility and we honor them.

If you see evidence of any of the "does NOT do" items, that is a security issue — please report.
