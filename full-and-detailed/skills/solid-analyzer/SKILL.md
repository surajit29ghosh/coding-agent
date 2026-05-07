---
name: solid-analyzer
description: Analyze .NET codebase for SOLID principle violations using AST
---

# SOLID Analyzer

## Purpose

Analyze C# code for violations of SOLID design principles using syntax trees from :contentReference[oaicite:1]{index=1}.

---

# Inputs

solution_path

---

# Principles Checked

## Single Responsibility Principle (SRP)

A class should have **only one reason to change**.

Detect:

- classes with excessive methods
- classes mixing business + persistence + API logic

Example violation:

```csharp
class UserService
{
    public void CreateUser() {}
    public void SaveToDatabase() {}
    public void SendEmail() {}
}
```

---

## Open Closed Principle (OCP)

Classes should be **open for extension but closed for modification**.

Detect:

- switch statements on types
- large conditional behavior blocks

Violation:

```csharp
if(type == "Admin") {}
else if(type == "User") {}
```

---

## Liskov Substitution Principle (LSP)

Subtypes must be replaceable for their base types.

Detect:

- overridden methods throwing exceptions
- breaking base class contracts

Example violation:

```csharp
class Bird
{
    public virtual void Fly() {}
}

class Penguin : Bird
{
    public override void Fly()
    {
        throw new Exception();
    }
}
```

---

## Interface Segregation Principle (ISP)

Clients should not depend on methods they do not use.

Violation:

```
IWorker
    Work()
    Eat()
```

Better:

```
IWorkable
IEatable
```

---

## Dependency Inversion Principle (DIP)

High level modules should depend on **abstractions**.

Violation:

```csharp
OrderService service = new OrderService(new SqlOrderRepository());
```

Better:

```csharp
OrderService service = new OrderService(IOrderRepository repo);
```

---

# Output

```
solid_findings.json
```
