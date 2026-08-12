# Database Deadlocks

## Overview

A database deadlock occurs when two or more transactions hold locks that prevent each other from completing.

---

## Customer Symptoms

Customers may experience:

- Failed transactions
- Slow requests
- Intermittent errors
- Transaction rollback

---

## Example

```text
Transaction A
    |
    +--> Locks Row 1
    |
    +--> Waits for Row 2


Transaction B
    |
    +--> Locks Row 2
    |
    +--> Waits for Row 1
```

Both transactions are waiting for each other.

---

## Common Causes

- Inconsistent locking order
- Long-running transactions
- Large transactions
- Missing indexes
- Concurrent updates
- Poor transaction design

---

## Investigation Steps

Review:

- Database deadlock logs
- Transaction queries
- Lock information
- Query execution plans
- Application transaction flow

---

## Resolution

Possible solutions:

- Access resources in a consistent order
- Reduce transaction duration
- Optimize queries
- Add appropriate indexes
- Reduce transaction scope
- Implement safe retry behavior

---

## Validation

Verify:

- Deadlocks no longer occur under expected concurrency
- Transaction success rate improves
- Query latency remains acceptable

---

## Prevention

- Consistent transaction ordering
- Short transactions
- Proper indexing
- Concurrency testing
- Database monitoring
