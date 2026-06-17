---
name: component-architecture
description: Enterprise Component Architecture analyzer for .NET projects - decomposition validation, independence assessment, multi-dimensional health scoring, refactoring guidance, and PR automation.
tags:
  - architecture
  - components
  - modular
  - .net
  - csharp
  - encapsulation
  - composition
---

# Component Architecture Skill for .NET

## Overview
Comprehensive Component Architecture conformity analyzer for .NET solutions. Evaluates component independence, proper decomposition, communication patterns, and provides detailed health metrics with actionable refactoring guidance.

## Core Architecture Principles Verified

### 1. **Component Cohesion**
- Logical grouping of related functionality
- High internal cohesion within components
- Clear, well-defined responsibilities
- Single reason to change (component-level SRP)
- Semantic versioning and stability

### 2. **Component Coupling**
- Low coupling between components
- Explicit, stable dependencies
- No circular component dependencies
- Acyclic Dependency Graph (ADP) principle
- Dependency inversion applied to components

### 3. **Component Boundaries**
- Clear, enforced public interfaces
- Encapsulation of internal details
- Version stability and compatibility
- API contracts between components
- Deprecation and migration paths

### 4. **Component Communication**
- Asynchronous messaging patterns (event-driven)
- Synchronous service calls with interfaces
- Contract-based integration
- Anti-corruption layers for external components
- Proper marshaling of data across boundaries

### 5. **Component Structure**
- Focused scope and clear purpose
- Balanced component sizing (not too large, not too small)
- Supporting packages properly organized
- Resource management per component
- Component-level transactions/consistency

### 6. **Dependency Management**
- Stable Abstractions Principle (SAP)
- Abstractness vs. Instability metrics
- Lower-level components more stable
- Higher-level components more abstract
- Dependency chains well-managed

### 7. **Reusability & Composability**
- Components can be independently deployed
- Composable without tight coupling
- Pluggable implementations
- Framework-independent components
- Easy to test in isolation

## Comprehensive Analysis Coverage

### Phase 1: Component Discovery & Classification
- Component Identification (project/namespace/package-based)
- Component Metadata (purpose, API, version, stability)
- Organizational Structure (hierarchy, internal vs external packages)
- Implicit component detection

### Phase 2: Cohesion Analysis
- Functional Coherence (related functionality grouping, semantic coherence)
- Type Distribution (per-component metrics, exposure analysis)
- Feature Completeness (self-contained functionality, redundancy detection)

### Phase 3: Coupling Analysis
- Dependency Direction (acyclic graph, circular detection, transitive analysis)
- Coupling Metrics (efferent, afferent, instability index, abstractness)
- Communication Patterns (direct instantiation, service locators, events)

### Phase 4: Interface & Contract Analysis
- Public API (stability, versioning, backward compatibility)
- Version Management (semantic versioning, breaking changes, deprecation)
- Integration Patterns (sync/async, request-reply, pub-sub, saga patterns)

### Phase 5: Reusability Assessment
- Deployment Independence (standalone deployability, runtime dependencies)
- Composability (pluggable implementations, feature flags, extensions)
- Testability (mock-friendly, DI, integration testing)

## Health Scoring System

Multi-dimensional scoring across 10 weighted categories (0-100 scale):

| Category | Weight | Evaluation Criteria |
|----------|--------|-------------------|
| **Component Cohesion** | 15% | Related functionality, single purpose, no fragmentation |
| **Coupling Balance** | 15% | Low coupling, stable abstractions, dependency direction |
| **Acyclic Dependencies** | 12% | No circular dependencies, clear dependency direction |
| **API Stability** | 12% | Interface stability, versioning, backward compatibility |
| **Communication Patterns** | 10% | Proper async/sync choices, contract-based integration |
| **Encapsulation** | 10% | Hidden implementation, public interface clarity |
| **Reusability** | 10% | Standalone deployable, composable, pluggable |
| **Documentation** | 8% | API docs, component purpose, integration guide |
| **Naming Consistency** | 5% | Clear names, consistency, descriptiveness |
| **Testing Support** | 3% | Testability, mocking, integration tests |

**Health Score Levels:**
- **90-100**: Excellent - Near-perfect component architecture
- **75-89**: Good - Minor coupling issues, mostly well-designed
- **60-74**: Fair - Several design issues, moderate refactoring needed
- **40-59**: Poor - Significant coupling problems, substantial work required
- **0-39**: Critical - Component architecture decay, immediate intervention

## Component Structure

### 1. Analyzer
Detects component architecture deviations:
- Component boundary violations
- Circular component dependencies
- Encapsulation breaches
- Stability principle violations
- Communication pattern issues
- API contract violations
- Reusability assessment

### 2. Scorer
Computes component health metrics:
- Component cohesion score
- Coupling metrics (efferent, afferent, instability)
- Abstractness index
- Component stability matrix
- Dependency graph analysis
- API surface metrics

### 3. Fix Suggestions
Refactoring patterns for component improvement:
- Split large components
- Merge fragmented functionality
- Resolve circular dependencies
- Extract shared abstractions
- Improve component interfaces
- Add missing components
- Simplify communication patterns
- Improve encapsulation

### 4. PR Review Automation
Intelligent component architecture reviews:
- Component boundary violations
- New circular dependencies
- Encapsulation breaches
- API contract changes
- Communication pattern issues
- Positive reinforcement for patterns

## Violation Severity Levels

- **CRITICAL**: Circular dependencies, reverse dependencies
- **MAJOR**: Encapsulation breach, API violation, stability violation
- **MODERATE**: Coupling imbalance, pattern inconsistency
- **MINOR**: Naming violation, documentation gaps

## Component Metrics

### Coupling Metrics
```
Efferent Coupling (Ce): Outbound component dependencies
Afferent Coupling (Ca): Inbound component dependencies
Instability (I): Ce / (Ce + Ca)
  - I = 0: Maximally stable (no outbound dependencies)
  - I = 1: Maximally unstable (no inbound dependencies)
```

### Abstractness
```
Abstractness (A): Abstract types / Total types
  - High A: Good for higher-level components
  - Low A: Good for lower-level components
```

### Distance from Main Sequence
```
D = |A + I - 1|
  - D close to 0: Well-positioned
  - D close to 1: Poorly positioned
```

## Usage Scenarios

- Initial Architecture Assessment
- Continuous Validation & PR Reviews
- Refactoring Guidance
- Microservices Planning & Extraction

## Integration Points

- Build System: MSBuild validation
- IDE: Real-time boundary checks
- CI/CD: Automated coupling metrics
- Repository: Pre-commit validation
- Monitoring: Health dashboard

## Configuration Options

```yaml
analysis:
  component_detection:
    by_project: true
    by_namespace: true
    by_package: true
  coupling:
    max_instability: 0.7
    max_depth: 5
  cohesion:
    min_types_per_component: 2
    max_types_per_component: 50
```

## Team Guidelines

1. Maintain component boundaries - No sneaking dependencies
2. Keep components focused - Single, clear responsibility
3. Minimize inter-component coupling - Use stable abstractions
4. Design for reusability - Consider standalone deployability
5. Version component APIs - Track compatibility carefully
6. Use events for loose coupling - Prefer pub-sub over direct calls
7. Encapsulate internals - Hide implementation details
8. Document component contracts - Clear public APIs
9. Monitor coupling metrics - Track instability over time
10. Plan for microservices - Design for potential extraction

## Related Documentation
- [Component Design - Robert C. Martin](https://www.amazon.com/Clean-Architecture-Craftsmans-Software-Structure/dp/0134494164)
- [Modular Monolith Architecture](https://www.kamilgrzybek.com/design/modular-monolith-primer/)
- [Building Microservices - Sam Newman](https://samnewman.io/books/building_microservices_2nd_edition/)
