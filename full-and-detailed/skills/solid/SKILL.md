---
name: solid
description: Comprehensive SOLID design skill: analyze, score, suggest fixes, and add PR review comments for SOLID principles in .NET codebases.
---

# SOLID Skill

This skill bundles SOLID analysis, scoring, automated refactor suggestions, and pull-request review comments for .NET projects.

## Components

- `Analyzer`: Detects violations of SRP, OCP, LSP, ISP, and DIP using syntax trees and code structure.
- `Scorer`: Computes a SOLID score (out of 100) across the five principles.
- `Fix Suggestions`: Produces targeted refactor suggestions and example transformations.
- `PR Review`: Posts concise SOLID review comments on pull requests with findings and recommendations.

## Inputs

- `solution_path` — path to the .sln or project folder to analyze.
- `solid_findings` — structured findings from the analyzer (when running scoring/fixes).

## Outputs

- `solid_findings.json` — analyzer findings.
- `solid_refactor_suggestions.md` — human-readable refactor suggestions.
- PR review comments via repository integration.

## Usage

1. Run the `Analyzer` against `solution_path` to produce `solid_findings.json`.
2. Run the `Scorer` to compute overall SOLID score and breakdown per principle.
3. Generate `Fix Suggestions` from `solid_findings.json` to get refactor examples.
4. Optionally run `PR Review` to post comments and a summary score on pull requests.

## Principles & Examples

### Single Responsibility Principle (SRP)
- Detects classes with mixed responsibilities or excessive methods.

Example violation:

```csharp
class UserService { void CreateUser() {} void SaveToDatabase() {} void SendEmail() {} }
```

### Open Closed Principle (OCP)
- Detects large conditional blocks or switches that should use polymorphism.

### Liskov Substitution Principle (LSP)
- Detects subclasses that break base-class contracts (e.g., methods that throw unexpectedly).

### Interface Segregation Principle (ISP)
- Detects fat interfaces used by multiple clients; suggests splitting interfaces.

### Dependency Inversion Principle (DIP)
- Detects concrete dependencies in high-level modules; suggests introducing abstractions and DI.

## Scoring

Score is out of 100 (20 points per principle). Interpretation:

- 90–100: Excellent
- 70–89: Good
- 50–69: Needs improvement
- <50: Poor

## PR Review Example

SOLID Review Summary

Score: 72/100

Issues detected:
- `UserManager` violates SRP
- `PaymentService` violates OCP
- `OrderService` tightly coupled to SQL repository

Recommendations:
- Split responsibilities, introduce strategy pattern, and add repository abstractions.
