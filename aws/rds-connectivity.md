# Amazon RDS Connectivity Troubleshooting

## Overview

RDS connectivity problems can prevent applications from accessing their database and may result in customer-facing application failures.

---

## Customer Symptoms

Customers may experience:

- HTTP 500 errors
- API failures
- Login failures
- Slow application responses
- Database connection timeouts
- Failed background jobs

---

## Common Causes

- Security group rules
- Network ACL configuration
- Incorrect hostname
- Incorrect port
- Incorrect credentials
- RDS instance unavailable
- VPC routing problems
- Private subnet connectivity
- DNS resolution issues
- Connection limit exhaustion

---

## Troubleshooting Flow

```text
Application
     |
     v
Network / VPC
     |
     v
Security Group
     |
     v
RDS Endpoint
     |
     v
Database
```

---

## Investigation Steps

### 1. Verify RDS Status

Check:

- Instance status
- Availability Zone
- Endpoint
- Port
- Engine
- Recent events

Example:

```bash
aws rds describe-db-instances \
  --db-instance-identifier <db-instance>
```

### 2. Verify Database Endpoint

Confirm that the application is using the correct RDS endpoint.

Example:

```text
database.example.region.rds.amazonaws.com
```

### 3. Check Security Groups

Verify that the application security group can connect to the RDS security group on the required database port.

Common ports:

```text
MySQL       3306
PostgreSQL  5432
```

Prefer security-group-to-security-group access rather than broad CIDR access where possible.

### 4. Check Network Configuration

Review:

- VPC
- Subnets
- Route tables
- Network ACLs
- NAT configuration where required

### 5. Check Credentials

Verify:

- Username
- Password
- Database name
- Secret configuration

**Do not** store database passwords in source code.

### 6. Check Connection Limits

Review:

- Active database connections
- Application connection pool
- RDS connection metrics

Connection exhaustion can look like a network problem from the application perspective.

---

## Remediation

Depending on the cause:

- Correct security group rules
- Correct database endpoint
- Fix routing
- Correct credentials
- Increase database capacity when justified
- Optimize connection pooling
- Reduce unnecessary connections

---

## Validation

Confirm:

- Application can connect
- Database queries succeed
- API requests succeed
- Error rate returns to normal
- Customer functionality is restored

---

## Prevention

- CloudWatch monitoring
- RDS alarms
- Connection monitoring
- Infrastructure as Code
- Automated configuration validation
- Proper secret management
