---
name: resillience-review
description: Quick resilience and fault-handling review
---


# Resilience Review (Deep)

## Fault Handling
- Graceful degradation strategies
- Retry only for transient failures

## Exception Handling
- Exceptions are not swallowed silently
- Proper exception types used (no generic catch-all unless justified)
- Exceptions translated appropriately across layers
- Consistent error contracts returned to API consumers

## Policies
- Polly usage (retry, circuit breaker, bulkhead)

## Timeouts
- Explicit timeout configuration

## External Systems
- Defensive coding for API failures
- Idempotency for retries
```md
# Resilience Review (Deep)

## Fault Handling
- Graceful degradation strategies
- Retry only for transient failures

## Policies
- Polly usage (retry, circuit breaker, bulkhead)

## Timeouts
- Explicit timeout configuration

## External Systems
- Defensive coding for API failures
- Idempotency for retries
```
