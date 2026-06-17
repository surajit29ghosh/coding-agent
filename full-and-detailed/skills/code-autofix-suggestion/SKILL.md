---
name: code-autofix-suggestion
description: Generate refactoring suggestions for NFR issues
---

# NFR Autofix Suggestions

## Performance Fix

Replace:

```
string s=""
```

With:

```
StringBuilder builder = new StringBuilder()
```

---

## Security Fix

Replace string SQL with parameterized query.

---

## Memory Fix

Use object pooling or reuse allocations.

---

## Async Fix

Replace:

```
task.Result
```

With:

```
await task
```
