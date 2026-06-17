---
name: monolith-architecture
description: Enterprise Monolith Architecture analyzer for .NET projects - structure validation, complexity assessment, multi-dimensional health scoring, refactoring guidance, and modernization support.
tags:
  - architecture
  - monolith
  - legacy-code
  - .net
  - csharp
  - maintainability
  - refactoring
---

# Monolith Architecture Skill for .NET

## Overview
Comprehensive Monolith Architecture conformity analyzer for .NET solutions. Assesses code organization, evaluates separation of concerns, analyzes coupling and complexity, and provides strategic guidance for modernization and refactoring.

## Core Architecture Principles Verified

### 1. **Layered Organization**
- Proper separation of concerns
- Clear layer definitions (Presentation, Business, Data)
- Unidirectional layer dependencies
- No business logic in presentation layer
- No presentation concerns in business layer

### 2. **Coupling & Cohesion**
- Minimal coupling between components
- High cohesion within components
- Reduced dependencies on shared utilities
- Avoided god objects and god methods
- Clear module boundaries

### 3. **Code Organization**
- Logical folder/namespace structure
- Related classes grouped appropriately
- Namespace hierarchy reflecting architecture
- No orphaned classes or utilities
- Consistent organization patterns

### 4. **Class Responsibility**
- Single Responsibility Principle
- Classes focused on one reason to change
- Balanced class sizes
- Avoided god classes
- Clear class purposes

### 5. **Method Quality**
- Reasonable method lengths
- Clear method names
- Single method responsibility
- Cyclomatic complexity within bounds
- Proper parameter counts

### 6. **Configuration Management**
- Externalized configuration
- Environment-specific settings
- No hardcoded values
- Configuration per deployment
- Feature flags for toggles

### 7. **Cross-Cutting Concerns**
- Proper logging placement
- Consistent exception handling
- Caching abstraction
- Transaction management
- Security concern isolation

## Comprehensive Analysis Coverage

### Phase 1: Structural Organization Analysis
- Layer Definition and Classification
- Namespace/Folder Structure Validation
- Component Identification
- Cross-cutting Concern Location
- Framework and Library Distribution

### Phase 2: Code Organization Assessment
- Class Organization (per package/namespace)
- Method Distribution and Balance
- Type Classification (entities, services, utilities)
- Dead code and orphaned classes
- Naming convention adherence

### Phase 3: Coupling & Complexity Analysis
- Dependency Chain Analysis
- Circular Dependency Detection
- Class coupling metrics (low, medium, high)
- Method complexity (cyclomatic)
- Inheritance hierarchy depth

### Phase 4: Separation of Concerns
- Business logic in wrong layers
- Presentation logic distribution
- Data access encapsulation
- Cross-cutting concern scattering
- Framework dependency location

### Phase 5: Modernization Readiness Assessment
- Modularization potential
- Microservices extraction candidates
- Legacy code concentration
- Test coverage per area
- Technical debt hotspots

## Health Scoring System

Multi-dimensional scoring across 12 weighted categories (0-100 scale):

| Category | Weight | Evaluation Criteria |
|----------|--------|-------------------|
| **Layer Separation** | 13% | Clear layers, proper dependencies |
| **Coupling Balance** | 13% | Low coupling, minimal dependencies |
| **Class Organization** | 12% | Logical grouping, clear purposes |
| **Method Quality** | 11% | Reasonable sizes, clear names, low complexity |
| **Code Organization** | 10% | Namespace hierarchy, folder structure |
| **Cohesion** | 9% | Classes focused, high internal coherence |
| **Configuration Mgmt** | 8% | Externalized, environment-specific |
| **Exception Handling** | 7% | Consistent, appropriate catching |
| **Logging** | 6% | Proper placement, non-intrusive |
| **Testing Support** | 5% | Testable design, mockable dependencies |
| **Naming Conventions** | 4% | Clear, descriptive, consistent |
| **Documentation** | 2% | Code comments, architectural clarity |

**Health Score Levels:**
- **90-100**: Excellent - Well-organized monolith
- **75-89**: Good - Minor organization issues
- **60-74**: Fair - Several issues, moderate refactoring
- **40-59**: Poor - Significant problems, substantial work
- **0-39**: Critical - Big ball of mud, emergency intervention

## Component Structure

### 1. Analyzer
Detects monolith architecture deviations:
- Layer violation detection
- Business logic in controllers
- God class identification
- Circular dependencies
- Excessive method complexity
- Hardcoded configuration
- Scattered concerns
- Dead code and orphaned classes
- Testing barriers
- Modernization blockers

### 2. Scorer
Computes monolith health metrics:
- Organization score per layer
- Coupling metrics per module
- Class complexity distribution
- Method complexity metrics
- Configuration externalization level
- Technical debt assessment
- Modernization readiness

### 3. Fix Suggestions
Refactoring patterns for monolith improvement:
- Extract methods from god classes
- Move business logic to services
- Separate presentation concerns
- Reduce class coupling
- Simplify inheritance hierarchies
- Externalize configuration
- Add proper exception handling
- Improve logging placement
- Extract modules for modularization
- Identify microservices candidates

### 4. PR Review Automation
Intelligent monolith architecture reviews:
- Layer violations
- Growing complexity
- God class additions
- Circular dependencies
- Configuration hardcoding
- Concern scattering
- Testing barrier creation
- Positive refactoring patterns

## Violation Severity Levels

- **CRITICAL**: Business logic in presentation, reverse layer dependencies
- **MAJOR**: God classes, circular dependencies, high complexity methods
- **MODERATE**: Coupling increases, organization issues, concern scattering
- **MINOR**: Naming violations, documentation gaps, configuration issues

## Monolith Metrics

### Class Metrics
```
Methods Per Class (avg, max)
Lines of Code Per Class (avg, max)
Cyclomatic Complexity Per Method (avg, max)
Afferent Coupling (classes depending on this)
Efferent Coupling (this class depends on)
```

### Layer Metrics
```
Layer Violation Count (per layer)
Cross-layer Coupling
Unidirectional Dependency Adherence
Layer Distribution (code percentage per layer)
```

### Modernization Index
```
M = ModuleIndependence × TestCoverage × LowCoupling
  - Close to 1.0: Ready for modularization/extraction
  - Close to 0.0: Significant refactoring needed first
```

## Usage Scenarios

- Monolith Health Assessment
- Codebase Organization Audit
- Continuous Quality Monitoring
- Refactoring Roadmap Planning
- Microservices Extraction Assessment

## Integration Points

- Build System: Code metrics collection
- IDE: Real-time code smell detection
- CI/CD: Continuous quality metrics
- Testing: Coverage per layer/module
- Documentation: Architecture visualization

## Configuration Options

```yaml
analysis:
  organization:
    max_namespace_depth: 5
    require_layer_naming: true
  
  complexity:
    max_cyclomatic_complexity: 10
    max_method_length_lines: 20
    max_class_methods: 15
  
  coupling:
    max_afferent_coupling: 15
    max_efferent_coupling: 10
    allow_circular_dependencies: false
  
  patterns:
    detect_god_classes: true
    detect_dead_code: true
    detect_scattered_concerns: true
```

## Team Guidelines

1. Respect layer boundaries - Clear separation of concerns
2. Keep classes focused - Single responsibility
3. Methods are small - Easy to understand and test
4. Minimize coupling - Explicit dependencies
5. Externalize configuration - No hardcoded values
6. Handle exceptions properly - Consistent strategy
7. Log appropriately - Not intrusive
8. Write testable code - Mock-friendly interfaces
9. Refactor continuously - Don't let decay accumulate
10. Plan modernization - Path to modularization/microservices

## Modernization Path

- Phase 1: Extract tightly-coupled modules
- Phase 2: Separate data per logical module
- Phase 3: Implement event-driven communication
- Phase 4: Add feature flags for independent deployment
- Phase 5: Extract critical modules as microservices
- Phase 6: Establish module contracts and APIs

## Related Documentation
- [Clean Architecture - Robert C. Martin](https://www.amazon.com/Clean-Architecture-Craftsmans-Software-Structure/dp/0134494164)
- [Refactoring to Patterns - Joshua Kerievsky](https://refactoring.com/catalog/)
- [The Pragmatic Programmer](https://pragprog.com/titles/tpp20/the-pragmatic-programmer-your-journey-to-mastery-second-edition/)
- [Modular Monolith Primer - Kamil Grzybek](https://www.kamilgrzybek.com/design/modular-monolith-primer/)
