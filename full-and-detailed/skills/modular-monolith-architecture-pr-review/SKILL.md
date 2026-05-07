---
name: modular-monolith-architecture-pr-review
description: Review pull requests for modular monolith architecture violations
---

# Modular Monolith PR Review

## Purpose

Review pull requests for violations of module boundaries.

---

# Review Areas

Module boundaries.

Internal class access across modules.

Module dependencies.

Domain separation.

---

# Violations to Detect

Cross-module direct class usage.

Example:

OrderModule directly accessing BillingModule internal classes.

Shared global services that bypass module boundaries.

Circular dependencies between modules.

---

# Output

Provide PR comment including:

Violation summary  
Affected modules  
Recommended improvements
