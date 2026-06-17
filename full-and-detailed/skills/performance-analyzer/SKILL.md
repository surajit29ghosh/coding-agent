---
name: performance-analyzer
description: Analyze .NET code for performance issues
---

# Performance Analyzer

## Purpose

Detect common performance anti-patterns.

Uses AST analysis and heuristics.

---

# Checks

## N+1 Database Queries

Detect loops calling database queries.

Example violation:

```csharp
foreach(var user in users)
{
    var orders = repository.GetOrders(user.Id);
}
```

Fix:

Batch queries.

---

## Inefficient LINQ

Detect:

```
ToList().Where()
```

Better:

```
Where().ToList()
```

---

## Large Object Allocation

Detect allocations > 85KB triggering LOH.

Example:

```
new byte[100000]
```

---

## String Concatenation in Loops

Violation:

```
string s="";
for(...)
   s+=value;
```

Fix:

Use `StringBuilder`.

---

# Output

```
performance_findings.json
```
