---
name: performance-review
description: Quick performance and scalability review
---


# Performance Review (Deep)

## Presentation Layer
- Avoid synchronous I/O in controllers
- Ensure minimal payload size (DTO shaping, pagination)
- Avoid over-fetching in API responses

## Business Layer
- Detect redundant computations across service calls
- Ensure proper async flow (no sync-over-async)
- Avoid excessive object mapping (AutoMapper misuse)

## Data Layer
- Identify N+1 queries (EF Core navigation pitfalls)
- Verify IQueryable vs IEnumerable usage (deferred execution)
- Ensure projections (Select) instead of full entity loads
- Check index usage via query patterns
- Detect chatty DB calls (multiple small queries vs batching)

## Memory & CPU
- Avoid large object allocations in loops
- Detect boxing/unboxing issues
- Watch for LINQ inefficiencies in hot paths

## Threading & Concurrency
- Avoid unnecessary thread creation (prefer async/await)
- Ensure thread-safe access to shared resources
- Avoid blocking calls that cause thread pool starvation
- Use concurrent collections where appropriate

## Loops & Algorithms
- Avoid nested loops where possible (optimize to O(n) / O(log n))
- Replace loops with set-based operations (LINQ/DB-side execution)
- Prevent repeated enumeration of collections

## Scalability
- Ensure stateless services
- Validate horizontal scaling readiness
- Check thread pool starvation risks
