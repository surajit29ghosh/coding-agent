---
name: monolith-architecture-pr-review
description: Review pull requests for violations of monolithic architecture best practices
---

# Monolith Architecture PR Review

## Purpose

Review pull request changes and identify architectural violations in a monolithic system.

Focus on maintainability and separation of concerns.

---

# Review Areas

Controllers

Controllers should only orchestrate requests and call services.

Controllers must not contain business logic.

---

Services

Services should encapsulate business rules.

Detect services that depend directly on controllers or UI frameworks.

---

Repositories

Repositories should only handle data persistence.

Business logic must not be implemented inside repositories.

---

# Violations to Detect

Business logic added to controllers.

Direct database calls from controllers.

Large classes added in PR changes.

Cross-module dependencies introduced.

---

# Output

Provide PR comments including:

Summary of architecture violations  
File paths affected  
Recommended improvements
