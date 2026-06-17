# Copilot Instructions for C# Clean Architecture Project

This file defines unified guidance for Copilot across **code review**, **code completion**, **documentation**, **testing**, and **unit test generation**.  
The project follows Clean Architecture principles with **Domain, Business (Application), and Infrastructure layers**, uses **Dependency Injection**, and implements **Vertical Slice Architecture** for pages/features.

---

## 🔍 Code Review

### Goals
Ensure submitted code adheres to Clean Architecture, coding best practices, and project conventions.

### Detailed Guidelines
- **Architecture Boundaries**
  - Domain layer must remain pure (no external dependencies).
  - Business/Application layer depends only on Domain.
  - Infrastructure layer implements interfaces defined in Business layer.
- **Dependency Injection**
  - All services, repositories, and handlers registered in DI container.
  - Correct lifetimes applied (`Scoped` for DbContext, `Singleton` for stateless services, etc.).
  - Avoid service locator anti-pattern.
- **Vertical Slice Architecture**
  - Each feature has its own folder with command/query, handler, DTOs, and validators.
  - Controllers remain thin, delegating logic to handlers.
- **Coding Best Practices**
  - Apply SOLID principles.
  - Use async/await properly, avoid blocking calls.
  - Ensure exception handling and logging via `ILogger<T>`.
  - Unit tests exist for business/domain logic.

---

## ✍️ Code Completion

### Goals
Generate new C# code that is clean, maintainable, and aligned with architecture.

### Detailed Guidelines
- **Layering**
  - Domain: entities, value objects, domain services.
  - Business: use cases, commands, queries, handlers.
  - Infrastructure: persistence, external APIs, implementations.
- **Dependency Injection**
  - Always inject dependencies via constructors.
  - Register abstractions in DI container.
- **Vertical Slice**
  - Each feature self-contained (command/query + handler).
  - Use MediatR or equivalent for request/response.
- **Coding Conventions**
  - Follow C# naming standards (PascalCase for classes, camelCase for variables).
  - Keep classes small and focused (SRP).
  - Use async/await for I/O operations.
- **Maintainability**
  - Code should be testable (no static dependencies).
  - Favor interfaces and abstractions over concrete implementations.

---

## 📖 Documentation

### Goals
Generate clear, developer-friendly documentation that explains purpose and usage.

### Detailed Guidelines
- **XML Comments**
  - Add `<summary>` for all public classes, methods, and interfaces.
  - Document parameters (`<param>`) and return values (`<returns>`).
- **Usage Examples**
  - Provide sample code snippets for handlers, commands, queries.
- **Architecture Documentation**
  - Domain: explain core business rules/entities.
  - Business: explain use cases and vertical slices.
  - Infrastructure: explain persistence and external service integration.
- **Dependency Injection**
  - Document how services are registered and resolved.
- **Style**
  - Concise, professional, developer-friendly language.

---

## 🧪 Testing

### Goals
Ensure robust test coverage across all layers.

### Detailed Guidelines
- **Unit Tests**
  - Cover domain entities, value objects, and business logic.
  - Validate edge cases (nulls, invalid inputs).
- **Mocking**
  - Use Moq (or equivalent) for external dependencies.
- **Patterns**
  - Follow AAA (Arrange, Act, Assert).
  - Clear test naming: `MethodName_ShouldExpectedBehavior_WhenCondition`.
- **Integration Tests**
  - Validate Infrastructure (repositories, API calls).
  - Ensure database queries are optimized (no N+1).
- **Quality**
  - Tests must be fast, deterministic, and independent.
  - Maintain high coverage without sacrificing readability.

---

## 🧩 Unit Test Generation

### Goals
Guide Copilot to generate high-quality unit tests automatically.

### Detailed Guidelines
- **Frameworks**
  - Use xUnit or NUnit (consistent with project setup).
- **Structure**
  - Follow AAA pattern.
  - Isolate tests (no reliance on external state).
- **Mocking**
  - Use Moq for dependencies.
  - Verify interactions (e.g., `Verify(repo.SaveAsync(...))`).
- **Coverage**
  - Generate tests for:
    - Happy path scenarios.
    - Edge cases (nulls, empty collections, invalid inputs).
    - Exception handling and logging.
- **Naming**
  - Use descriptive names: `Handler_ShouldReturnResult_WhenInputIsValid`.
- **Best Practices**
  - Keep tests small and focused.
  - Avoid duplication by using helper methods or test data builders.

---

## ✅ Copilot Review Prompts

When assisting, Copilot should:
1. Flag violations of Clean Architecture boundaries.
2. Suggest improvements for DI registration and lifetimes.
3. Recommend refactoring if vertical slice boundaries are blurred.
4. Generate code that is testable, maintainable, and documented.
5. Ensure unit and integration tests are present and meaningful.
6. Generate new unit tests that follow AAA, mocking, and naming best practices.