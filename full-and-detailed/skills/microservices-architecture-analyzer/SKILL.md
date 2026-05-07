---
name: microservices-architecture-analyzer
description: Analyze microservices architecture compliance
---

# Microservices Architecture Analyzer

## Purpose

Evaluate whether the system follows microservices architecture principles.

Each service should be:

Independent  
Deployable  
Own its own database  

---

# Violations to Detect

Shared databases between services.

Service accessing another service database.

Strong synchronous service dependencies.

Shared domain models across services.

---

# Output

Provide:

Service boundary violations  
File paths  
Description  
Suggested improvements
