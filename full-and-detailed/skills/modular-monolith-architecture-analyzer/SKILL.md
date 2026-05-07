---
name: modular-monolith-architecture-analyzer
description: Analyze repository for modular monolith architecture compliance
---

# Modular Monolith Architecture Analyzer

## Purpose

Analyze whether the system follows modular monolith architecture principles.

A modular monolith is:

- a single deployable application
- composed of well-defined modules
- each module encapsulates its domain logic

Example modules:

Orders  
Inventory  
Billing  
Users

---

# Module Rules

Modules must:

Encapsulate internal implementation.

Expose functionality through module APIs or interfaces.

Avoid direct access to internal classes of other modules.

---

# Violations to Detect

Direct access to internal classes across modules.

Example:

OrderModule accessing BillingModule internal classes.

Shared global services used by many modules.

Circular dependencies between modules.

Cross-module database access.

---

# What to Analyze

Folder structure

Project boundaries

Class dependencies

Domain models

---

# Output

Provide:

Module boundary violations  
Affected files  
Description of issue  
Recommended refactoring
