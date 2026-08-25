
# AWS Security Gap Analysis

## 1. Overview

This gap analysis identifies security controls that require customer action under the AWS Shared Responsibility Model.

The assessment focuses on the three-tier application described in the lab scenario and the AWS services used by the environment.

---

# 2. Critical Gaps

## Gap 1: EC2 Guest Operating System Patching

**Responsibility:** Customer

**Risk:** High

**Status:** TODO

### Risk

AWS manages the underlying physical infrastructure and hypervisor, but the customer is responsible for the guest operating system running on EC2.

Unpatched operating systems may contain known vulnerabilities that attackers can exploit.

### Recommended Action

Implement automated patch management using AWS Systems Manager.

### Priority

**Critical**

### Target Timeline

Within 1 week.

---

## Gap 2: IAM Multi-Factor Authentication

**Responsibility:** Customer

**Risk:** High

**Status:** TODO

### Risk

A compromised password can allow an attacker to access AWS resources.

### Recommended Action

Enable MFA for all human users and use centralized identity management where possible.

### Priority

**Critical**

### Target Timeline

Immediately.

---

## Gap 3: Excessive IAM Permissions

**Responsibility:** Customer

**Risk:** High

**Status:** Review Needed

### Risk

Overly broad IAM policies can allow compromised accounts or applications to perform unauthorized actions.

### Recommended Action

Review IAM users, groups and roles.

Apply least-privilege permissions and remove unnecessary permissions.

### Priority

**Critical**

### Target Timeline

Within 1 week.

---

# 3. High Priority Gaps

## Gap 4: S3 Public Access

**Responsibility:** Customer

**Risk:** High

**Status:** TODO

### Risk

Incorrect bucket policies or public-access settings can expose sensitive objects.

### Recommended Action

Enable S3 Block Public Access and review bucket policies and object permissions.

### Priority

**High**

### Target Timeline

Within 1 week.

---

## Gap 5: S3 Encryption

**Responsibility:** Customer

**Risk:** High

**Status:** TODO

### Risk

Sensitive data stored without appropriate encryption increases the impact of unauthorized access.

### Recommended Action

Enable default encryption on appropriate S3 buckets and use AWS KMS where stronger key-management requirements exist.

### Priority

**High**

### Target Timeline

Within 1 week.

---

## Gap 6: RDS Encryption

**Responsibility:** Customer

**Risk:** High

**Status:** TODO

### Risk

Unencrypted database storage and snapshots may expose sensitive information if access controls fail.

### Recommended Action

Use an encrypted RDS database and manage encryption keys appropriately.

### Priority

**High**

### Target Timeline

Within 1 week.

---

## Gap 7: Security Group Review

**Responsibility:** Customer

**Risk:** High

**Status:** Review Needed

### Risk

Overly permissive security groups can expose EC2, ALB or database services to unauthorized network traffic.

Examples include SSH access from:

`0.0.0.0/0`

### Recommended Action

Review all inbound and outbound rules.

Only allow required traffic from trusted sources.

### Priority

**High**

### Target Timeline

Within 1 week.

---

# 4. Medium Priority Gaps

## Gap 8: S3 Versioning

**Risk:** Medium

**Status:** TODO

### Risk

Accidental deletion or overwriting of objects may result in data loss.

### Recommended Action

Enable versioning for important buckets.

---

## Gap 9: RDS Restore Testing

**Risk:** Medium

**Status:** TODO

### Risk

Having backups does not guarantee that the application can successfully recover from them.

### Recommended Action

Perform regular restore tests and document recovery procedures.

---

## Gap 10: CloudWatch Alarm Configuration

**Risk:** Medium

**Status:** TODO

### Risk

Security or availability problems may not be detected quickly without appropriate monitoring.

### Recommended Action

Create CloudWatch alarms for important application, infrastructure and security metrics.

---

## Gap 11: Application Dependency Management

**Risk:** Medium

**Status:** TODO

### Risk

Outdated Node.js packages may contain known vulnerabilities.

### Recommended Action

Regularly scan and update application dependencies.

---

## Gap 12: Application Logging

**Risk:** Medium

**Status:** TODO

### Risk

Insufficient logging makes security investigations and incident response difficult.

### Recommended Action

Centralize application logs in CloudWatch and configure appropriate retention.

---

# 5. Gap Prioritization

| Priority | Gap | Recommended Action |
|---|---|---|
| Critical | EC2 patching | Implement Systems Manager Patch Manager |
| Critical | IAM MFA | Enable MFA |
| Critical | Excessive IAM permissions | Implement least privilege |
| High | S3 public access | Enable Block Public Access |
| High | S3 encryption | Enable default encryption |
| High | RDS encryption | Enable encryption |
| High | Security groups | Restrict network access |
| Medium | S3 versioning | Enable versioning |
| Medium | RDS restore testing | Test recovery |
| Medium | CloudWatch alarms | Configure monitoring |
| Medium | Application dependencies | Patch dependencies |
| Medium | Application logging | Centralize logs |

---

# 6. Recommended Security Baseline

The following controls should be implemented as a minimum baseline:

1. Enable MFA.
2. Apply least-privilege IAM policies.
3. Patch EC2 operating systems.
4. Restrict security group access.
5. Enable S3 Block Public Access.
6. Enable S3 encryption.
7. Enable RDS encryption.
8. Configure RDS backups.
9. Test database restoration.
10. Enable appropriate CloudWatch logging and alarms.
11. Regularly patch application dependencies.
12. Review security configuration periodically.

