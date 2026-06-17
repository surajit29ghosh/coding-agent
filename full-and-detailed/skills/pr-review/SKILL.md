---
name: pr-review
description: Add NFR review comments to pull requests
---

# NFR Pull Request Review

Example comment:

NFR Score: 81/100

Issues detected:

- SQL injection risk
- Large object allocations
- Blocking async calls

Recommendations:

- Use parameterized queries
- Reduce large allocations
- Replace Result with await
