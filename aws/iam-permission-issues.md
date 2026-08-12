# AWS IAM Permission Troubleshooting

## Overview

IAM permission issues occur when an AWS principal attempts an action that is not authorized. These problems are common in applications that integrate multiple AWS services.

---

## Customer Symptoms

Customers may see:

- Application errors
- Failed uploads
- Failed API requests
- Missing data
- Background job failures
- HTTP 403 responses

---

## Common Causes

- Missing Allow permission
- Explicit Deny
- Incorrect resource ARN
- Incorrect IAM role
- Incorrect AWS account
- Permission boundary
- Service Control Policy
- Resource-based policy
- Incorrect conditions

---

## IAM Evaluation Concept

A simplified authorization flow:

```text
Request
   |
   v
Authentication
   |
   v
Identity Policy
   |
   +------> Resource Policy
   |
   +------> Permission Boundary
   |
   +------> Service Control Policy
   |
   v
Allow / Deny
```

An explicit Deny takes precedence over an Allow.

---

## Investigation Steps

### 1. Identify the Principal

Determine:

- IAM user
- IAM role
- Lambda execution role
- EC2 role
- ECS task role

### 2. Identify the Requested Action

Examples:

```text
s3:GetObject
dynamodb:GetItem
secretsmanager:GetSecretValue
bedrock:InvokeModel
```

### 3. Identify the Resource

Verify the resource ARN.

Example:

```text
arn:aws:s3:::example-bucket/*
```

### 4. Review IAM Policies

Look for:

- Missing Allow
- Incorrect Resource
- Incorrect Action
- Conditions preventing access

### 5. Check Explicit Denies

Investigate:

- Identity policies
- Resource policies
- Permission boundaries
- Service Control Policies

---

## Recommended Approach

Do not immediately attach `AdministratorAccess` as a troubleshooting shortcut.

Instead:

1. Identify the exact API action
2. Identify the exact resource
3. Add the minimum required permission
4. Test the operation
5. Remove unnecessary permissions

### Example Least Privilege Policy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject"
      ],
      "Resource": "arn:aws:s3:::example-bucket/*"
    }
  ]
}
```

---

## Validation

Verify:

- Correct role is being used
- Requested action succeeds
- Resource is correct
- No unnecessary permissions were granted

---

## Prevention

- Least privilege
- IAM policy reviews
- Infrastructure as Code
- IAM Access Analyzer
- CloudTrail auditing
- Automated security checks
