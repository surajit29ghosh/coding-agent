---
name: enterprise-architecture-style-detector
description: Automatically detect the architectural style of a repository including layered, component-based, microservices, monolith, and modular monolith
---

# Enterprise Architecture Style Detector

## Purpose

Analyze the repository structure and determine the architectural style implemented.

Supported architecture styles:

Layered Architecture  
Component-Based Architecture  
Microservices Architecture  
Monolithic Architecture  
Modular Monolith Architecture  

Hybrid architectures should also be detected.

---

# Step 1 — Analyze Repository Structure

Inspect:

Solution files  
Project folders  
Dependency graphs  
Service boundaries  
Deployment boundaries  
API contracts  
Database ownership  

Look for indicators such as:

Number of deployable services  
Shared database usage  
Module boundaries  
Component encapsulation  

---

# Step 2 — Detect Architecture Patterns

## Layered Architecture Indicators

Presence of folders such as:

Presentation  
Application  
Domain  
Infrastructure  

Dependencies flow downward only.

Controllers call services rather than repositories directly.

---

## Component-Based Architecture Indicators

Presence of functional components such as:

Orders  
Billing  
Users  
Inventory  

Each component contains its own:

API layer  
Domain logic  
Data access  

---

## Microservices Architecture Indicators

Multiple independently deployable services.

Characteristics:

Service folders or repositories  
Independent APIs  
Independent databases  
Service-to-service communication  

Communication methods:

REST APIs  
Messaging systems  
Event streaming  

---

## Monolithic Architecture Indicators

Single deployable application.

Characteristics:

Shared database  
Single solution  
Centralized application logic  

Modules may exist but not enforced.

---

## Modular Monolith Indicators

Single deployable application organized into strong modules.

Characteristics:

Business modules  
Clear module boundaries  
Encapsulated module logic  
Module APIs

Example modules:

Orders  
Payments  
Catalog  
Users  

---

# Step 3 — Identify Hybrid Architectures

If the repository contains multiple patterns, report hybrid architecture.

Examples:

Layered Monolith  
Modular Monolith  
Microservices with shared libraries  

---

# Step 4 — Architecture Confidence Score

Provide a confidence level for the detected architecture.

Example output:

Detected Architecture: Modular Monolith

Confidence Score: 85%

Secondary Pattern: Layered Architecture

---

# Step 5 — Architecture Summary

Output:

Detected architecture style  
Confidence score  
Supporting observations  
Key structural indicators
