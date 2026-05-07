---
name: solid-fix-suggestion
description: Generate SOLID refactoring suggestions
---

# SOLID Autofix Suggestions

## Input

solid_findings

---

# SRP Fix

Split large classes into smaller ones.

Before:

```csharp
class UserManager
{
    SaveUser()
    SendEmail()
    LogActivity()
}
```

After:

```
UserService
EmailService
AuditService
```

---

# OCP Fix

Replace conditionals with polymorphism.

Before:

```csharp
switch(paymentType)
```

After:

```
IPaymentStrategy
CreditCardPayment
PaypalPayment
```

---

# LSP Fix

Refactor inheritance hierarchy.

Use composition when subclass cannot fulfill base contract.

---

# ISP Fix

Split large interfaces.

Before:

```
IWorker
```

After:

```
IWorkable
IReportable
```

---

# DIP Fix

Introduce dependency injection.

Example:

```csharp
public class OrderService
{
    private readonly IOrderRepository repository;

    public OrderService(IOrderRepository repository)
    {
        this.repository = repository;
    }
}
```

---

# Output

```
solid_refactor_suggestions.md
```
