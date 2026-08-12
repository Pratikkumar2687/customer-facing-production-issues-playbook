# Slow Database Queries

## Overview

Slow database queries occur when a query takes longer than expected to execute, leading to delayed responses and degraded application performance.

---

## Customer Symptoms

Customers experience slow page loads, delayed API responses, or request timeouts.

---

## Possible Causes

- Missing database indexes
- Inefficient SQL query
- Large table scans
- Excessive joins
- Database resource constraints
- Lock contention

---

## Investigation Steps

1. Identify the slow endpoint.
2. Identify the SQL query involved.
3. Measure query execution time.
4. Review the query execution plan.
5. Check indexes.
6. Check database CPU and memory.
7. Check for locks or blocking queries.

### Example

```sql
EXPLAIN
SELECT *
FROM orders
WHERE customer_id = 123;
```

---

## Resolution

Possible remediation:

- Add an appropriate index
- Rewrite the query
- Reduce unnecessary columns
- Optimize joins
- Improve pagination
- Review database resources

---

## Validation

Verify:

- Query execution time
- API response time
- Database CPU
- Customer-facing performance

---

## Prevention

- Query performance monitoring
- Slow query logging
- Index reviews
- Database performance testing

---

## Root Cause

Document the confirmed cause here.

**Example:** A frequently executed query was performing a full table scan because the filtering column did not have an appropriate index.
