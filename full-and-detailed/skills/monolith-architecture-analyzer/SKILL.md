---
name: monolith-architecture-analyzer
description: Analyze repository for monolithic architecture structure and maintainability issues
---

# Monolith Architecture Analyzer

## Purpose

Analyze whether the system follows a maintainable monolithic architecture.

A monolith is typically:

- a single deployable application
- a shared codebase
- a shared database
- internally structured into logical layers

Even monoliths must maintain clear separation of concerns.

---

# What to Analyze

Analyze the repository for:

Project structure  
Folder organization  
Dependency relationships  
Class sizes  
Module boundaries

---

# Best Practices for Monolith Architecture

A well-designed monolith should have internal separation such as:

Presentation Layer  
Business Logic Layer  
Data Access Layer  

Business logic should reside in services or domain models.

Controllers should remain thin.

---

# Violations to Detect

Controllers containing business logic.

Example:

Controller → Business Logic → Database access

God classes (very large classes handling many responsibilities).

Large controllers containing hundreds of lines of logic.

Tightly coupled modules with many cross-dependencies.

Business logic implemented inside repository classes.

Unstructured folder organization.

---

# Output

Provide the following:

Violation summary  
File path  
Class name  
Description of the issue  

Example output:

File: OrderController.cs  
Issue: Business logic implemented inside controller  
Recommendation: Move logic to OrderService
