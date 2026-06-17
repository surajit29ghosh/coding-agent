---
name: application-review
description: Quick application architecture and style review
---
# application-review
```md
# Architecture Review (Deep)

# Architecture Style Detection

Analyze repository structure to determine the dominant architecture pattern:

**Detection Criteria:**
- Folder structure and organization
- Project boundaries and dependencies
- Service/module isolation
- Database access patterns
- Deployment configuration
- Communication patterns (sync/async)

**Supported Architecture Styles:**
- `clean-architecture` - Domain/Application/Infrastructure layers
- `layered` - Presentation/Business/Data layers
- `component` - Encapsulated components with interfaces
- `microservices` - Distributed services with APIs/events
- `modular-monolith` - Internal modules with clear boundaries
- `custom-layered` - Plugin/Processor/ApiClient/Helper flow


## Layer Enforcement
- layers should be strictly followed based on detected architecture style
- No business logic leakage into controllers
- No direct DbContext usage outside repositories

## Dependency Direction
- Dependencies flow inward only
- No circular dependencies

## Abstractions
- Interfaces used at boundaries
- Avoid over-abstraction (YAGNI violations)

## Domain Integrity
- Business rules centralized in service/domain layer
- Avoid anemic domain model (logic not just DTOs)

## Anti-Patterns
- God services
- Service-to-service tight coupling
- Repository returning IQueryable to upper layers
```
