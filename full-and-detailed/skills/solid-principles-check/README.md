# SOLID Principles Check Skill

Brief: Analyzes .NET solutions/projects for SOLID violations (SRP, OCP, LSP, ISP, DIP), produces a health score, prioritized remediation tasks, and optional quick-patch suggestions suitable for CI and PR automation.

Usage
- Run analyzer: point to a solution or repository root.

Example CLI (pseudo):
```
dotnet run --project tools/SolidAnalyzer -- --solution ./src/MySolution.sln --out ./reports/solid_findings.json --profile full
```

Key outputs
- `solid_findings.json` — detailed findings per file/type.
- `solid_health_report.json` — aggregated health and per-principle scores.
- `solid_action_plan.md` — prioritized remediation tasks with effort estimates.
- `solid_diag/` — optional artifacts: AST snippets, example diffs, patches.

Features
- Cross-module dependency and centrality analysis.
- Temporal (git) analysis to detect recent coupling increases.
- Risk scoring with confidence and estimated remediation effort.
- Quick-patch generation for small refactors (extract interface, constructor DI).

CI / PR integration
- Fail CI when `overall_health_score` < configurable threshold.
- Post top-N findings as PR review comments with suggested quick fixes.

Implementation notes
- Analyzer should use Roslyn for semantic analysis and `git` for temporal data.
- Graph analysis can use QuickGraph or similar for dependency centrality.

How to extend
- Adjust `analysis_profile` to tune heuristics and thresholds.
- Add custom rule modules that output findings in the `solid_findings.json` schema.

Contact
- For help or contributions, open an issue or PR in this repository.
