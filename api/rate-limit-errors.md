# API Rate Limit Errors

## Overview

Rate limiting protects APIs from excessive traffic and helps maintain service availability.

---

## Customer Symptoms

Customers may receive:

```text
HTTP 429 Too Many Requests
```

---

## Common Causes

- Excessive client requests
- Retry loops
- Traffic spikes
- Incorrect client configuration
- Shared API quotas
- Unexpected automated traffic

---

## Investigation

Determine:

- Which client is affected?
- When did the issue begin?
- How many requests are being generated?
- Is the problem isolated to one customer?
- Is the entire API affected?

---

## Checks to Perform

Review:

- API Gateway metrics
- Application logs
- Client request frequency
- Rate-limit configuration
- Traffic patterns

---

## Resolution

Possible solutions:

- Correct client retry behavior
- Implement exponential backoff
- Increase limits when justified
- Cache frequently requested data
- Reduce unnecessary API calls
- Use asynchronous processing

### Recommended Retry Pattern

Clients should avoid immediate repeated retries.

Example:

```text
Request
   |
   v
429
   |
   v
Wait
   |
   v
Retry with backoff
```

---

## Prevention

- Rate-limit monitoring
- Client-side throttling
- Exponential backoff
- Request caching
- Usage alerts
