---
name: monolith-architecture-score
description: Compute architectural quality score for monolithic applications
---

# Monolith Architecture Score

## Purpose

Evaluate the structural quality of the monolithic system.

Score range:

0 – 100

---

# Scoring Criteria

Code organization: 25

Evaluate project structure and folder organization.

---

Separation of concerns: 25

Business logic should not exist in controllers or repositories.

---

Coupling: 25

Evaluate dependencies between modules.

Low coupling improves maintainability.

---

Class complexity: 25

Evaluate large classes and methods.

Detect god classes and excessive class responsibilities.

---

# Score Calculation

Architecture Score =

Code Organization  
+ Separation of Concerns  
+ Coupling  
+ Class Complexity

Maximum Score: 100

---

# Output

Architecture Score: X / 100

Strengths

List architectural strengths.

Weaknesses

List architectural weaknesses.

Architecture Risk Level

Low  
Moderate  
High
