---
name: microservices-architecture
description: Enterprise Microservices Architecture analyzer for .NET projects - service boundary validation, independence scoring, distributed pattern analysis, health metrics, and PR automation.
tags:
  - architecture
  - microservices
  - distributed
  - .net
  - csharp
  - service-oriented
  - scalability
---

# Microservices Architecture Skill for .NET

## Overview
Comprehensive Microservices Architecture conformity analyzer for .NET solutions. Validates service boundaries, evaluates independence and autonomy, analyzes communication patterns, and provides detailed health assessment with actionable guidance.

## Core Architecture Principles Verified

### 1. **Service Boundaries**
- Clear, well-defined service responsibilities
- Single Business Capability per service
- Minimal cross-service dependencies
- Domain-driven service design
- Clear service ownership

### 2. **Data Ownership**
- Database per service pattern
- No shared databases between services
- Eventual consistency where needed
- Proper event-driven data synchronization
- Clear data ownership boundaries

### 3. **Service Autonomy**
- Independent deployment
- Independent scaling
- Technology diversity
- Internal technology choices
- Minimal shared libraries

### 4. **Synchronous Communication**
- API contracts via interfaces
- REST/gRPC proper usage
- Request-response patterns
- Timeout and retry policies
- Circuit breaker patterns

### 5. **Asynchronous Communication**
- Event-driven architecture
- Message queue patterns
- Event sourcing where appropriate
- Publish-subscribe patterns
- Saga patterns for distributed transactions

### 6. **Resilience & Fault Tolerance**
- Service isolation
- Timeout management
- Retry policies with backoff
- Circuit breaker implementation
- Graceful degradation

### 7. **Operational Maturity**
- Service observability
- Distributed tracing
- Monitoring and alerting
- Service discovery
- Configuration management

## Comprehensive Analysis Coverage

### Phase 1: Service Discovery & Classification
- Service Identification (by project, namespace, artifact)
- Service Purpose & Ownership
- Business Capability mapping
- Service versioning and stability
- Technology stack per service

### Phase 2: Boundary Analysis
- Data Ownership (database per service validation)
- Direct database access across services
- Shared resource usage
- Resource coupling detection
- Shared library analysis

### Phase 3: Autonomy Assessment
- Deployment independence
- Scaling configuration
- Technology choices
- Configuration management
- Infrastructure dependencies

### Phase 4: Communication Pattern Analysis
- Synchronous call chains (depth and complexity)
- Asynchronous message patterns
- Event-driven implementation
- Saga pattern usage
- API versioning strategy

### Phase 5: Resilience & Operational Analysis
- Timeout policies
- Retry patterns
- Circuit breaker implementation
- Bulkhead pattern usage
- Health check endpoints
- Service discovery integration
- Monitoring instrumentation
- Distributed tracing

## Health Scoring System

Multi-dimensional scoring across 11 weighted categories (0-100 scale):

| Category | Weight | Evaluation Criteria |
|----------|--------|-------------------|
| **Service Boundaries** | 14% | Clear responsibilities, domain-driven design |
| **Data Independence** | 14% | Database per service, no shared databases |
| **Service Autonomy** | 13% | Independent deployment, scaling, technology |
| **API Quality** | 11% | Versioning, contracts, stability |
| **Async Patterns** | 11% | Event-driven, messaging, pub-sub |
| **Sync Patterns** | 10% | Proper REST/gRPC, request-reply patterns |
| **Resilience** | 10% | Timeouts, retries, circuit breakers |
| **Observability** | 9% | Tracing, monitoring, logging |
| **Configuration Mgmt** | 5% | Externalized, environment-specific |
| **Naming Consistency** | 2% | Clear, descriptive service names |
| **Documentation** | 1% | API docs, service purpose |

**Health Score Levels:**
- **90-100**: Excellent - Mature microservices architecture
- **75-89**: Good - Mostly well-designed, minor coupling
- **60-74**: Fair - Distributed monolith concerns, refactoring needed
- **40-59**: Poor - Significant issues, significant work required
- **0-39**: Critical - Not truly microservices, immediate intervention

## Component Structure

### 1. Analyzer
Detects microservices architecture deviations:
- Service boundary violations
- Shared database usage
- Excessive service coupling
- Synchronous call chains
- Missing event patterns
- Deployment dependencies
- Resilience pattern gaps
- Observability gaps

### 2. Scorer
Computes microservices health metrics:
- Service independence score
- Data coupling metrics
- Deployment complexity
- Communication pattern scores
- Resilience readiness
- Observability level
- Operational maturity

### 3. Fix Suggestions
Refactoring patterns for microservices improvement:
- Extract new services
- Separate shared databases
- Implement event-driven patterns
- Add resilience patterns
- Improve API versioning
- Add observability
- Implement service discovery
- Optimize communication

### 4. PR Review Automation
Intelligent microservices architecture reviews:
- Service boundary violations
- Data ownership breaches
- Excessive coupling
- Missing resilience
- API contract issues
- Positive reinforcement

## Violation Severity Levels

- **CRITICAL**: Shared database, reverse service dependency
- **MAJOR**: Excessive call chains, missing resilience patterns
- **MODERATE**: API versioning issues, poor async implementation
- **MINOR**: Documentation gaps, naming inconsistencies

## Microservices Metrics

### Service Coupling Metrics
```
Afferent Service Coupling (incoming calls)
Efferent Service Coupling (outgoing calls)
Call Chain Depth (max sync call depth)
Data Coupling (shared resources)
```

### Autonomy Index
```
A = (1 - DataCoupling) × (1 - CommunicationCoupling)
  - Close to 1.0: Highly autonomous
  - Close to 0.0: Tightly coupled
```

### Resilience Readiness
```
R = (Timeouts + RetryPolicies + CircuitBreakers) / ExpectedPatterns
  - 1.0: Fully resilient
  - <1.0: Gaps in resilience
```

## Usage Scenarios

- Monolith to Microservices Migration Assessment
- Service Boundary Validation
- Continuous Coupling Monitoring
- Resilience Pattern Verification
- Distributed System Health Check

## Integration Points

- CI/CD: Deployment verification
- Service Registry: Service discovery validation
- Monitoring: Health metrics collection
- Testing: Integration and contract testing
- Operations: Service dependencies documentation

## Configuration Options

```yaml
analysis:
  service_detection:
    by_project: true
    by_namespace: true
    by_deployment_unit: true
  
  data_ownership:
    enforce_database_per_service: true
    detect_shared_resources: true
  
  communication:
    max_sync_call_depth: 3
    require_async_for_eventual_consistency: true
  
  resilience:
    require_timeouts: true
    require_retry_policies: true
    require_circuit_breakers: true
```

## Team Guidelines

1. Keep services small and focused - One business capability
2. Own your data - No shared databases or entities
3. Design for independent deployment - Minimize coupling
4. Use async where appropriate - Decouple with events
5. Implement resilience patterns - Timeouts, retries, circuit breakers
6. Version your APIs carefully - Contract stability
7. Monitor everything - Distributed tracing essential
8. Own service discovery - Know how services find each other
9. Plan for failures - Services will fail
10. Document service contracts - Clear API specifications

## Related Documentation
- [Building Microservices - Sam Newman](https://samnewman.io/books/building_microservices_2nd_edition/)
- [Microservices Patterns - Chris Richardson](https://microservices.io/)
- [Domain-Driven Design - Eric Evans](https://www.domainlanguage.com/ddd/)
- [The Twelve-Factor App](https://12factor.net/)
