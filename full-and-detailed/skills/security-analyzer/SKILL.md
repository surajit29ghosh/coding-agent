---
name: security-analyzer
description: Detect security vulnerabilities in .NET code
---

# Security Analyzer

## Purpose

Detect common application vulnerabilities.

---

# Checks

## SQL Injection

Violation:

```csharp
var query = "SELECT * FROM Users WHERE name=" + username;
```

Fix:

Use parameterized queries.

---

## Hardcoded Secrets

Detect:

```
password
apiKey
connectionString
```

---

## Insecure Deserialization

Detect usage of unsafe serializers.

---

## Missing Input Validation

Detect controllers without validation attributes.

---

## Weak Cryptography

Flag usage of outdated algorithms.

---

# Output

```
security_findings.json
```
