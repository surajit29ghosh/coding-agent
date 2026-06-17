---
name: custom-layered-architecture
description: Enterprise Custom Layered Architecture analyzer for .NET projects - custom layer validation, adherence scoring, custom pattern detection, health metrics, and PR automation.
tags:
  - architecture
  - layered
  - custom
  - .net
  - csharp
  - organization
  - patterns
---

# Custom Layered Architecture Skill for .NET

## Overview
Comprehensive Custom Layered Architecture conformity analyzer for .NET solutions. Validates adherence to custom layer definitions, assesses layer-specific patterns, and provides health metrics aligned with project-specific architectural requirements.

## Core Architecture Principles Verified

### 1. **Custom Layer Definitions**
- User-defined layer specifications
- Layer naming and identification
- Clear layer purposes and responsibilities
- Flexible layer organization
- Organization-specific patterns

### 2. **Custom Dependency Rules**
- Project-defined dependency directions
- Custom layer ordering
- Allowed and prohibited dependencies
- Cross-cutting layer exceptions
- Bypass rules and their justification

### 3. **Pattern Adherence**
- Custom architectural patterns
- Organization-specific conventions
- Naming standards
- Folder structure requirements
- Project layout expectations

### 4. **Technology Integration**
- Framework-specific layer placement
- ORM usage patterns per layer
- Logging and monitoring placement
- Caching strategy implementation
- Security concern distribution

### 5. **Custom Metrics**
- Organization-specific code metrics
- Custom complexity thresholds
- Layer-specific expectations
- Coupling baselines per layer
- Performance metrics

### 6. **Customizable Validation Rules**
- Business rule enforcement
- Architectural decision enforcement
- Coding standard enforcement
- Team-specific guidelines
- Project-specific constraints

### 7. **Flexible Scoring**
- Custom scoring algorithms
- Organization-defined weights
- Project-specific baselines
- Custom success criteria
- Organizational KPIs

## Comprehensive Analysis Coverage

### Phase 1: Custom Layer Configuration & Validation
- Layer Definition Loading (YAML/JSON configuration)
- Custom Layer Structure Validation
- Layer Identification Rules
- Project/Namespace Mapping to Layers
- Configuration Compliance

### Phase 2: Custom Dependency Analysis
- Custom Dependency Rule Parsing
- Dependency Direction Validation
- Allowed Cross-layer Communication
- Prohibited Dependency Detection
- Exception Rule Handling

### Phase 3: Pattern Compliance Analysis
- Custom Pattern Detection
- Naming Convention Validation
- Folder Structure Verification
- Project Layout Conformance
- Organizational Practice Adherence

### Phase 4: Custom Metric Calculation
- Organization-defined Metrics
- Threshold Validation
- Baseline Comparisons
- Anomaly Detection
- Trend Analysis

### Phase 5: Custom Rule Enforcement
- Business Rule Validation
- Architectural Decision Verification
- Coding Standard Enforcement
- Team-specific Guideline Adherence
- Project Constraint Checking

## Health Scoring System

Multi-dimensional scoring across 10+ custom weighted categories (0-100 scale):

| Category | Default Weight | Description |
|----------|---|---|
| **Custom Layer Adherence** | 20% | Following custom layer definitions |
| **Dependency Rule Compliance** | 18% | Adhering to custom dependency rules |
| **Pattern Compliance** | 15% | Following organization patterns |
| **Naming Consistency** | 12% | Organization naming standards |
| **Technology Integration** | 10% | Framework/technology placement |
| **Custom Metrics** | 8% | Custom metric thresholds |
| **Coding Standards** | 7% | Team coding standards |
| **Documentation** | 5% | Architecture documentation |
| **Test Coverage** | 3% | Testing per custom criteria |
| **Performance** | 2% | Custom performance criteria |

**Customizable by Organization:**
- Weight adjustments per category
- Custom category addition
- Threshold customization
- Metric definition
- Success criteria

**Health Score Levels:**
- **90-100**: Excellent - Excellent adherence to custom architecture
- **75-89**: Good - Minor deviations from standards
- **60-74**: Fair - Several issues, moderate correction needed
- **40-59**: Poor - Significant deviations, substantial work
- **0-39**: Critical - Severe non-compliance, immediate action

## Component Structure

### 1. Analyzer
Detects custom architecture deviations:
- Custom layer boundary violations
- Custom dependency rule violations
- Pattern non-compliance
- Naming inconsistencies
- Technology placement issues
- Custom metric violations
- Business rule violations
- Coding standard breaches
- Custom constraint violations

### 2. Scorer
Computes custom health metrics:
- Layer adherence score
- Custom dependency compliance
- Pattern compliance score
- Metric compliance per category
- Custom aggregate scoring
- Organization-specific KPIs
- Customizable health index

### 3. Fix Suggestions
Refactoring for custom architecture:
- Layer boundary corrections
- Dependency rule violations fixes
- Pattern compliance refactoring
- Naming standardization
- Technology relocation
- Custom metric threshold resolution
- Coding standard alignment
- Custom rule compliance fixes

### 4. PR Review Automation
Custom architecture PR reviews:
- Custom layer violations
- Custom dependency rule violations
- Pattern non-compliance detection
- Naming standard breaches
- Technology placement issues
- Custom metric impacts
- Business rule violations
- Positive pattern reinforcement

## Custom Configuration

```yaml
layers:
  - name: "API"
    patterns: ["*.API", "*.Web"]
    namespace_patterns: ["*.API.*", "*.Web.*"]
    max_depth: 2
    allowed_dependencies:
      - "Application"
      - "Infrastructure"
    forbidden_dependencies:
      - "Database"
      - "Domain"  # Commented out: Legacy exception
    allowed_frameworks:
      - "AspNetCore"
    forbidden_frameworks:
      - "EntityFramework"
    
  - name: "Application"
    patterns: ["*.Application"]
    allowed_dependencies:
      - "Domain"
      - "Infrastructure"
    forbidden_dependencies:
      - "API"
    
  - name: "Domain"
    patterns: ["*.Domain"]
    allowed_dependencies: []
    forbidden_frameworks:
      - "EntityFramework"
      - "AspNetCore"
    
  - name: "Infrastructure"
    patterns: ["*.Infrastructure"]
    allowed_dependencies:
      - "Domain"
      - "Application"

rules:
  - name: "no_business_logic_in_api"
    condition: "!contains_business_logic(api_layer)"
    severity: "CRITICAL"
    
  - name: "database_access_only_in_infrastructure"
    condition: "!contains_database_access(api_layer, application_layer)"
    severity: "MAJOR"
    
  - name: "service_naming_convention"
    pattern: ".*Service$"
    applies_to: ["application_layer"]
    severity: "MINOR"

scoring:
  categories:
    - name: "CustomLayerAdherence"
      weight: 20
      metrics: ["layer_violations", "boundary_breaches"]
    
    - name: "DependencyRuleCompliance"
      weight: 18
      metrics: ["dependency_rule_violations"]
    
    - name: "PatternCompliance"
      weight: 15
      metrics: ["pattern_violations", "naming_violations"]

metrics:
  - name: "ClassesPerLayer"
    target: [15, 30]  # Acceptable range
    
  - name: "MaxCyclomaticComplexity"
    target: 10
    per_layer:
      API: 8
      Application: 12
      Domain: 15
    
  - name: "TestCoveragePercentage"
    target: 75
    per_layer:
      Application: 90
      Domain: 95
      Infrastructure: 70

reporting:
  custom_metrics:
    - "business_rule_violations"
    - "architectural_decision_adherence"
    - "team_guideline_compliance"
  
  export_formats:
    - "json"
    - "markdown"
    - "html"
    - "custom_xml"
```

## Usage Scenarios

- Define organization-specific architecture
- Enforce team standards during development
- Continuous validation in CI/CD
- Custom reporting and analytics
- Multi-project consistency across organization
- Support for various architectural patterns

## Integration Points

- Custom Rule Engine
- Organization Metric Dashboard
- Custom Report Generation
- Team Onboarding Automation
- Standards Documentation

## Team Guidelines

1. Define architecture explicitly - Document custom layers and rules
2. Maintain configuration - Keep definitions current
3. Justify exceptions - Document why rules are bypassed
4. Communicate changes - Alert team of architecture updates
5. Train consistently - Ensure team understands custom architecture
6. Measure adherence - Track compliance over time
7. Refactor proactively - Address violations promptly
8. Share patterns - Document proven solutions
9. Review regularly - Quarterly architecture review
10. Evolve thoughtfully - Update standards with team input

## Configuration Management

- **Version Control**: Architecture configuration in repository
- **Review Process**: Architecture changes go through PR review
- **Team Communication**: Architecture changes announced to team
- **Migration Paths**: Documented transitions for standard changes
- **Rollback Plans**: Clear process for reverting changes

## Related Documentation
- [Domain-Driven Design - Eric Evans](https://www.domainlanguage.com/ddd/)
- [Clean Architecture - Robert C. Martin](https://www.amazon.com/Clean-Architecture-Craftsmans-Software-Structure/dp/0134494164)
- [Architectural Decision Records](https://adr.github.io/)
- [Architecture Decision Logging](https://github.com/joelparkerhenderson/architecture_decision_record)
