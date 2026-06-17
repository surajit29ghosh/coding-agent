---
name: modular-monolith-architecture
description: Enterprise Modular Monolith Architecture analyzer for .NET projects - module boundary validation, coupling analysis, multi-dimensional health scoring, migration guidance, and PR automation.
tags:
  - architecture
  - modular-monolith
  - modularity
  - .net
  - csharp
  - scalability
  - microservices-ready
---

# Modular Monolith Architecture Skill for .NET

## Overview
Comprehensive Modular Monolith Architecture conformity analyzer for .NET solutions. Validates module boundaries, assesses independence, analyzes domain coherence, and provides health metrics with strategic guidance for microservices transition.

## Core Architecture Principles Verified

### 1. **Module Cohesion**
- Domain-driven module boundaries
- High internal cohesion
- Clear single responsibility per module
- Feature completeness within modules
- Logical organization

### 2. **Module Isolation**
- No circular module dependencies
- Explicit module interfaces
- Acyclic dependency graph
- Minimal cross-module coupling
- Internal encapsulation

### 3. **Data Management**
- Module-scoped data schemas
- Logical data boundaries
- Minimal cross-module joins
- Event-based data synchronization
- Transaction boundaries

### 4. **API Contracts**
- Well-defined module interfaces
- Clear service boundaries
- Versioning strategy
- Contract stability
- Anti-corruption layers for external modules

### 5. **Business Logic Organization**
- Business logic in domain layer
- Application services per module
- Use case patterns
- Command/Query separation
- Event publication

### 6. **Testing Strategy**
- Module-level unit testing
- Integration tests for boundaries
- Contract testing between modules
- Isolated testing capability
- Mock-friendly interfaces

### 7. **Deployment Readiness**
- Module-level feature toggling
- Independent module deployment (logical)
- Configuration per module
- Resource management per module
- Migration path to microservices

## Comprehensive Analysis Coverage

### Phase 1: Module Discovery & Classification
- Module Identification (by package, namespace, project)
- Business Capability mapping
- Module Ownership and stakeholders
- Stability and maturity levels
- Cross-cutting concern location

### Phase 2: Boundary Analysis
- Module Interface Definition
- Internal vs. Public API surface
- Encapsulation verification
- Data boundary validation
- Cross-module access patterns

### Phase 3: Coupling & Dependency Analysis
- Module dependency graph
- Circular dependency detection
- Instability metrics
- Abstractness calculation
- Coupling balance assessment

### Phase 4: Domain Analysis
- Bounded context alignment
- Ubiquitous language consistency
- Aggregate identification per module
- Repository pattern per module
- Domain event patterns

### Phase 5: Microservices Readiness Assessment
- Deployment independence (logical)
- Data isolation capability
- Communication pattern readiness
- Event-driven capability
- Independent scaling potential

## Health Scoring System

Multi-dimensional scoring across 11 weighted categories (0-100 scale):

| Category | Weight | Evaluation Criteria |
|----------|--------|-------------------|
| **Module Cohesion** | 14% | Logical grouping, domain alignment, completeness |
| **Coupling Balance** | 14% | Acyclic dependencies, low coupling, isolation |
| **Boundary Clarity** | 12% | Clear interfaces, explicit contracts, encapsulation |
| **Data Independence** | 12% | Module-scoped schemas, minimal cross-module joins |
| **Domain Organization** | 11% | Bounded contexts, aggregates, domain events |
| **API Quality** | 10% | Interface stability, versioning, backward compatibility |
| **Testing Support** | 10% | Mockability, integration tests, contract tests |
| **Business Logic** | 7% | Domain layer richness, application services |
| **Documentation** | 5% | Module purpose, API docs, integration guides |
| **Microservices Readiness** | 3% | Extraction potential, deployment logic |
| **Naming Consistency** | 2% | Clear, descriptive module names |

**Health Score Levels:**
- **90-100**: Excellent - Well-designed modular architecture
- **75-89**: Good - Minor coupling, mostly independent
- **60-74**: Fair - Several issues, moderate refactoring needed
- **40-59**: Poor - Significant coupling, substantial work required
- **0-39**: Critical - Monolithic spaghetti code, immediate intervention

## Component Structure

### 1. Analyzer
Detects modular monolith deviations:
- Module boundary violations
- Circular module dependencies
- Encapsulation breaches
- Cross-module data coupling
- Business logic distribution
- Missing event patterns
- Testing isolation issues
- Microservices extraction blockers

### 2. Scorer
Computes modular health metrics:
- Module cohesion score
- Coupling metrics per module
- Stability index per module
- Data independence score
- Domain alignment assessment
- Microservices extraction readiness

### 3. Fix Suggestions
Refactoring patterns for modularity improvement:
- Extract new modules
- Separate data boundaries
- Add explicit interfaces
- Resolve circular dependencies
- Implement event-driven patterns
- Add domain events
- Improve API contracts
- Enhance testability

### 4. PR Review Automation
Intelligent modular architecture reviews:
- Module boundary violations
- Cross-module coupling increases
- Encapsulation breaches
- Data boundary violations
- Missing domain events
- Testing isolation issues
- Microservices readiness impacts

## Violation Severity Levels

- **CRITICAL**: Circular dependencies, reverse dependencies
- **MAJOR**: Encapsulation breach, shared data coupling, logic misdistribution
- **MODERATE**: Coupling imbalance, missing events, interface issues
- **MINOR**: Naming inconsistency, documentation gaps

## Module Metrics

### Module Coupling
```
Efferent Coupling (Ce): Modules this depends on
Afferent Coupling (Ca): Modules depending on this
Instability (I): Ce / (Ce + Ca)
Distance (D): |A + I - 1|
```

### Microservices Extraction Index
```
E = ModuleIndependence × DataIndependence × DeploymentReadiness
  - Close to 1.0: Ready for extraction
  - Close to 0.0: Needs significant refactoring
```

## Usage Scenarios

- Module Architecture Assessment
- Modular Monolith Maturity Check
- Continuous Coupling Monitoring
- Microservices Transition Planning
- Module Boundary Validation

## Integration Points

- Build System: Module boundary enforcement
- CI/CD: Module dependency validation
- Feature Flags: Per-module deployment
- Testing: Module-level test suite organization
- Documentation: Module contract registry

## Configuration Options

```yaml
analysis:
  module_detection:
    by_project: true
    by_namespace: true
    by_package: true
  
  boundaries:
    enforce_module_isolation: true
    detect_circular_dependencies: true
    max_module_coupling: 5
  
  data:
    enforce_module_data_ownership: true
    detect_cross_module_joins: true
  
  microservices_readiness:
    assess_extraction_potential: true
    identify_independent_modules: true
```

## Team Guidelines

1. Respect module boundaries - No sneaking dependencies
2. Keep modules focused - Single business capability
3. Explicit module interfaces - Clear API contracts
4. Own module data - No shared schemas
5. Use domain events - Decouple with events
6. Test in isolation - Mock module boundaries
7. Document contracts - Clear module purpose
8. Plan extraction - Design for microservices
9. Monitor coupling - Track metrics over time
10. Version carefully - Maintain backward compatibility

## Microservices Transition Path

- Phase 1: Establish module boundaries and APIs
- Phase 2: Separate data per module (logical)
- Phase 3: Implement event-driven communication
- Phase 4: Add feature flags for independent deployment
- Phase 5: Extract critical modules as microservices

## Related Documentation
- [Modular Monolith Primer - Kamil Grzybek](https://www.kamilgrzybek.com/design/modular-monolith-primer/)
- [Modularity - Steve Tate](https://dev.to/stevegrunwell/modularity-1og)
- [Domain-Driven Design - Eric Evans](https://www.domainlanguage.com/ddd/)
- [Building Microservices - Sam Newman](https://samnewman.io/books/building_microservices_2nd_edition/)
