---
name: security-review
description: Quick security and vulnerability review
---


# Security Review (Deep)

## Input Validation
- Validate at API boundary + business layer
- Enforce strict DTO contracts
- Detect over-posting vulnerabilities

## Authentication & Authorization
- Verify claims-based auth correctness
- Ensure authorization is NOT bypassed in services
- Check for privilege escalation paths

## Data Protection
- Ensure encryption at rest (sensitive fields)
- TLS enforced for all communication
- Validate hashing (bcrypt, PBKDF2—not plain SHA)

## Secrets Management
- No secrets in appsettings.json
- Use managed identity / vaults

## Vulnerabilities
- Injection (SQL, NoSQL, command)
- Insecure deserialization
- Broken access control

## Dependency & Package Security
- Check NuGet packages for known vulnerabilities (e.g., CVEs)
- Ensure no outdated or deprecated packages are used
- Verify transitive dependencies (not just direct ones)
- Use tools like `dotnet list package --vulnerable` or SCA scanners
- Ensure critical libraries are regularly patched
- Avoid untrusted or unofficial packages

## Logging Risks
- No PII/sensitive data in logs
- No PII/sensitive data in logs
```
