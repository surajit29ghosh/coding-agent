---
name: clean-architecture-analyzer
description: Deep Roslyn AST analysis of .NET Clean Architecture compliance
---

# Roslyn Clean Architecture Analyzer

## Purpose

Perform deep AST analysis of a .NET solution to detect architecture violations.

Uses the compiler platform from :contentReference[oaicite:1]{index=1}.

---

# Inputs

solution_path

---

# Checks

## Dependency Direction

Allowed dependencies:

Domain → none  
Application → Domain  
Infrastructure → Domain + Application  
Presentation → Application  

---

## Domain Purity

Domain layer must NOT reference:

- Entity Framework
- ASP.NET
- Dapper
- HttpClient

---

## Repository Pattern

Application must define interfaces:

```
IUserRepository
IOrderRepository
```

Infrastructure must implement them.

---

## Use Case Layer

Detect classes named:

```
CreateUserHandler
RegisterCustomerUseCase
CreateOrderCommand
```

---

## Fat Controllers

Controllers must only call Application services.

Bad:

```
controller → database
```

Good:

```
controller → application service → repository
```

---

## Output

Return structured findings:

```json
{
  "dependencyViolations": [],
  "domainViolations": [],
  "missingRepositories": [],
  "fatControllers": []
}
```