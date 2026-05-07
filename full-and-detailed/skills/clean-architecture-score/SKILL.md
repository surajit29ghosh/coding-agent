---
name: clean-architecture-score
description: Calculate architecture health score for .NET solutions
---

# Clean Architecture Score

## Purpose

Calculate an architecture health score between **0 and 100**.

## Inputs

`architecture_findings`

Example:

```json
{
  "dependencyViolations": 1,
  "domainViolations": 1,
  "missingRepositories": 2,
  "fatControllers": 1
}
```

---

# Scoring Weights

| Category | Max Score |
|--------|--------|
Dependency Direction | 30 |
Domain Purity | 25 |
Abstractions | 20 |
Use Case Structure | 15 |
Controller Thinness | 10 |

---

# Scoring Rules

## Dependency Direction

Perfect layering

Score: **30**

Minor violations

Score: **20**

Major violations

Score: **5**

---

## Domain Purity

No frameworks

Score: **25**

Minor references

Score: **10**

Heavy framework usage

Score: **0**

---

## Abstraction Usage

Repository pattern implemented

Score: **20**

Partial implementation

Score: **10**

Missing

Score: **0**

---

## Use Case Layer

Dedicated use case classes

Score: **15**

Only services

Score: **8**

None

Score: **0**

---

## Controller Thinness

Thin controllers

Score: **10**

Moderate logic

Score: **5**

Fat controllers

Score: **0**

---

# Output

Example report:

```
Architecture Score: 82/100

Breakdown

Dependency Direction: 25
Domain Purity: 20
Abstractions: 15
Use Case Structure: 12
Controller Thinness: 10

Interpretation

90–100 → Excellent architecture  
70–89 → Good architecture  
50–69 → Needs improvement  
<50 → Major architecture issues
```
