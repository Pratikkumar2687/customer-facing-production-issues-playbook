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

---
## Investigation Steps
1. Check CloudWatch Logs

Look for:

Task timed out after XX.XX seconds

Review the logs immediately before the timeout.

Determine what operation was running when the function stopped.

2. Check Lambda Configuration

Review:

Timeout
Memory
Runtime
Environment variables
VPC configuration

Example AWS CLI command:

aws lambda get-function-configuration \
  --function-name <function-name>
3. Check Lambda Metrics

Review:

Duration
Errors
Throttles
Invocations
Concurrent executions

A consistent increase in duration can indicate an underlying performance problem.

4. Check Database Performance

If Lambda calls a database:

Check query execution time
Check connection latency
Check database CPU
Check database connections
Check connection pool configuration
5. Check External APIs

If Lambda calls an external service:

Measure response time
Check service availability
Review client timeout configuration
Check retry behavior
Possible Remediation

Depending on the root cause:

Optimize application code
Optimize database queries
Increase Lambda memory
Increase timeout when appropriate
Reduce unnecessary processing
Improve external API timeout handling
Move long-running work to asynchronous processing
Use SQS for decoupling when appropriate
Validation

After applying a fix:

Reproduce the original request
Verify Lambda completes successfully
Check CloudWatch logs
Compare execution duration
Verify API response time
Confirm customer functionality
Prevention

Consider:

CloudWatch alarms
Lambda duration monitoring
Error-rate monitoring
Distributed tracing
Performance testing
Dependency monitoring
Root Cause

Document the confirmed root cause here.

Do not classify the Lambda timeout itself as the root cause unless the timeout configuration was actually the underlying problem.

