---
name: modular-monolith-architecture-fix-suggestions
description: Suggest fixes for modular monolith architecture violations
---

# Modular Monolith Fix Suggestions

## Purpose

Provide architectural refactoring suggestions to improve modular monolith structure.

---

# Suggested Fix Patterns

## Introduce Module Interfaces

Modules should communicate through interfaces rather than direct class access.

Example:

OrderModule → IBillingService → BillingModule

---

## Enforce Module Encapsulation

Internal module classes should not be accessed externally.

Use public module APIs instead.

---

## Remove Circular Dependencies

Introduce domain events or service interfaces to break cycles.

---

# Output

Provide:

Problem description  
Recommended refactoring  
Example architecture improvement
