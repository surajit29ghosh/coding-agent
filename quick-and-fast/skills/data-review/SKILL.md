---
name: data-review
description: Quick data model, transactions, and ORM review
---


# data-review.md
```md
# Data Review (Deep)

## Integrity
- Constraints enforced (DB + app level)
- Null handling explicitly defined

## Transactions
- Proper transaction scope
- Avoid long-running transactions

## ORM Usage
- EF tracking vs NoTracking usage correct
- Lazy loading risks identified

## Concurrency
- Optimistic concurrency handling (RowVersion)
- Deadlock risks minimized

## Data Evolution
- Migrations backward compatible
- Rollback strategy exists
```

