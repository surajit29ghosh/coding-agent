---
name: memory-analyzer
description: Detect memory pressure and GC issues
---

# GC Memory Analyzer

## Purpose

Detect patterns causing excessive allocations and garbage collection.

---

# Checks

## Large Object Heap Allocations

Objects > 85 KB.

---

## Excessive Allocations

Detect allocations inside loops.

---

## Boxing Allocations

Example:

```
object x = 10
```

---

## IDisposable Misuse

Detect missing disposal.

Example:

```
FileStream stream = new FileStream(...)
```

Should use:

```
using var stream = new FileStream(...)
```

---

# Output

```
gc_findings.json
```
