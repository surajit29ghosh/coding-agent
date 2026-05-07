---
name: concurrency-analyzer
description: Detect concurrency issues in .NET applications
---

# Concurrency Analyzer

## Checks

## Blocking Calls in Async Methods

Violation:

```
task.Result
task.Wait()
```

---

## Missing ConfigureAwait

Detect missing ConfigureAwait in library code.

---

## Deadlock Risks

Detect nested locks.

---

## Thread Safety Issues

Detect shared mutable state without locking.
