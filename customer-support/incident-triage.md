# Customer Incident Triage

## Overview

Incident triage is the process of quickly understanding a customer-facing production issue, determining its scope and severity, and coordinating the appropriate response.

The goal is not to immediately identify the root cause. The initial goal is to:

1. Confirm the issue
2. Understand customer impact
3. Determine severity
4. Identify affected systems
5. Begin investigation
6. Establish ownership
7. Communicate appropriately

---

## Customer Symptoms

Customers may report:

- Application unavailable
- API requests failing
- Slow application responses
- Login failures
- Payment failures
- Missing or delayed data
- Email or notification delays
- File upload/download failures
- Intermittent errors

---

## 1. Confirm the Incident

First determine whether the reported behavior represents an actual system problem.

Verify:

- What functionality is affected?
- When did the issue begin?
- Is the issue reproducible?
- Is the issue affecting one customer or multiple customers?
- Are monitoring systems reporting related errors?

Avoid assuming that every customer-reported issue is caused by a production outage.

---

## 2. Identify Customer Impact

Determine the scope of the incident.

### Customer Scope

Ask:

- Is one customer affected?
- Are multiple customers affected?
- Are all customers affected?
- Is the issue limited to a specific region?
- Is the issue limited to a specific customer segment?

### Functionality Scope

Determine which functionality is affected:

- Authentication
- Payments
- APIs
- Data access
- Reporting
- Notifications
- File processing
- Background jobs
- Application availability

---

## 3. Establish the Timeline

Create an initial timeline.

Important timestamps include:

- First customer report
- First monitoring alert
- First observed error
- Last known successful request
- Recent deployment
- Configuration change
- Infrastructure change
- Dependency failure

Example:

```text
09:42 AM  First customer report
09:45 AM  Monitoring alert triggered
09:48 AM  Engineering investigation started
09:55 AM  Increased API error rate identified
10:05 AM  Recent deployment identified as potential factor
10:15 AM  Mitigation applied
10:22 AM  Error rate returned to normal
```

The timeline should contain observed facts rather than assumptions.

---

## 4. Assess Severity

Severity should be based on customer and business impact.

Consider:

- Number of affected customers
- Business functionality affected
- Service availability
- Revenue impact
- Data integrity
- Security implications
- Duration
- SLA commitments

Example severity model:

| Severity | Example |
|----------|---------|
| Low      | Minor functionality issue affecting a small number of users |
| Medium   | Important functionality degraded for a subset of customers |
| High     | Major functionality unavailable for many customers |
| Critical | Widespread outage, major data issue, or significant security impact |

Organizations may use different severity definitions. Always follow the organization's incident-management policy when one exists.

---

## 5. Identify the Affected System

Determine which component may be involved. Possible systems include:

```text
Customer
   |
   v
Frontend
   |
   v
API Gateway / Load Balancer
   |
   v
Application
   |
   +------> Database
   |
   +------> Cache
   |
   +------> Queue
   |
   +------> Third-Party API
   |
   +------> AWS Services
```

Do not assume the first component showing an error is necessarily the root cause.

---

## 6. Check Monitoring and Logs

Review available observability data.

### Application

Check:

- Application logs
- Error rates
- Response times
- Exception rates
- Request IDs

### AWS

Depending on the architecture, check:

- CloudWatch Logs
- CloudWatch Metrics
- Lambda metrics
- API Gateway metrics
- RDS metrics
- S3 events
- CloudTrail events

### Infrastructure

Check:

- CPU
- Memory
- Network
- Disk
- Connection counts
- Queue depth

---

## 7. Check Recent Changes

Recent changes are important investigation signals.

Review:

- Application deployments
- Infrastructure deployments
- Terraform changes
- Configuration changes
- Database migrations
- Dependency updates
- IAM policy changes
- Third-party API changes

Example:

```text
Customer issue
      |
      v
Error rate increased
      |
      v
Check recent changes
      |
      v
Deployment occurred 10 minutes earlier
      |
      v
Investigate deployment
```

A recent deployment is a potential contributing factor, not automatic proof of causation.

---

## 8. Determine Immediate Mitigation

During an active incident, restoring customer functionality may be more important than immediately finding the permanent root cause.

Possible mitigation actions include:

- Roll back a deployment
- Disable a problematic feature
- Restart an unhealthy component
- Redirect traffic
- Increase capacity
- Temporarily disable a failing integration
- Process queued work after recovery

Any mitigation should be assessed for potential side effects before implementation.

---

## 9. Establish Incident Ownership

Clearly identify:

- Incident owner
- Technical investigator
- Customer/support contact
- Infrastructure owner
- Vendor or third-party contact when required

Avoid having multiple engineers independently investigate the same issue without coordination.

---

## 10. Customer Communication

Communication should be timely, accurate, and appropriate for the audience.

**Initial Communication**

> We are investigating an issue affecting [functionality]. Our engineering team is actively working to identify the cause and restore normal service.

**Progress Update**

> Our engineering team has identified an issue affecting [functionality] and is working on mitigation. We are continuing to monitor the affected service.

**Resolution**

> The issue affecting [functionality] has been resolved. We have verified that the service is operating normally and will continue monitoring it.

---

## 11. Information to Avoid Sharing

Do not expose:

- Passwords
- API keys
- Access tokens
- Private credentials
- Customer PII
- Internal security controls
- Confidential infrastructure information
- Unconfirmed root causes
- Internal blame

Technical details should be shared according to the organization's security and communication policies.

---

## 12. Validate Recovery

After mitigation or resolution, verify that customer functionality has actually recovered.

Check:

- Error rate
- Response latency
- Application logs
- Infrastructure metrics
- Queue processing
- Database health
- Customer reports

Do not close an incident solely because an error metric returned to normal. Confirm the affected customer workflow works as expected.

---

## 13. Post-Incident Review

After the incident is resolved, document:

- Customer impact
- Timeline
- Symptoms
- Root cause
- Contributing factors
- Mitigation
- Permanent resolution
- Detection gaps
- Preventive actions
- Lessons learned

---

## 14. Triage Checklist

Use this checklist during an incident:

- [ ] Confirm the reported issue
- [ ] Identify affected functionality
- [ ] Identify affected customers
- [ ] Determine when the issue started
- [ ] Assess severity
- [ ] Establish incident owner
- [ ] Check application logs
- [ ] Check infrastructure metrics
- [ ] Check recent deployments
- [ ] Check configuration changes
- [ ] Check external dependencies
- [ ] Determine immediate mitigation
- [ ] Communicate customer impact
- [ ] Validate recovery
- [ ] Document the incident
- [ ] Identify preventive actions

---

## 15. Key Principle

The objective of incident triage is not to guess the root cause quickly.

The objective is to establish facts, understand customer impact, stabilize the system, and create a structured path toward root-cause identification and permanent resolution.
