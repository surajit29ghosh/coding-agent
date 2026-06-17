# Component Architecture Analysis & Guidance

## Table of Contents
1. [Analysis & Detection](#analysis--detection)
2. [Scoring & Assessment](#scoring--assessment)
3. [Fix Suggestions](#fix-suggestions)
4. [PR Review Automation](#pr-review-automation)

---

## Analysis & Detection

### Purpose
Detects component architecture deviations including boundary violations, excessive coupling, encapsulation breaches, and reusability issues.

### Analysis Phases

#### Phase 1: Component Discovery
```
1. Scan project structure
2. Identify components (by project/namespace/package)
3. Classify component types
4. Map component boundaries
5. Document component purposes
```

#### Phase 2: Boundary Validation
```
1. Extract public API per component
2. Identify internal packages
3. Detect encapsulation breaches
4. Validate visibility rules
5. Check API contracts
```

#### Phase 3: Coupling Analysis
```
1. Build component dependency graph
2. Calculate coupling metrics (Ce, Ca, I)
3. Detect circular dependencies
4. Analyze transitive chains
5. Assess stability matrix
```

#### Phase 4: Communication Pattern Analysis
```
1. Identify sync vs async calls
2. Detect event patterns
3. Validate messaging contracts
4. Check integration points
5. Assess API versioning
```

#### Phase 5: Reusability Assessment
```
1. Check deployment independence
2. Validate composability
3. Assess testability
4. Identify pluggable points
5. Evaluate framework coupling
```

### Violation Detection Rules

- **BOUNDARY_VIOLATION**: Direct access to internal component members (CRITICAL)
- **CIRCULAR_DEPENDENCY**: Component A → B → A (CRITICAL)
- **EXCESSIVE_COUPLING**: Ce > max_efferent OR Ca > max_afferent (MAJOR)
- **UNSTABLE_COMPONENT**: I = Ce / (Ce + Ca) > 0.7 (MAJOR)
- **MISSING_ABSTRACTION**: Multiple similar implementations (MODERATE)
- **ENCAPSULATION_BREACH**: Public exposure of internal classes (MODERATE)
- **VERSION_INCOMPATIBILITY**: Breaking API changes without major version (MODERATE)

### Key Metrics

- **Efferent Coupling (Ce)**: Outbound component dependencies
- **Afferent Coupling (Ca)**: Inbound component dependencies
- **Instability (I)**: Ce / (Ce + Ca)
- **Abstractness (A)**: Abstract types / Total types
- **Distance (D)**: |A + I - 1|
- **Component Count**: Total in solution
- **Coupling Ratio**: Average coupling per component
- **Reusability Index**: Independently deployable components / Total

---

## Scoring & Assessment

### Purpose
Computes comprehensive component architecture health scores across 10 weighted dimensions.

### Scoring Dimensions (10 Categories)

#### 1. Component Cohesion (15%)
Measures: Related functionality grouping, single purpose, no fragmentation
- Fragmented features: -10 pts each
- Redundant functionality: -5 pts each

#### 2. Coupling Balance (15%)
Measures: Low coupling, stable abstractions, dependency direction
- Instability > 0.7: -15 pts each
- High coupling (Ce > max): -10 pts
- Reverse dependencies: -20 pts

#### 3. Acyclic Dependencies (12%)
Measures: No circular dependencies, clear ordering
- Each circular dependency: -20 pts
- Each transitive chain: -5 pts

#### 4. API Stability (12%)
Measures: Interface stability, versioning, backward compatibility
- Breaking changes without major version: -15 pts
- Unversioned APIs: -8 pts

#### 5. Communication Patterns (10%)
Measures: Proper async/sync choices, contract-based
- Over-reliance on sync: -10 pts
- Undocumented contracts: -8 pts

#### 6. Encapsulation (10%)
Measures: Hidden implementation, clear public interface
- Each public internal class: -15 pts
- Leaked implementation details: -8 pts

#### 7. Reusability (10%)
Measures: Independent deployment, composability
- Deployment dependencies: -12 pts
- Framework coupling: -10 pts

#### 8. Documentation (8%)
Measures: API docs, component purpose, integration guide
- Missing documentation: -8 pts
- Unclear component purpose: -5 pts

#### 9. Naming Consistency (5%)
Measures: Clear, descriptive names, consistency
- Poor naming: -3 pts each
- Inconsistent patterns: -2 pts

#### 10. Testing Support (3%)
Measures: Mockability, integration test support
- Hard dependencies: -8 pts
- Untestable patterns: -10 pts

### Overall Score Calculation

```
OverallScore = Σ(CategoryScore[i] × Weight[i])
Range: 0-100
```

### Score Interpretation

| Score | Grade | Status | Action |
|-------|-------|--------|--------|
| 90-100 | A | Excellent | Maintain, document patterns |
| 75-89 | B | Good | Address minor issues |
| 60-74 | C | Fair | Plan refactoring |
| 40-59 | D | Poor | Prioritize improvements |
| 0-39 | F | Critical | Emergency intervention |

---

## Fix Suggestions

### Priority 1: Critical Violations (0-2 days)

#### 1. Resolve Circular Component Dependencies
**Pattern**: Component A ↔ Component B
**Fix**: Extract shared abstraction to shared component
**Effort**: 2-4 hours

#### 2. Fix Encapsulation Breaches
**Pattern**: Direct access to internal component members
**Fix**: Route through public component interface
**Effort**: 1-3 hours per breach

---

### Priority 2: Major Issues (1-2 days)

#### 3. Reduce Excessive Coupling
**Pattern**: Component has Ce > max_efferent
**Fix**:
- Extract new component
- Create shared abstractions
- Use events instead of direct calls
**Effort**: 4-8 hours

#### 4. Improve Component Stability
**Pattern**: Instability I > 0.7
**Fix**:
- Make component more abstract
- Have higher-level components depend on it
- Move stable parts to lower level
**Effort**: 4-8 hours

---

### Priority 3: Moderate Issues (2-5 days)

#### 5. Add Missing Abstractions
**Pattern**: Multiple implementations without interface
**Fix**: Extract common interface, create abstraction layer
**Effort**: 2-4 hours

#### 6. Improve Component Versioning
**Pattern**: No versioning strategy
**Fix**: Implement semantic versioning, deprecation paths
**Effort**: 1-2 days

---

### Effort Summary

- Total Estimated: 10-20 days
- Quick Wins: 2-3 days
- Medium Work: 5-10 days
- Long Term: 5-10 days

---

## PR Review Automation

### Review Focus

PR reviews validate:
- Component boundary violations
- New circular dependencies
- Encapsulation breaches
- API contract changes
- Communication pattern issues
- Positive pattern usage

### Comment Types

#### 🚨 Critical Violation Alert
```markdown
## Circular Component Dependency Detected

**Components**: ComponentA → ComponentB → ComponentA
**Impact**: Testing, deployment complexity
**Severity**: CRITICAL
**Fix**: Extract shared abstraction
```

#### ⚠️ Major Issue Warning
```markdown
## Encapsulation Breach

**Component**: UIComponent accessing Infrastructure internals
**Line**: 45
**Fix**: Use public API from shared component
```

#### 💡 Improvement Suggestion
```markdown
## Component Coupling Issue

Your component has 8 outbound dependencies (Ce=8).
Consider extracting smaller components.
**Estimated Effort**: 2-4 days
```

#### ✅ Good Pattern
```markdown
## Great Component Design!

- Clear boundary ✓
- Low coupling (Ce=2) ✓
- Well-versioned API ✓
- Excellent example!
```

---

### Configuration

```yaml
pr_review:
  enabled: true
  
  block_on:
    - CIRCULAR_DEPENDENCY
    - REVERSE_DEPENDENCY
    - CRITICAL_ENCAPSULATION_BREACH
  
  request_changes_on:
    - EXCESSIVE_COUPLING
    - MAJOR_BOUNDARY_VIOLATION
```
