# AWS Lambda Timeout Troubleshooting

## Overview

AWS Lambda timeouts occur when a function does not complete within its configured timeout period.

A timeout can result in API failures, delayed processing, or customer-facing errors.

---

## Customer Symptoms

Customers may experience:

- API request timeout
- HTTP 5xx response
- Slow application response
- Background job failure
- Intermittent application errors

---

## Common Causes

- Slow database queries
- Slow third-party API
- Lambda timeout configured too low
- Cold start latency
- Network connectivity issues
- Large payload processing
- Inefficient application code
- Insufficient Lambda memory

---

## Troubleshooting Flow

```text
Customer Request
       |
       v
API Gateway
       |
       v
AWS Lambda
       |
       +-----------> Database
       |
       +-----------> External API
       |
       v
CloudWatch Logs
