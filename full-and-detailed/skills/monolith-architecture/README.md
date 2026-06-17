# Monolith Architecture Analysis & Guidance

## Table of Contents
1. [Analysis & Detection](#analysis--detection)
2. [Scoring & Assessment](#scoring--assessment)
3. [Fix Suggestions](#fix-suggestions)
4. [PR Review Automation](#pr-review-automation)

---

## Analysis & Detection

### Purpose
Detects monolith code organization issues including layer violations, god classes, high complexity, and testability barriers.

### Analysis Phases

#### Phase 1: Layer Structure Analysis
```
1. Scan codebase structure
2. Identify logical layers
3. Map namespaces to layers
4. Classify classes by layer
5. Detect layer violations
```

#### Phase 2: Class Organization Assessment
```
1. Analyze class count and distribution
2. Identify god classes
3. Calculate class complexity metrics
4. Assess cohesion per class
5. Detect orphaned classes
```

#### Phase 3: Method Quality Analysis
```
1. Calculate cyclomatic complexity
2. Measure method length
3. Assess parameter count
4. Identify complex methods
5. Detect code duplication
```

#### Phase 4: Separation of Concerns
```
1. Detect business logic in wrong layers
2. Identify scattered concerns
3. Analyze logging placement
4. Check exception handling strategy
5. Verify configuration externalization
```

#### Phase 5: Modernization Assessment
```
1. Identify modularization candidates
2. Assess microservices extraction potential
3. Evaluate technical debt concentration
4. Check test coverage per area
5. Identify refactoring priorities
```

### Violation Detection Rules

- **BUSINESS_LOGIC_IN_CONTROLLER**: Business logic in presentation layer (CRITICAL)
- **GOD_CLASS**: Class with too many responsibilities (MAJOR) - >15 methods OR >500 LOC OR CC > 20
- **LAYER_VIOLATION**: Dependencies not following layer order (MAJOR)
- **HIGH_METHOD_COMPLEXITY**: Method too complex to understand/test (MAJOR) - CC > 10 OR LOC > 20
- **CIRCULAR_DEPENDENCY**: Classes depend on each other (MAJOR)
- **HARDCODED_VALUES**: Configuration hardcoded instead of externalized (MODERATE)
- **SCATTERED_CONCERNS**: Cross-cutting concerns scattered throughout (MODERATE)

### Key Metrics

- **Layer Violations**: Count and severity
- **Average Class Size**: Methods and LOC
- **Average Method Complexity**: Cyclomatic complexity
- **God Classes**: Classes exceeding thresholds
- **Cyclic Dependencies**: Count and depth
- **Unused Classes**: Dead code percentage
- **Testing Barriers**: Testability assessment

---

## Scoring & Assessment

### Purpose
Computes comprehensive monolith health scores across 12 dimensions.

### Scoring Dimensions

#### 1. Layer Separation (13%)
Clear layers, proper dependencies
- Layer violations: -15 pts
- Bidirectional dependencies: -12 pts
- Unclear layers: -8 pts

#### 2. Coupling Balance (13%)
Low coupling, minimal dependencies
- High coupling: -10 pts
- Circular dependencies: -15 pts
- Tight coupling: -10 pts

#### 3. Class Organization (12%)
Logical grouping, clear purposes
- Miscategorized classes: -8 pts
- Poor organization: -8 pts
- Orphaned classes: -8 pts

#### 4. Method Quality (11%)
Reasonable sizes, clear names, low complexity
- High complexity methods: -8 pts
- Large methods: -8 pts
- Unclear names: -5 pts

#### 5. Code Organization (10%)
Namespace hierarchy, folder structure
- Poor structure: -8 pts
- Inconsistent organization: -8 pts
- Deep nesting: -5 pts

#### 6. Cohesion (9%)
Classes focused, high internal coherence
- Low cohesion: -8 pts
- God classes: -15 pts
- Mixed concerns: -8 pts

#### 7. Configuration Mgmt (8%)
Externalized, environment-specific
- Hardcoded values: -10 pts
- Embedded config: -8 pts

#### 8. Exception Handling (7%)
Consistent, appropriate catching
- Swallowed exceptions: -8 pts
- Inconsistent handling: -5 pts

#### 9. Logging (6%)
Proper placement, non-intrusive
- Business logic in logs: -5 pts
- Missing logging: -8 pts

#### 10-12. (Testing/Naming/Docs)

### Score Interpretation

| Score | Grade | Status | Action |
|-------|-------|--------|--------|
| 90-100 | A | Excellent | Maintain |
| 75-89 | B | Good | Minor improvements |
| 60-74 | C | Fair | Plan refactoring |
| 40-59 | D | Poor | Significant work |
| 0-39 | F | Critical | Emergency |

---

## Fix Suggestions

### Priority 1: Critical (1-3 days)

#### 1. Extract Business Logic from Controllers
**Pattern**: Complex logic in controllers
**Fix**: Create application services/use cases
**Effort**: 1-2 days

#### 2. Break Up God Classes
**Pattern**: Classes > 500 LOC or > 15 methods
**Fix**: Split into focused, single-responsibility classes
**Effort**: 1-2 days per god class

#### 3. Resolve Layer Violations
**Pattern**: Direct layer boundary crossing
**Fix**: Route through intermediate layer
**Effort**: 4-8 hours

---

### Priority 2: Major Issues (3-7 days)

#### 4. Reduce Method Complexity
**Pattern**: CC > 10 or LOC > 20
**Fix**: Extract smaller methods, simplify logic
**Effort**: 1-2 days

#### 5. Eliminate Circular Dependencies
**Pattern**: Classes depend on each other
**Fix**: Extract shared class or refactor
**Effort**: 4-8 hours

#### 6. Externalize Configuration
**Pattern**: Hardcoded values
**Fix**: Move to config files, environment variables
**Effort**: 1-2 days

---

### Priority 3: Modernization (2-4 weeks)

#### 7. Modularize Monolith
**Pattern**: Single large project
**Fix**: Split into modules by business capability
**Effort**: 2-4 weeks

---

## PR Review Automation

### Review Focus

PR reviews validate:
- Layer boundary violations
- God class additions
- Method complexity growth
- Business logic in wrong layers
- Circular dependencies
- Configuration management

### Comment Types

#### 🚨 Critical: Layer Violation
```markdown
## Layer Boundary Violation

Your Controller directly accesses Database (skipping Repository layer)
**Location**: OrderController.cs, line 45
**Impact**: Difficult to test, violates layering principle
**Fix**: Use injected IOrderRepository
```

#### ⚠️ Major: God Class Alert
```markdown
## God Class Growing

UserService now has 22 methods and 800 LOC
- Previous score: 45/100
- Current score: 35/100
**Fix**: Split into UserCreationService, UserAuthService, etc.
```

#### 💡 Method Complexity
```markdown
## Method Complexity High

ProcessOrder() has cyclomatic complexity of 15
**Consider**: Extract nested conditions into separate methods
**Effort**: 2-3 hours
```

#### ✅ Good Layering
```markdown
## Excellent Layering!

- Clear separation of concerns ✓
- Repository pattern used correctly ✓
- Thin controller, rich domain ✓
- High testability ✓
```

---

### Configuration

```yaml
pr_review:
  enabled: true
  check_layer_violations: true
  detect_god_classes: true
  max_class_lines: 500
  max_class_methods: 15
  max_method_complexity: 10
  check_circular_deps: true
  check_config_hardcoding: true
```
