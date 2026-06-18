---
name: solid-principles-check
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

## Extended Inputs
- `repository_root` — top-level folder for repository-wide analysis (optional).
- `analysis_profile` — configuration profile (quick, full, staged) controlling depth and heuristics.

## Outputs

- `solid_findings.json` — analyzer findings.
- `solid_refactor_suggestions.md` — human-readable refactor suggestions.
- PR review comments via repository integration.

## Extended Outputs
- `solid_health_report.json` — aggregated health metrics and per-module scores.
- `solid_action_plan.md` — prioritized remediation tasks and estimated effort.
- `solid_diag/` — optional directory with AST snippets, example diffs, and suggested patches.

## Usage

1. Run the `Analyzer` against `solution_path` to produce `solid_findings.json`.
2. Run the `Scorer` to compute overall SOLID score and breakdown per principle.
3. Generate `Fix Suggestions` from `solid_findings.json` to get refactor examples.
4. Optionally run `PR Review` to post comments and a summary score on pull requests.

## Principles & Examples

### Single Responsibility Principle (SRP)
- Detects a single class performing unrelated tasks, too many public methods or large bodies.
-
> **Common patterns**
  * Class containing both persistence and communication logic.
  * Methods with names like `Create`, `Save`, `Delete` co‑existing with UI or logging in the same class.
  * A single method that does >300 lines of code.
- **Example violation** – mixed responsibilities:
-
```csharp
public class UserService {
    public void CreateUser(UserDto dto) { /* create */ }
    private void SaveToDatabase(User user) { /* DB logic */ }
    private void SendVerificationEmail(string email) { /* send mail */ }
}
```
- **Detection heuristics**
  * Count of public methods > N (configurable, default 5).
  * Presence of `Save`, `Retrieve`, or repository‑like names along with business logic.
  * Methods that directly instantiate `DbContext` or send emails.
- **Suggested refactor** – split responsibilities: 
  1. `IUserRepository` for persistence.
  2. `IEmailSender` for communication.
  3. Thin orchestrating service calling them.

### Extended Analysis Features
- Cross-module analysis: find responsibilities that span multiple projects/assemblies.
- Dependency graph generation: produce a directed graph of project and type dependencies and highlight high-centrality nodes.
- Temporal code-change analysis: if VCS history available, detect recent changes that increased coupling or responsibility breadth.
- Risk scoring per finding: classify each violation as Low/Medium/High and provide a confidence score.
- Example automated fix snippets: where feasible, generate minimal code diffs illustrating the suggested refactor.



### Open Closed Principle (OCP)
- Detects large conditional blocks or switches that should use polymorphism.

### Liskov Substitution Principle (LSP)
- Detects subclasses that break base-class contracts (e.g., methods that throw unexpectedly).

### Interface Segregation Principle (ISP)
- Detects fat interfaces used by multiple clients; suggests splitting interfaces.

### Dependency Inversion Principle (DIP)
- Detects concrete dependencies in high-level modules; suggests introducing abstractions and DI.

## Health Scoring and Metrics
- overall_health_score: 0-100 (weighted composition of principle scores, code churn, test-coverage impact, and coupling).
- principle_scores: object with SRP/OCP/LSP/ISP/DIP each 0-20.
- module_scores: per-project scores and top 10 risky types.
- coupling_index: normalized 0-1 measure of inter-module coupling.
- churn_risk: metric showing recent change velocity for risky files.
- suggested_effort: rough person-days estimate to remediate top N issues.

Scoring example: overall_health_score = 0.5 * avg(principle_scores_normalized) + 0.3*(1 - coupling_index) + 0.2*(1 - churn_risk)

## Scoring

Score is out of 100 (20 points per principle). Interpretation:

- 90–100: Excellent
- 70–89: Good
- 50–69: Needs improvement
- <50: Poor

### Health Report Structure (JSON)

```
{
  "overall_health_score": 72,
  "principle_scores": {"SRP":14,"OCP":15,"LSP":13,"ISP":15,"DIP":15},
  "module_scores": {"Project.Api":78,"Project.Core":65},
  "top_findings": [ {"id":"F-001","principle":"SRP","risk":"High","file":"src/Service/UserManager.cs","summary":"Mixed persistence and communication"} ]
}
```

## PR Review Example

SOLID Review Summary

Score: 72/100

Issues detected:
- `UserManager` violates SRP
- `PaymentService` violates OCP
- `OrderService` tightly coupled to SQL repository

Recommendations:
- Split responsibilities, introduce strategy pattern, and add repository abstractions.

## Automated Suggestions & Action Plan
- Prioritized tasks: generated `solid_action_plan.md` with task list, priority, and estimated effort.
- Quick fixes: small refactors (extract interface, introduce constructor DI) auto-generated as patch suggestions under `solid_diag/patches/`.
- Manual recommendations: larger architectural suggestions that need human review with example code and rationale.

## Usage - Extended
1. Run the `Analyzer` against `solution_path` or `repository_root` to produce `solid_findings.json` and `solid_health_report.json`.
2. Review `solid_health_report.json` for overall health and `solid_action_plan.md` for prioritized fixes.
3. Apply quick patches from `solid_diag/patches/` or use suggestions to implement larger refactors.
4. Re-run analysis to validate improvements and track trend over time.

## Integration and Automation
- CI check: fail if `overall_health_score` below threshold (configurable).
- Pull request bot: post top 3 findings with suggested quick fixes as review comments.
- Dashboard: ingest `solid_health_report.json` to visualize trend and hotspots.

## Implementation Notes
- Analyzer should leverage Roslyn for syntax and semantic analysis, and optionally `git` for temporal analysis.
- Use graph libraries (e.g., QuickGraph) to produce dependency graphs and compute centrality.
- Persist intermediate artifacts to `solid_diag/` for auditability and reproducibility.

---

This extended skill adds cross-module, temporal, and risk-aware analysis, plus health scoring, prioritized action plans, and automated patch suggestions to help teams remediate SOLID violations at scale.
