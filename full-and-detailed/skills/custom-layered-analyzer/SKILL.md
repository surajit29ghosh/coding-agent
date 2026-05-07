---
name: custom-layered-analyzer
description: Analyze repository for custom layered architecture with Plugin, Processor, ApiClient, Helper, Domain, and BaseClientContext
---

# Custom Layered Architecture Analyzer

## Purpose

Validate architecture compliance for the following layered system:

Plugin → Processor → ApiClient → Helper → External API  
Processor → Wrapper → Database  
ApiClient → Domain  
BaseClientContext used across layers for configuration

---

# Layer Responsibilities

## Plugin

- Entry point
- Invokes Processor
- Must not contain business logic

## Processor

- Orchestrates workflow
- Identifies candidates
- Calls ApiClient
- Uses Wrapper for DB operations

## ApiClient

- Converts request/response objects
- Calls Helper
- Maps responses to Domain entities

## Helper

- Prepares HTTP requests
- Calls external APIs
- Returns raw responses

## Domain

- Contains entities only
- No infrastructure or API logic

## BaseClientContext

- Shared configuration and settings
- Must not contain business logic

## Wrapper

- Handles database communication
- Used only by Processor

---

# Allowed Flow

Plugin → Processor  
Processor → ApiClient  
ApiClient → Helper  
Helper → External API  

Response Flow:

Helper → ApiClient → Domain → Processor → Wrapper

---

# Forbidden Patterns

Plugin calling ApiClient or Helper directly.

Processor calling Helper directly.

ApiClient accessing database.

Helper containing business logic.

Domain referencing infrastructure or HTTP logic.

Wrapper used outside Processor.

---

# Violations to Detect

- Layer skipping
- Business logic in Plugin or Helper
- ApiClient bypassing Domain models
- Direct HTTP calls outside Helper
- Database access outside Wrapper
- Improper BaseClientContext usage

---

# Output

Provide:

Violation summary  
File path  
Class name  
Layer violation description  
Recommended fix
