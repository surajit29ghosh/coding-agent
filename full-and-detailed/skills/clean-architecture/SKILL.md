---
name: clean-architecture
description: Enterprise-grade Clean Architecture analyzer for .NET projects - comprehensive deviation detection, multi-dimensional health scoring, intelligent fix suggestions, and PR automation.
tags:
  - architecture
  - clean-code
  - .net
  - csharp
  - refactoring
  - dependency-injection
  - patterns
---

# Clean Architecture Skill for .NET

## Overview
Comprehensive Clean Architecture conformity analyzer for .NET solutions. Identifies architectural deviations, computes multi-dimensional health scores, suggests refactoring patterns, and provides PR automation with actionable feedback.

## Core Architecture Principles Verified

### 1. **Layered Architecture**
- Presentation Layer (Controllers, Views, API Endpoints)
- Application Layer (Use Cases, Interactors, Services)
- Domain Layer (Entities, Value Objects, Business Rules)
- Infrastructure Layer (Data Access, External Services, Framework Concerns)
- Dependency Direction: Always inward (outer → inner, never inner → outer)

### 2. **Dependency Inversion**
- High-level modules independent of low-level modules
- Both depend on abstractions (interfaces)
- Infrastructure implementations injected into Application/Domain
- No direct references to concrete implementations in business logic

### 3. **Domain Driven Design (DDD)**
- Entity identification and proper aggregation
- Value Objects with immutability
- Bounded Context recognition
- Domain Events and Event Sourcing patterns
- Repository pattern for aggregates (not entities)
- Anti-corruption layers for external integrations

### 4. **Use Case/Interactor Pattern**
- Clear one-use-case-per-class principle
- Use case input ports (interfaces)
- Use case output ports (interfaces/DTOs)
- Separation of concerns across use cases
- No business logic in controllers or UI

### 5. **Interface Segregation**
- Small, focused interfaces (ISP)
- No fat interfaces causing artificial dependencies
- Proper abstraction hierarchies
- Clear contracts for cross-layer communication

### 6. **Entity Purity**
- Domain entities free from infrastructure concerns
- No direct database persistence attributes
- No tight coupling to frameworks
- Domain logic encapsulated in entities
- No leakage of persistence state

### 7. **Data Transfer Objects (DTOs)**
- Proper DTO usage for layer boundaries
- Domain-to-Presentation DTO mapping
- External API DTO conversions
- No direct entity exposure across layers

## Comprehensive Analysis Coverage

### Phase 1: Structural Analysis
- **Project Organization**
  - Correct layer segregation by project/namespace
  - Naming conventions adherence
  - Circular dependency detection
  - Missing layer identification

- **Dependency Flow**
  - Bidirectional dependency warnings
  - Infrastructure → Domain references (violations)
  - Presentation → Domain direct coupling issues
  - Proper abstraction boundaries

- **Layer Composition**
  - Project count per layer
  - Namespace hierarchy correctness
  - Layer consolidation opportunities

### Phase 2: Code Pattern Analysis

- **Domain Layer Patterns**
  - Entity structure validation
  - Value Object detection
  - Business rule encapsulation
  - Aggregate root definitions
  - Rich domain model indicators
  - Missing domain logic indicators

- **Application Layer Patterns**
  - Use case/Interactor implementation
  - Use case input/output ports
  - Service locator anti-pattern detection
  - Proper dependency injection usage
  - Business logic leakage from domain
  - CQRS pattern adoption

- **Infrastructure Layer Patterns**
  - Repository pattern implementation
  - Unit of Work pattern usage
  - Database context management
  - External service abstraction
  - Logging/Monitoring integration
  - Configuration management

- **Presentation Layer Patterns**
  - Controller/Presenter thickness
  - Direct database access detection
  - Business logic in controllers
  - Proper model binding usage
  - API endpoint structure

### Phase 3: Dependency Analysis
- Direct vs. Interface dependencies
- Transitive dependency chains
- Framework dependency locations
- NuGet package distribution per layer
- Unused dependency detection
- Version conflict identification

### Phase 4: DDD Pattern Recognition
- Aggregate identification
- Bounded Context mapping
- Repository boundaries
- Entity vs. Value Object classification
- Domain Event patterns
- Ubiquitous Language consistency

## Health Scoring System

Multi-dimensional scoring across 12 weighted categories (0-100 scale):

| Category | Weight | Evaluation Criteria |
|----------|--------|-------------------|
| **Layer Isolation** | 15% | Proper separation, no violations, correct abstraction levels |
| **Dependency Flow** | 15% | Unidirectional dependencies, no cycles, proper abstractions |
| **Domain Purity** | 12% | Entity independence, no infrastructure concerns, rich models |
| **Use Case Pattern** | 12% | Clear interactors, proper ports, single responsibility |
| **Interface Quality** | 10% | ISP adherence, focused abstractions, clear contracts |
| **Abstraction Levels** | 8% | Proper hierarchy, no unnecessary levels, right-sized interfaces |
| **Repository Pattern** | 8% | Correct boundaries, aggregate adherence, abstraction |
| **DTOs & Mapping** | 7% | Proper conversion, no entity leakage, clear boundaries |
| **Testing Support** | 5% | Mockable dependencies, testable structure, isolation support |
| **Code Distribution** | 5% | Balanced layer sizes, no bloated layers, even distribution |
| **Naming Conventions** | 3% | Consistency, clarity, adherence to standards |
| **Documentation** | 4% | Code comments, architectural decisions, pattern documentation |

**Health Score Levels:**
- **90-100**: Excellent - Near-perfect architecture adherence
- **75-89**: Good - Minor deviations, mostly compliant
- **60-74**: Fair - Several deviations, moderate refactoring needed
- **40-59**: Poor - Significant violations, substantial refactoring required
- **0-39**: Critical - Severe architectural decay, immediate intervention needed

## Component Structure

### 1. Analyzer
Detects architectural deviations across entire codebase.

**Inputs:**
- Solution path or repository root
- Target framework (.NET 5+, .NET Framework 4.6+)
- Custom layer naming conventions (optional)

**Outputs:**
- `architecture_findings.json`
  - Violation categories
  - Severity levels
  - Affected files/namespaces
  - Code references with line numbers

**Checks Performed:**
- Layer boundary violations
- Circular dependencies
- DDD pattern compliance
- Naming convention adherence
- Repository pattern correctness
- Entity purity violations
- DTO boundary crossings
- Dependency direction validation
- Framework leakage detection
- Service locator patterns
- Tight coupling indicators

### 2. Scorer
Computes comprehensive health metrics.

**Inputs:**
- Architecture findings
- Solution statistics
- Code metrics

**Outputs:**
- `architecture_score.json`
  - Overall score (0-100)
  - Category scores
  - Trend analysis
  - Comparison benchmarks
  - Risk assessment

**Metrics Generated:**
- Layer compliance percentage
- Dependency correctness ratio
- Test coverage alignment
- Code smell density per layer
- Architectural complexity index
- Violation severity distribution

### 3. Fix Suggestions
Provides specific, actionable refactoring recommendations.

**Inputs:**
- Architecture findings
- Code patterns detected
- Violation severity

**Outputs:**
- `architecture_refactor_suggestions.md`
  - Prioritized recommendations
  - Before/after code examples
  - Implementation difficulty
  - Estimated effort
  - Risk assessment
  - Pattern migration guides

**Suggestion Categories:**
- Extract entity to domain layer
- Create repository abstraction
- Implement use case/interactor
- Add DTO conversion layer
- Extract interface for dependency injection
- Move infrastructure concern
- Resolve circular dependency
- Split bloated service
- Implement aggregate pattern
- Add event patterns
- Create bounded context
- Implement caching abstraction

### 4. PR Review Automation
Posts intelligent code review comments on pull requests.

**Inputs:**
- Changed files/code
- Architecture baseline
- Violation summary

**Outputs:**
- PR comments with:
  - Architectural impact assessment
  - Specific violation flags
  - Fix suggestions
  - Links to documentation

**Comment Types:**
- Layer violation warnings
- New circular dependencies
- Dependency direction violations
- Missing abstractions
- Positive reinforcement for patterns
- Pattern inconsistency alerts

## Violation Severity Levels

- **CRITICAL**: Direct layer boundary violation, reverse dependencies
- **MAJOR**: Infrastructure → Domain reference, business logic in controller
- **MODERATE**: DDD pattern inconsistency, missing abstraction
- **MINOR**: Naming convention violation, documentation missing

## Execution Flow

```
Input (Solution Path)
       ↓
   [ANALYZER]
   ├─ Scan project structure
   ├─ Analyze dependencies
   ├─ Check code patterns
   └─ Identify violations
       ↓
   Findings Output
       ↓
   [SCORER]
   ├─ Calculate category scores
   ├─ Aggregate metrics
   ├─ Assess trends
   └─ Generate risk matrix
       ↓
   Score Output
       ↓
   [FIX SUGGESTIONS]
   ├─ Prioritize violations
   ├─ Generate recommendations
   ├─ Create code examples
   └─ Estimate effort
       ↓
   Suggestions Output
       ↓
   [PR REVIEW] (if applicable)
   ├─ Review changed files
   ├─ Map to architecture
   ├─ Post comments
   └─ Link recommendations
       ↓
   PR Comments / Report
```

## Usage Scenarios

### Scenario 1: Initial Assessment
Analyze existing solution for architectural baseline
```
Input: solution path
Output: findings, score, suggestions
Action: Review findings, create refactoring roadmap
```

### Scenario 2: Continuous Validation
Scan on each PR/commit to prevent regression
```
Input: changed files, baseline
Output: PR comments, trend metrics
Action: Enforce architecture during development
```

### Scenario 3: Refactoring Guidance
Get step-by-step modernization path
```
Input: current architecture, target pattern
Output: prioritized suggestions, migration guides
Action: Execute refactoring incrementally
```

### Scenario 4: Onboarding/Documentation
Generate architecture documentation
```
Input: solution structure
Output: architecture report, diagrams, guidelines
Action: Share with team, establish standards
```

## Integration Points

### Build System Integration
- MSBuild tasks for CI/CD validation
- Fail build on critical violations
- Archive reports per build

### IDE Integration
- Real-time inline violation indicators
- Quick-fix suggestions
- Refactoring templates

### Repository Integration
- Pre-commit hooks for validation
- PR comment automation
- Branch protection rules

### Monitoring Integration
- Architecture metrics dashboard
- Trend tracking over time
- Health score alerts

## Output Formats

### Architecture Findings JSON
```json
{
  "summary": {
    "total_violations": 42,
    "critical": 3,
    "major": 8,
    "moderate": 18,
    "minor": 13
  },
  "violations": [
    {
      "id": "CIRC_DEP_001",
      "type": "circular_dependency",
      "severity": "CRITICAL",
      "description": "Circular dependency detected",
      "path": "Project A → Project B → Project A",
      "files": ["file1.cs", "file2.cs"],
      "recommendation": "Extract common interface to shared layer"
    }
  ],
  "patterns": {
    "ddd_compliance": 0.75,
    "layer_isolation": 0.82,
    "dependency_correctness": 0.68
  }
}
```

### Architecture Refactor Suggestions Markdown
```markdown
## Priority 1: Critical Violations (Estimated Effort: 3 days)

### 1. Resolve Circular Dependencies
- **Risk**: High
- **Impact**: Blocks unit testing, complicates maintenance
- **Before/After**: [code examples]
- **Steps**: [implementation steps]

## Priority 2: DDD Pattern Implementation
...
```

## Configuration Options

```yaml
analysis:
  target_framework: "net6.0"
  custom_layers:
    - name: "Presentation"
      patterns: ["*.Web", "*.API", "*.UI"]
    - name: "Application"
      patterns: ["*.Application", "*.Services"]
    - name: "Domain"
      patterns: ["*.Domain", "*.Core"]
    - name: "Infrastructure"
      patterns: ["*.Infrastructure", "*.Data"]

scoring:
  weights:
    layer_isolation: 15
    dependency_flow: 15
    domain_purity: 12
    # ... other categories

violations:
  fail_on_severity: "CRITICAL"
  warn_on_severity: "MAJOR"
  
reporting:
  include_metrics: true
  generate_diagrams: true
  export_formats: ["json", "md", "html"]
```

## Team Guidelines

1. **Enforce layer boundaries** - No exceptions for tight deadlines
2. **Maintain dependency direction** - Always inward/downward
3. **Keep domain logic in Domain layer** - Not in services or controllers
4. **Use interfaces for cross-layer communication**
5. **Create repositories for aggregate roots** - Not for all entities
6. **Use DTOs at layer boundaries** - Never expose entities directly
7. **Write testable code** - Dependency injection enables unit testing
8. **Document architectural decisions** - ADRs for patterns used
9. **Review violations promptly** - Don't let technical debt accumulate
10. **Measure progress** - Track health scores over time

## Related Documentation
- [Clean Architecture by Robert C. Martin](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html)
- [Domain-Driven Design by Eric Evans](https://www.domainlanguage.com/ddd/)
- [SOLID Principles](https://en.wikipedia.org/wiki/SOLID)
- [C# Coding Guidelines](https://github.com/dotnet/coding-conventions)
