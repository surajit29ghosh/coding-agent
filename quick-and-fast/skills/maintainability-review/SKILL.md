---
name: maintainability-review
description: Quick maintainability and code quality review
---


# maintainability-review.md
```md
# Maintainability Review (Deep)

## Readability
- Intent-revealing names
- Avoid nested complexity (>3 levels)

## Structure
- Small cohesive classes
- Clear module boundaries

## Mutability & State
- Prefer immutability where possible
- Avoid unintended side effects
- Use readonly and init-only properties appropriately

## Resource Management
- Proper use of using statements for IDisposable
- Ensure streams, DB connections, and unmanaged resources are disposed

## Technical Debt
- TODO/FIXME tracked
- No commented-out dead code

## Documentation
- Explain WHY, not WHAT
```md
# Maintainability Review (Deep)

## Readability
- Intent-revealing names
- Avoid nested complexity (>3 levels)

## Structure
- Small cohesive classes
- Clear module boundaries

## Technical Debt
- TODO/FIXME tracked
- No commented-out dead code

## Documentation
- Explain WHY, not WHAT
```