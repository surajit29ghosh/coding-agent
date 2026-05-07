---
name: component-architecture-fix-suggestions
description: Suggest fixes for component architecture violations
---

# Component Architecture Fix Suggestions

## Introduce Component Interfaces

Components should communicate through interfaces.

Example:

OrderComponent → IBillingService → BillingComponent

---

## Encapsulate Component Logic

Internal classes should remain private to the component.

Expose only APIs.

---

## Remove Circular Dependencies

Introduce shared contracts or messaging patterns.
