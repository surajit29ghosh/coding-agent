---
name: component-architecture-pr-review
description: Review PR changes for component architecture violations
---

# Component Architecture PR Review

## Purpose

Review pull request changes for violations of component boundaries.

---

# Review Areas

Component encapsulation

Internal classes should not be accessed by other components.

---

Component dependencies

Components should communicate through APIs or interfaces.

---

Circular dependencies

Avoid component dependency cycles.

---

# Output

Provide PR comment including:

Violation summary  
Affected components  
Suggested improvements
