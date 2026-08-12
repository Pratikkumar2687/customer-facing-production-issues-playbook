# Amazon S3 Access Denied Troubleshooting

## Overview

Amazon S3 AccessDenied errors occur when an AWS principal does not have sufficient permission to perform an operation on an S3 resource.

---

## Customer Symptoms

Customers may experience:

- File upload failure
- File download failure
- Missing documents
- Application errors
- Failed image or asset retrieval

---

## Common Causes

- Missing IAM permission
- Incorrect bucket policy
- Incorrect object ARN
- Explicit Deny statement
- S3 Block Public Access configuration
- KMS permission issue
- Incorrect AWS account
- Incorrect bucket name or region

---

## Troubleshooting Flow

```text
Application
     |
     v
AWS Principal
     |
     v
IAM Evaluation
     |
     +------> Identity Policy
     |
     +------> Bucket Policy
     |
     +------> KMS Policy
     |
     v
Amazon S3
```

---

## Investigation Steps

### 1. Identify the AWS Principal

Determine which identity is making the request. Examples:

- IAM role
- Lambda execution role
- EC2 instance role
- ECS task role
- IAM user

### 2. Identify the S3 Operation

Determine whether the application is attempting:

```text
GetObject
PutObject
DeleteObject
ListBucket
```

These actions require different permissions.

### 3. Check IAM Permissions

Review the relevant IAM policy.

Example:

```json
{
  "Effect": "Allow",
  "Action": [
    "s3:GetObject"
  ],
  "Resource": "arn:aws:s3:::example-bucket/*"
}
```

### 4. Check Bucket Policy

Look for:

- Explicit Deny
- Incorrect principal
- Incorrect resource ARN
- Conditions that are not satisfied

**Remember:** an explicit Deny overrides an Allow.

### 5. Check Object Encryption

If the object uses SSE-KMS, verify that the requesting principal has the required KMS permissions.

### 6. Check Block Public Access

If public access was expected, verify whether S3 Block Public Access is preventing the request.

**Do not** disable Block Public Access simply to resolve an application permission problem.

---

## Remediation

Possible solutions:

- Correct IAM permissions
- Correct bucket policy
- Correct object ARN
- Grant required KMS permissions
- Correct AWS account or role
- Fix application configuration

---

## Security Considerations

Avoid using:

```json
"Principal": "*"
```

or overly broad permissions simply to make the error disappear. Use least privilege.

---

## Validation

Verify:

- Correct AWS principal
- Correct bucket
- Correct object
- Correct action
- Successful request
- No unnecessary permissions added

---

## Prevention

- IAM policy reviews
- CloudTrail auditing
- Least privilege
- Infrastructure as Code
- Automated security checks
