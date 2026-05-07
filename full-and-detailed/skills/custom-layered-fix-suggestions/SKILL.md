---
name: custom-layered-fix-suggestions
description: Provide fixes for custom layered architecture violations
---

# Custom Layered Architecture Fix Suggestions

## Purpose

Provide refactoring guidance for architecture violations.

---

# Fix Patterns

## Fix Layer Skipping

Incorrect:

Plugin → ApiClient

Correct:

Plugin → Processor → ApiClient

---

## Move Business Logic

Incorrect:

Helper contains logic

Correct:

Move logic to Processor

---

## Fix API Flow

Incorrect:

Processor → Helper

Correct:

Processor → ApiClient → Helper

---

## Enforce Domain Usage

Incorrect:

ApiClient returns raw API data

Correct:

Map to Domain entities

---

## Fix Database Access

Incorrect:

ApiClient accessing DB

Correct:

Processor → Wrapper → DB

---

## Fix Context Usage

Ensure BaseClientContext is used only for configuration.

---

# Output

Provide:

Problem description  
Refactoring steps  
Improved architecture example
