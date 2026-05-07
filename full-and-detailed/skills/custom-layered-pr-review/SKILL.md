---
name: custom-layered-pr-review
description: Review pull requests for custom layered architecture violations
---

# Custom Layered Architecture PR Review

## Purpose

Review pull request changes for violations in:

Plugin → Processor → ApiClient → Helper architecture

---

# Review Areas

## Plugin

Ensure:

- no business logic
- only invokes Processor

---

## Processor

Ensure:

- orchestrates flow correctly
- uses Wrapper for DB
- does not call Helper directly

---

## ApiClient

Ensure:

- maps objects properly
- does not call DB
- does not skip Helper

---

## Helper

Ensure:

- only prepares and sends HTTP requests
- no business logic

---

## Domain

Ensure:

- contains only entities
- no infrastructure dependencies

---

# Violations to Detect

- Layer skipping
- Improper dependency usage
- Business logic leakage
- Incorrect data flow

---

# Output

Provide PR comments:

Summary of violations  
Affected files  
Suggested refactoring
