---
name: enterprise-architecture-scoring-engine
description: Evaluate architecture quality and produce enterprise architecture score (0–100)
---

# Enterprise Architecture Scoring Engine

## Purpose

Evaluate the quality of the system architecture and produce an architecture score.

Score range:

0 – 100

This score represents overall architectural health.

---

# Scoring Categories

Evaluate the architecture across the following dimensions.

Each dimension contributes to the final score.

Architecture Structure  
Dependency Management  
Module Boundaries  
Service Independence  
Data Ownership  
Coupling and Cohesion  
Scalability Readiness  
Maintainability  

---

# Category Scoring

## Architecture Structure (0–15)

Evaluate whether the system structure follows a consistent architectural pattern.

Examples:

Layered  
Microservices  
Modular Monolith  

Violations:

Mixed architecture patterns without boundaries.

---

## Dependency Management (0–15)

Check for proper dependency flow.

Violations:

Circular dependencies  
Domain referencing infrastructure  
Cross-module direct access  

---

## Module Boundaries (0–15)

Evaluate separation of business capabilities.

Strong architecture should have clear modules.

Violations:

God modules  
Cross-module coupling  
Shared internal classes  

---

## Service Independence (0–15)

For microservices architecture.

Evaluate:

Independent deployments  
Independent scaling  
Loose service coupling  

Violations:

Shared databases  
Direct service database access  

---

## Data Ownership (0–10)

Check whether services or modules own their data.

Violations:

Shared database tables across services.

---

## Coupling and Cohesion (0–10)

Measure:

Loose coupling  
High cohesion within modules  

Violations:

Cross-cutting dependencies  
God services  

---

## Scalability Readiness (0–10)

Evaluate architecture scalability.

Indicators:

Stateless services  
Horizontal scalability  
Event-driven architecture  

---

## Maintainability (0–10)

Evaluate long-term maintainability.

Indicators:

Clear module boundaries  
Low complexity  
Readable project structure  

---

# Final Score Calculation

Total Score =

Structure  
+ Dependencies  
+ Module Boundaries  
+ Service Independence  
+ Data Ownership  
+ Coupling & Cohesion  
+ Scalability  
+ Maintainability  

Maximum Score: 100

---

# Score Interpretation

90 – 100  
Excellent architecture

75 – 89  
Strong architecture

60 – 74  
Moderate architecture

40 – 59  
Weak architecture

Below 40  
Critical architectural issues

---

# Output Format

Architecture Score: X / 100

Strengths

List architectural strengths.

Weaknesses

List architectural weaknesses.

Recommendations

Provide actionable improvements.

Architecture Risk Level

Low  
Moderate  
High
