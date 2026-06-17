# Clean Architecture Analysis & Guidance

## Table of Contents
1. [Analysis & Detection](#analysis--detection)
2. [Scoring & Assessment](#scoring--assessment)
3. [Fix Suggestions](#fix-suggestions)
4. [PR Review Automation](#pr-review-automation)

---

## Analysis & Detection

### Purpose
Comprehensive static analysis of .NET solutions to identify architectural deviations from Clean Architecture principles.

### Execution

The analyzer performs a multi-phase scan:

#### Phase 1: Project Structure Mapping
```
1. Enumerate all projects in solution
2. Classify projects into layers based on:
   - Project naming patterns
   - Namespace hierarchies
   - Project dependencies
3. Identify missing layers or misconfigured projects
4. Generate project topology map
```

#### Phase 2: Dependency Analysis
```
1. Parse project files (.csproj)
2. Extract direct project references
3. Build dependency graph
4. Detect cycles (circular dependencies)
5. Validate dependency direction (inward)
6. Map transitive dependencies
7. Categorize NuGet packages by layer
```

#### Phase 3: Code Pattern Detection
```
For each source file in each layer:
  1. Parse C# syntax tree
  2. Identify class declarations
  3. Detect patterns:
     - Entity/ValueObject indicators
     - Repository implementations
     - Service/Interactor patterns
     - Controller/Presenter classes
     - DTO patterns
     - Interface definitions
  4. Analyze method bodies for violations:
     - Direct database access in wrong layer
     - Business logic in controller
     - Infrastructure concern in domain
     - Framework dependency in business logic
```

#### Phase 4: DDD Pattern Recognition
```
1. Aggregate identification:
   - Root entity detection
   - Aggregate boundary analysis
   - Child entity relationships
   
2. Bounded Context mapping:
   - Namespace analysis
   - Cross-context communication patterns
   - Anti-corruption layer detection
   
3. Domain Event patterns:
   - Event class detection
   - Event handler identification
   - Event sourcing patterns
   
4. Repository boundaries:
   - Repository per aggregate validation
   - Query abstraction analysis
   - Specification pattern detection
```

#### Phase 5: Architecture Violation Detection

##### Critical Violations
- **Circular Dependencies**: Project A → B → A
- **Reverse Layer Dependencies**: Infrastructure → Domain
- **Framework in Domain**: Direct use of EF Core, ASP.NET in domain layer
- **Business Logic in Controller**: Complex calculations in controller methods
- **Direct Entity Exposure**: Returning entities instead of DTOs across layers

##### Major Violations
- **Service Locator Pattern**: ServiceLocator usage in domain/application
- **Static Class Dependencies**: Hard dependencies on static classes
- **Tight Controller Coupling**: Controllers directly calling data layer
- **Missing Abstraction**: Infrastructure directly exposed to presentation
- **DTO Inconsistency**: Entity returned across boundaries

##### Moderate Violations
- **Repository Anti-Pattern**: Repository for each entity instead of aggregates
- **Interface Segregation**: Fat interfaces forcing multiple implementations
- **Transaction Boundaries**: Improper Unit of Work usage
- **Naming Inconsistency**: Violations of layer naming conventions
- **Missing Abstractions**: Multiple implementations without interface

##### Minor Violations
- **Documentation Gaps**: Missing XML comments on public types
- **Inconsistent Patterns**: Mixed use of patterns in similar code
- **Unused Dependencies**: NuGet packages not utilized
- **Code Organization**: Miscategorized classes in layer

### Violation Detection Rules

#### Rule: LAYER_VIOLATION
```
Detects when class in Layer X directly references non-abstracted type from Layer Y
Where LayerOrder[X] > LayerOrder[Y] (violates inward dependency)
```

#### Rule: CIRCULAR_DEPENDENCY
```
Detects cycles in project dependency graph using DFS
Reports all projects involved in cycle
Suggests merge or abstraction extraction point
```

#### Rule: FRAMEWORK_LEAKAGE
```
Detects direct usage of framework in domain layer:
- DbContext, DbSet (Entity Framework)
- ControllerBase, ActionResult (ASP.NET)
- ILogger (Logging frameworks)
- HttpClient (HTTP frameworks)
Suggests abstraction pattern and location
```

#### Rule: ENTITY_LEAKAGE
```
Detects domain entity returned across layer boundary:
- Entity in API response model
- Entity in repository interface return type
- Entity in application service return type
Suggests DTO creation and mapping
```

#### Rule: BUSINESS_LOGIC_IN_CONTROLLER
```
Detects complex logic in controller methods:
- Loops with computations
- Conditional logic beyond routing
- Data transformations
- Service orchestration
Suggests extraction to application service/interactor
```

#### Rule: REPOSITORY_ANTI_PATTERN
```
Detects repository per entity instead of per aggregate:
- High number of repositories for single bounded context
- Entity repositories (not aggregate roots)
- Repos with identical interface patterns
Suggests aggregation of related repositories
```

#### Rule: MISSING_ABSTRACTION
```
Detects multiple implementations of similar patterns:
- Multiple repositories with similar logic
- Multiple services implementing same functionality
- Duplicated validation logic
Suggests common interface and abstraction
```

#### Rule: INTERFACE_SEGREGATION
```
Detects fat interfaces causing artificial dependencies:
- Interfaces with > 5 methods (threshold)
- Clients implementing unused interface members
- Unrelated methods in same interface
Suggests splitting into smaller, focused interfaces
```

#### Rule: SERVICE_LOCATOR_PATTERN
```
Detects service locator anti-pattern:
- Direct ServiceProvider.GetService calls
- Manual dependency resolution
- Use of service locator containers
Suggests proper dependency injection
```

#### Rule: TIGHT_COUPLING
```
Detects static dependencies and tight coupling:
- new keyword for dependencies in business logic
- Static method calls to services
- Direct instantiation of complex types
Suggests constructor or property injection
```

#### Rule: MISSING_DDD_PATTERNS
```
Detects missing DDD patterns:
- ValueObject candidates not using immutability
- Aggregate boundaries not enforced
- Domain events not published
- Repository not following aggregate pattern
```

---

## Scoring & Assessment

### Purpose
Computes comprehensive, multi-dimensional health scores for Clean Architecture conformity across 12 weighted categories.

### Scoring Philosophy

The scorer uses a **holistic, weighted approach** that:
- Recognizes that different aspects have different criticality
- Rewards clean architecture adoption patterns
- Penalizes violations based on severity and frequency
- Tracks trends over time for improvement visibility
- Provides actionable feedback on improvement areas

### Scoring Dimensions (12 Categories)

#### 1. Layer Isolation (Weight: 15%)
**Assesses**: Proper separation between layers with minimal cross-cutting

**Calculation**:
```
Layer_Isolation_Score = 100 - (Layer_Violations / Total_Dependencies × 100)

Where:
- Layer_Violations = Direct cross-layer references bypassing abstraction
- Total_Dependencies = All project dependencies
```

**Indicators**:
- ✅ Dependencies flow strictly inward
- ✅ No bidirectional dependencies
- ✅ Clear abstraction boundaries
- ✅ Presentation never references Infrastructure directly
- ✅ Domain never references outer layers

#### 2. Dependency Flow (Weight: 15%)
**Assesses**: Correctness of dependency direction and cycle-free dependency graph

**Calculation**:
```
Dependency_Flow_Score = (Valid_Dependencies / Total_Dependencies) × 100
                       - (Circular_Cycles × 10)
                       - (Reverse_Dependencies × 5)

Floor: 0, Ceiling: 100
```

**Indicators**:
- ✅ No circular dependencies
- ✅ All dependencies flow inward
- ✅ Framework dependencies isolated to Infrastructure
- ✅ NuGet packages appropriately layered

#### 3. Domain Purity (Weight: 12%)
**Assesses**: Domain layer independence from infrastructure concerns

**Indicators**:
- ✅ Domain entities have no framework attributes
- ✅ No EntityFramework, ASP.NET, or logging framework imports
- ✅ Domain logic encapsulated in entities/value objects
- ✅ No database-specific patterns in domain
- ✅ Rich business logic concentrated in domain

#### 4. Use Case Pattern (Weight: 12%)
**Assesses**: Proper implementation of use cases/interactors with clear input/output ports

**Indicators**:
- ✅ One use case per class principle
- ✅ Input ports defined as interfaces
- ✅ Output ports (presenters) implemented
- ✅ Controllers delegate to use cases
- ✅ Command/Query separation (CQRS ready)

#### 5. Interface Quality (Weight: 10%)
**Assesses**: Interface Segregation Principle (ISP) adherence and abstraction quality

**Indicators**:
- ✅ Focused interfaces (avg 3-4 methods)
- ✅ No fat/god interfaces
- ✅ Multiple implementations have common interface
- ✅ Clients depend on small, focused interfaces
- ✅ Clear abstraction hierarchies

#### 6. Abstraction Levels (Weight: 8%)
**Assesses**: Proper use of abstractions, interfaces, and polymorphism

**Indicators**:
- ✅ Multiple abstraction layers for complex domains
- ✅ Dependency inversion properly applied
- ✅ Abstract base classes used appropriately
- ✅ No leaky abstractions

#### 7. Repository Pattern (Weight: 8%)
**Assesses**: Proper repository implementation per aggregate

**Indicators**:
- ✅ Repository per aggregate root
- ✅ Repositories abstract data access
- ✅ Query abstraction via specifications
- ✅ No entity-specific repositories

#### 8. DTOs & Mapping (Weight: 7%)
**Assesses**: Data Transfer Objects and mapping strategies

**Indicators**:
- ✅ DTOs separate from domain entities
- ✅ Consistent mapping strategy
- ✅ API models distinct from internal models
- ✅ Proper cross-boundary mapping

#### 9. Testing Support (Weight: 5%)
**Assesses**: Design supports unit and integration testing

**Indicators**:
- ✅ Mock-friendly design
- ✅ Dependency injection enabling test doubles
- ✅ Testable business logic
- ✅ Clear test boundaries

#### 10. Code Distribution (Weight: 5%)
**Assesses**: Proper distribution across layers

**Indicators**:
- ✅ Domain layer has business logic (40-50%)
- ✅ Infrastructure layer isolated (15-20%)
- ✅ No code duplication across layers
- ✅ Balanced distribution

#### 11. Naming Conventions (Weight: 3%)
**Assesses**: Consistent, meaningful naming

**Indicators**:
- ✅ Layer naming clear and consistent
- ✅ Domain terms properly reflected
- ✅ Service/Repository naming patterns clear

#### 12. Documentation (Weight: 4%)
**Assesses**: Architecture documentation and guidance

**Indicators**:
- ✅ Clear layer responsibilities documented
- ✅ Architecture decision records (ADRs)
- ✅ Pattern usage guidelines
- ✅ Onboarding documentation

### Overall Score Calculation

```
OverallScore = Σ(CategoryScore[i] × Weight[i])

Where CategoryScore ranges 0-100
Final Score ranges 0-100
```

### Score Interpretation

| Score | Grade | Status | Action |
|-------|-------|--------|--------|
| 90-100 | A | Excellent | Maintain, document patterns |
| 75-89 | B | Good | Address minor issues |
| 60-74 | C | Fair | Plan refactoring |
| 40-59 | D | Poor | Prioritize improvements |
| 0-39 | F | Critical | Emergency intervention |

### Output: clean_architecture_score.json

```json
{
  "overall_score": 78,
  "grade": "B",
  "status": "Good - Minor coupling issues, minor DDD gaps",
  "category_scores": {
    "layer_isolation": 82,
    "dependency_flow": 85,
    "domain_purity": 75,
    "use_case_pattern": 72,
    "interface_quality": 78,
    "abstraction_levels": 76,
    "repository_pattern": 74,
    "dtos_mapping": 80,
    "testing_support": 70,
    "code_distribution": 80,
    "naming_conventions": 85,
    "documentation": 72
  },
  "metrics": {
    "layer_violations": 3,
    "circular_dependencies": 0,
    "ddd_patterns_adopted": 0.85,
    "test_coverage": 0.68
  },
  "trend_analysis": {
    "previous_score": 75,
    "improvement": 3,
    "trend": "improving"
  }
}
```

---

## Fix Suggestions

### Priority Classification

#### Priority 1: CRITICAL (Implement First)
- Circular dependencies blocking deployments
- Framework leakage compromising domain purity
- Business logic scattered across layers
- Reverse dependencies causing maintenance issues
- **Estimated Effort**: 1-3 days per issue

#### Priority 2: MAJOR (Implement Soon)
- Missing abstractions causing tight coupling
- Entity leakage across boundaries
- Repository anti-pattern violations
- Service locator patterns
- **Estimated Effort**: 3-7 days per issue

#### Priority 3: MODERATE (Schedule Next)
- Interface segregation violations
- Code distribution imbalances
- Missing DDD patterns
- Documentation gaps
- **Estimated Effort**: 1-3 days per issue

#### Priority 4: MINOR (Continuous Improvement)
- Naming convention inconsistencies
- Code organization improvements
- Documentation enhancements
- **Estimated Effort**: 2-8 hours per issue

### Suggestion Categories

#### Category 1: Circular Dependency Resolution

**Issue**: Projects or modules form circular dependency cycles

**Before Code**:
```csharp
// MyApp.Application/Services/UserService.cs
using MyApp.Infrastructure.Repositories;

public class UserService
{
    private readonly UserRepository _repo;
}

// MyApp.Infrastructure/Repositories/UserRepository.cs
using MyApp.Application.Services;

public class UserRepository
{
    public void LogActivity(UserService service) { }
}
```

**Fix: Extract Abstraction**

**After Code**:
```csharp
// MyApp.Application/Interfaces/IUserRepository.cs
public interface IUserRepository
{
    Task<User> GetByIdAsync(int id);
    Task AddAsync(User user);
}

// MyApp.Application/Services/UserService.cs
public class UserService
{
    private readonly IUserRepository _repo;
    public UserService(IUserRepository repo) => _repo = repo;
}

// MyApp.Infrastructure/Repositories/UserRepository.cs
public class UserRepository : IUserRepository
{
    public async Task<User> GetByIdAsync(int id) { /* ... */ }
    public async Task AddAsync(User user) { /* ... */ }
}
```

**Implementation Steps**:
1. Create interface in Application layer (`IUserRepository`)
2. Make Infrastructure Repository implement interface
3. Inject interface in Application services
4. Remove direct Infrastructure references from Application
5. Verify no circular references remain

**Effort**: 2-4 hours | **Risk**: Low - Interface extraction is safe refactoring

---

#### Category 2: Framework Leakage Elimination

**Issue**: Framework-specific code mixed into domain layer

**Before Code**:
```csharp
// MyApp.Domain/Entities/Order.cs
using Microsoft.EntityFrameworkCore;
using System.ComponentModel.DataAnnotations;

[Table("Orders")]
[Index(nameof(CustomerId))]
public class Order
{
    [Key]
    public int Id { get; set; }

    [Required]
    [MaxLength(200)]
    public string Description { get; set; }
}
```

**Fix: Move Mapping to Infrastructure**

**After Code**:
```csharp
// MyApp.Domain/Entities/Order.cs
public class Order
{
    public int Id { get; set; }
    public string Description { get; set; }
}

// MyApp.Infrastructure/Data/Configurations/OrderConfiguration.cs
public class OrderConfiguration : IEntityTypeConfiguration<Order>
{
    public void Configure(EntityTypeBuilder<Order> builder)
    {
        builder.ToTable("Orders");
        builder.HasKey(x => x.Id);
        builder.Property(x => x.Description)
            .IsRequired()
            .HasMaxLength(200);
    }
}
```

**Effort**: 3-6 hours per entity

---

#### Category 3: Entity Leakage Prevention

**Fix**: Always return DTOs across boundaries

**Before**: `public Product GetProduct(int id) => _repo.Get(id);`

**After**:
```csharp
public ProductDto GetProduct(int id)
{
    var product = _repo.Get(id);
    return _mapper.Map<ProductDto>(product);
}
```

---

#### Category 4: Use Case Pattern Implementation

**Fix**: Extract business logic into use cases

**Pattern**:
```csharp
public interface ICreateUserInputPort
{
    void Execute(CreateUserRequest request);
}

public class CreateUserUseCase : ICreateUserInputPort
{
    public void Execute(CreateUserRequest request) { }
}
```

---

#### Category 5: Repository Pattern Correction

**Fix**: Repository per aggregate, not per entity

---

#### Category 6: Interface Segregation

**Fix**: Split fat interfaces into focused ones

**Before**: `IUserService` with 10 methods
**After**: `ICreateUserService`, `IUpdateUserService`, `IDeleteUserService`

---

### Effort Summary

- Total Time: 10-20 days
- Quick Wins: 2-3 days
- Medium Work: 5-10 days
- Long Term: 5-10 days

---

## PR Review Automation

### Purpose
Automatically reviews pull requests for architectural conformance, posts intelligent comments with violations and suggestions, tracks architecture score trends, and enforces architectural standards in CI/CD.

### Review Strategy

PR review automation performs:

1. **Scope Analysis**: Identifies changed files and affected layers
2. **Baseline Comparison**: Compares current architecture against baseline
3. **Violation Detection**: Identifies new violations introduced by PR
4. **Pattern Recognition**: Detects architecture-positive changes
5. **Score Impact**: Calculates impact on overall architecture score
6. **Feedback Generation**: Creates targeted, helpful review comments
7. **Enforcement**: Can block PR if critical violations detected

### PR Analysis Pipeline

```
Pull Request Created/Updated
        ↓
Fetch Changed Files
        ↓
Classify Changes by Layer
        ↓
Analyze Each File
        ├─ Check dependencies
        ├─ Check code patterns
        ├─ Check layer boundaries
        └─ Check for violations
        ↓
Compare Against Baseline
        ├─ New violations?
        ├─ New good patterns?
        └─ Score impact?
        ↓
Generate Review Comments
        ├─ Critical issues
        ├─ Major violations
        ├─ Moderate concerns
        └─ Positive reinforcement
        ↓
Post PR Comments & Status Check
```

### Review Comment Types

#### Type 1: Critical Violation Alert

**Trigger**: New circular dependency, reverse dependency, or framework leakage

**Template**:
```markdown
## 🚨 Critical Architecture Violation Detected

**Issue**: Circular dependency introduced
**File**: `src/Application/Services/UserService.cs`
**Line**: 23
**Code**: `using MyApp.Infrastructure.Repositories;`

### Problem
This creates a circular dependency:
- Application → Infrastructure (new)
- Infrastructure → Application (existing)

This violates Clean Architecture and prevents unit testing.

### Suggested Fix
1. Move repository interface to Application layer
2. Keep repository implementation in Infrastructure
3. Inject interface, not concrete implementation
```

---

#### Type 2: Major Issue Warning

**Trigger**: Entity leakage, framework in domain, business logic in controller

**Template**:
```markdown
## ⚠️ Major Architectural Issue

**Issue**: Domain entity returned directly in API response
**File**: `src/API/Controllers/ProductController.cs`
**Line**: 45

### Problem
Returning domain `Product` entity directly in API response:
- Exposes internal implementation to clients
- Prevents API evolution
- Violates DTO boundary pattern

### Suggested Fix
1. Create `ProductDto` in Application layer
2. Map `Product` → `ProductDto` in controller
3. Return `ProductDto` in API response
```

---

#### Type 3: Moderate Improvement Suggestion

**Trigger**: Interface segregation, missing abstractions, pattern inconsistencies

**Template**:
```markdown
## 💡 Architectural Improvement Opportunity

**Suggestion**: Interface segregation
**File**: `src/Application/Interfaces/IProductService.cs`

The `IProductService` interface has 8 methods with mixed responsibilities.
Consider splitting into focused interfaces.

**Effort**: 4-6 hours
```

---

#### Type 4: Pattern Recognition & Praise

**Trigger**: Good architecture patterns detected

**Template**:
```markdown
## ✅ Great Architecture Pattern!

**File**: `src/Application/UseCases/CreateUser/CreateUserUseCase.cs`

Excellent implementation:
- ✅ Single responsibility
- ✅ Clear input/output ports
- ✅ No framework dependencies
- ✅ Proper dependency injection
- ✅ Testable design

Great example for the team!
```

---

#### Type 5: DDD Pattern Recognition

**Trigger**: Good DDD pattern usage detected

**Template**:
```markdown
## 📚 Good Domain-Driven Design Pattern

**File**: `src/Domain/Aggregates/Order/Order.cs`

Well-implemented DDD patterns:
- ✅ Aggregate root with child entities
- ✅ Value object for Address
- ✅ Private setters enforcing invariants
- ✅ Factory method for creation
- ✅ Rich domain logic

Consider publishing domain events for order status changes.
```

### Configuration

```yaml
pr_review:
  enabled: true
  
  block_on:
    - CIRCULAR_DEPENDENCY
    - REVERSE_DEPENDENCY
    - CRITICAL_FRAMEWORK_IN_DOMAIN
  
  request_changes_on:
    - ENTITY_LEAKAGE
    - BUSINESS_LOGIC_IN_CONTROLLER
    - SERVICE_LOCATOR_PATTERN
  
  comment_on:
    - INTERFACE_SEGREGATION
    - MISSING_ABSTRACTIONS
    - REPOSITORY_ANTI_PATTERN
  
  praise:
    enabled: true
    patterns:
      - proper_use_case_pattern
      - good_ddd_patterns
      - proper_dto_usage
```

### Output

Posted comments include:
- Violation description
- Code location with snippet
- Impact assessment
- Suggested fix
- Links to documentation
- Examples from codebase
