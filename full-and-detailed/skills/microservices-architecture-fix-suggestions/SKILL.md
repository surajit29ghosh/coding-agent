---
name: microservices-architecture-fix-suggestions
description: Suggest improvements for microservices architecture violations
---

# Microservices Fix Suggestions

## Introduce Service APIs

Services should communicate through APIs.

Example:

OrderService → HTTP API → PaymentService

---

## Separate Databases

Each service must own its database.

Avoid shared schemas.

---

## Introduce Event-Driven Communication

Use messaging patterns such as:

Event Bus  
Message Queues
