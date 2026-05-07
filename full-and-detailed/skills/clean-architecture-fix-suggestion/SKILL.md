---
name: clean-architecture-fix-suggestion
description: Generates refactoring suggestions for architecture violations
---

# Architecture Refactoring Suggestions

## Input

architecture_findings

---

# Suggestions

## Domain referencing EF Core

Fix:

Move persistence to Infrastructure.

Example:

Application:

```
public interface IUserRepository
{
    Task<User> GetById(Guid id);
}
```

Infrastructure:

```
public class EfUserRepository : IUserRepository
{
    private readonly AppDbContext _context;
}
```

---

## Fat Controller

Extract business logic into UseCase.

Before:

```
controller -> dbcontext
```

After:

```
controller -> service -> repository
```

---

# Output

Markdown suggestions list.

Example:

```
Architecture Fix Suggestions

1. Move DbContext to Infrastructure layer
2. Introduce IUserRepository abstraction
3. Extract business logic from UserController
```