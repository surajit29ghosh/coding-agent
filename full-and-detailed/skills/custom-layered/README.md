# Custom Layered Architecture Analysis & Guidance

## Table of Contents
1. [Analysis & Detection](#analysis--detection)
2. [Scoring & Assessment](#scoring--assessment)
3. [Fix Suggestions](#fix-suggestions)
4. [PR Review Automation](#pr-review-automation)

---

## Analysis & Detection

### Purpose
Detects custom architecture violations by validating adherence to organization-specific layer definitions, dependency rules, patterns, and custom metrics.

### Analysis Phases

#### Phase 1: Configuration Loading & Validation
```
1. Load custom architecture configuration (YAML/JSON)
2. Parse layer definitions
3. Validate dependency rules
4. Load custom patterns
5. Load custom metrics
```

#### Phase 2: Layer Classification
```
1. Map projects/namespaces to layers
2. Validate layer structure
3. Identify miscategorized elements
4. Check naming conventions
5. Verify folder structure adherence
```

#### Phase 3: Dependency Rule Validation
```
1. Build dependency graph
2. Validate each dependency against rules
3. Detect prohibited dependencies
4. Check allowed dependencies
5. Verify exception handling
```

#### Phase 4: Pattern Compliance Analysis
```
1. Detect custom patterns
2. Validate naming standards
3. Check organizational conventions
4. Verify design patterns
5. Assess best practice adherence
```

#### Phase 5: Custom Metric Evaluation
```
1. Calculate custom metrics
2. Compare against thresholds
3. Detect anomalies
4. Assess trends
5. Generate alerts
```

### Violation Detection Rules

All configurable per organization:

- **CUSTOM_LAYER_VIOLATION**: Violations of custom layer definitions (severity: configurable)
- **CUSTOM_DEPENDENCY_VIOLATION**: Violations of custom dependency rules (severity: configurable)
- **PATTERN_VIOLATION**: Violations of custom patterns (severity: configurable)
- **CUSTOM_METRIC_VIOLATION**: Exceeding custom metric thresholds (severity: configurable)
- **BUSINESS_RULE_VIOLATION**: Violations of business rules (severity: configurable)

### Configuration-Driven Analysis

All analysis parameters are defined in organization configuration files, allowing full customization of violation rules, severity levels, and metrics.

---

## Scoring & Assessment

### Purpose
Dynamically computes architecture scores based on organization-specific configuration.

### Default Scoring Dimensions

All dimensions are customizable per organization.

| Dimension | Default Weight | Description |
|-----------|---|---|
| Custom Layer Adherence | 20% | Following custom layer definitions |
| Dependency Rule Compliance | 18% | Adhering to custom rules |
| Pattern Compliance | 15% | Following patterns |
| Naming Consistency | 12% | Standards adherence |
| Technology Integration | 10% | Framework placement |
| Custom Metrics | 8% | Threshold compliance |
| Coding Standards | 7% | Team standards |
| Documentation | 5% | Architecture docs |
| Test Coverage | 3% | Testing per criteria |
| Performance | 2% | Custom performance |

### Dynamic Scoring

```
Scoring calculated based on:
1. Load custom configuration (architecture.yaml)
2. Parse custom weights and metrics
3. Evaluate violations against custom severity
4. Calculate composite score
5. Compare against organizational baselines
```

### Score Interpretation

Organizations can define:
- Custom score ranges
- Custom grade mappings
- Custom interpretation messages
- Custom action thresholds
- Custom benchmark comparisons

### Output Format

```json
{
  "overall_score": 82,
  "assessment": "Good - Minor deviations from standards",
  "configuration_used": "architecture.yaml",
  "organization": "[Organization Name]",
  "category_scores": {...},
  "organizational_metrics": {...},
  "custom_benchmarks": {...},
  "violations_summary": {...}
}
```

---

## Fix Suggestions

### Dynamic Suggestion Generation

Suggestions are generated based on custom architecture configuration.

### Generic Fix Categories

#### Priority 1: Custom Critical Violations
As configured in architecture.yaml

**Pattern**: Custom critical rule violations
**Fix**: Depends on specific violation
**Effort**: As configured in architecture.yaml

#### Priority 2: Custom Major Issues
As configured

**Pattern**: Custom major violations
**Examples**:
- Layer boundary violations
- Dependency rule violations
- Business rule violations
- Configuration violations
**Effort**: Varies by violation

#### Priority 3: Custom Moderate Issues
As configured

**Pattern**: Custom moderate violations
**Examples**:
- Naming inconsistencies
- Pattern non-compliance
- Documentation gaps
**Effort**: Varies

---

### Fix Suggestion Template

```yaml
- id: CUSTOM_FIX_001
  violation: CUSTOM_LAYER_VIOLATION
  description: "[Organization-specific description]"
  pattern: "[Custom pattern being violated]"
  fix_options:
    - option_1: "[First approach]"
      effort: "X hours/days"
      risk: "Low/Medium/High"
      steps: ["Step 1", "Step 2"]
    - option_2: "[Second approach]"
      effort: "X hours/days"
      risk: "Low/Medium/High"
```

---

### Customization Examples

Organizations can define:
- Custom fix patterns
- Organization-specific code examples
- Custom effort estimates
- Custom risk assessments
- Custom implementation templates
- Custom testing strategies

### Output

Generated based on:
1. Custom architecture configuration
2. Detected violations
3. Organization templates
4. Previous similar fixes
5. Industry best practices

Each suggestion tailored to organization's specific architecture and patterns.

---

## PR Review Automation

### Dynamic Review Generation

PR reviews are generated based on custom architecture configuration.

### Review Comment Types (Customizable)

#### 🚨 Critical Violations
As configured in architecture.yaml

```yaml
critical_rules:
  - rule_name: "CUSTOM_LAYER_BOUNDARY"
    description: "[Organization-specific description]"
    violations_block_merge: true
    comment_template: "custom_templates/critical_boundary.md"
```

#### ⚠️ Major Issues
As configured

```yaml
major_rules:
  - rule_name: "CUSTOM_DEPENDENCY_RULE"
    violations_request_changes: true
```

#### 💡 Suggestions
As configured

#### ✅ Positive Patterns
As configured

---

### Configuration Template

```yaml
pr_review:
  enabled: true
  custom_rules: true
  
  comment_templates:
    critical: "templates/critical_violation.md"
    major: "templates/major_issue.md"
    suggestion: "templates/improvement.md"
    praise: "templates/good_pattern.md"
  
  metrics_to_track:
    - custom_metric_1
    - custom_metric_2
  
  thresholds:
    custom_threshold_1: value
    custom_threshold_2: value
  
  business_rules_validation: true
  adr_consistency_check: true
```

---

### Organization-Specific Features

- **Custom Rule Violations**: Detect org-specific architectural violations
- **Metrics Tracking**: Monitor custom metrics over time
- **Business Logic**: Validate organization-specific patterns
- **ADR Compliance**: Ensure Architectural Decision Records are followed
- **Custom Templates**: Use org-specific comment formats
- **Trend Analysis**: Track architecture health trends

---

### Output

PR comments include:
- Custom violation description
- Custom templates
- Organization-specific guidance
- Custom metrics impact
- Links to organization documentation
- Custom remediation steps
