---
name: component-architecture-analyzer
description: Analyze component-based architecture boundaries
---

# Component Architecture Analyzer

## Purpose

Evaluate whether the system is structured into independent components.

Examples:

Orders  
Users  
Billing  
Inventory  

Each component should contain:

API  
Domain Logic  
Data Access

---

# Violations to Detect

Cross-component internal class access.

Shared implementation across components.

Circular dependencies between components.

Large "god components".

---

# Output

Provide:

Component boundary violations  
File paths  
Description  
Recommended improvements
