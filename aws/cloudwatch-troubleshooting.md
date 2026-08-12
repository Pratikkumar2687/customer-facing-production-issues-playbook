# Amazon CloudWatch Troubleshooting

## Overview

Amazon CloudWatch provides logs, metrics, alarms, and operational visibility for AWS workloads. Effective observability is essential when troubleshooting customer-facing production issues.

---

## Customer Symptoms

Examples:

- API errors
- Slow responses
- Lambda failures
- Infrastructure alerts
- Missing application functionality

---

## Troubleshooting Flow

```text
Customer Report
       |
       v
Application Metrics
       |
       v
CloudWatch Logs
       |
       v
CloudWatch Metrics
       |
       v
Correlate Timeline
       |
       v
Identify Root Cause
```

---

## Investigation Steps

### 1. Establish the Incident Time

Determine:

- First occurrence
- Last known good state
- Deployment time
- Configuration changes
- Dependency failures

This helps narrow the investigation window.

### 2. Review CloudWatch Logs

Look for:

- ERROR
- WARN
- Exception
- Timeout
- AccessDenied
- Connection errors

Avoid searching only for the final customer-facing error. Investigate the events leading to it.

### 3. Review Metrics

Depending on the service, review:

- Error count
- Request count
- Latency
- CPU
- Memory where available
- Throttles
- Concurrent executions

### 4. Check Alarms

Review:

- Alarm state
- Threshold
- Evaluation period
- Metric source
- Recent state changes

### 5. Correlate Events

Compare:

```text
Application Logs
       +
AWS Metrics
       +
Deployments
       +
Configuration Changes
       +
Customer Reports
```

A timeline often reveals the relationship between these events.

**Example Timeline:**

```text
10:00  Deployment started
10:05  API latency increases
10:07  HTTP 500 errors increase
10:08  Customer reports begin
10:12  Deployment rolled back
10:15  Error rate returns to normal
```

This strongly suggests investigating the deployment as a potential contributing factor. It does not automatically prove that the deployment was the root cause.

---

## Remediation

Depending on the issue:

- Roll back a problematic deployment
- Fix application errors
- Correct configuration
- Resolve dependency problems
- Adjust infrastructure capacity
- Improve monitoring

---

## Prevention

Implement:

- CloudWatch dashboards
- CloudWatch alarms
- Structured application logging
- Log retention policies
- Correlation IDs
- Distributed tracing where appropriate
- Clear operational runbooks

---

## Important Principle

Logs and metrics provide evidence. Do not declare a root cause until the available evidence supports it.

---

## Incident Documentation

After resolution, document:

- Customer impact
- Timeline
- Symptoms
- Root cause
- Resolution
- Preventive actions
