---
name: monolith-architecture-fix-suggestions
description: Provide refactoring suggestions to improve monolithic architecture
---

# Monolith Architecture Fix Suggestions

## Purpose

Suggest architectural improvements for violations detected in a monolithic application.

---

# Suggested Fix Patterns

## Move Business Logic to Services

Incorrect:

Controller contains business logic.

Correct:

Controller → Service → Repository

---

## Refactor God Classes

Large classes should be split into smaller focused classes.

Example:

OrderManager → OrderService + OrderValidator + OrderCalculator

---

## Introduce Layer Separation

Ensure the following layers exist:

Presentation  
Application/Service  
Data Access  

Each layer should have clear responsibilities.

---

# Output

Provide:

Problem description  
Recommended refactoring  
Improved code structure
