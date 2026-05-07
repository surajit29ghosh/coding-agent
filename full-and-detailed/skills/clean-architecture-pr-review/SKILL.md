---
name: clean-architecture-pr-review
description: Adds architecture review comments to pull requests
---

# PR Architecture Reviewer

Posts review comments on pull requests.

Works with repositories hosted on :contentReference[oaicite:2]{index=2}.

---

# Example PR Comment

## Architecture Review

Score: 74/100

Issues detected:

- Domain references EF Core
- Controller contains business logic

Suggestions:

- Move persistence to Infrastructure
- Introduce IUserRepository abstraction
