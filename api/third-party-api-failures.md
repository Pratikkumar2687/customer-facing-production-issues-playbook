# Third-Party API Failures

## Overview

Applications often depend on external services for payments, messaging, identity, shipping, analytics, or other business functionality. A third-party failure can therefore become a customer-facing application issue.

---

## Customer Symptoms

Customers may experience:

- Failed transactions
- Slow responses
- Missing data
- HTTP 5xx errors
- Intermittent functionality

---

## Common Causes

- Third-party service outage
- Network failure
- API rate limiting
- Authentication failure
- API contract change
- Increased latency
- Invalid request
- Third-party maintenance

---

## Investigation Steps

### 1. Check Application Logs

Identify:

- HTTP status
- Response time
- Request ID
- Error message
- Endpoint

Do not log sensitive request data.

### 2. Check Third-Party Status

Review the provider's official status information when available.

### 3. Compare Current and Historical Behavior

Determine:

- Normal response time
- Current response time
- Error-rate increase
- Time of first failure

---

## Resolution

Depending on the situation:

- Retry transient failures
- Implement exponential backoff
- Use circuit breakers
- Queue requests
- Fail gracefully
- Use fallback functionality
- Contact the third-party provider

---

## Customer Experience

If the external dependency is unavailable, avoid exposing technical implementation details. Provide a clear explanation of the functionality affected and the current status.

---

## Prevention

- Dependency monitoring
- Timeouts
- Retries
- Circuit breakers
- Fallback mechanisms
- External-service health monitoring
- Contract testing
