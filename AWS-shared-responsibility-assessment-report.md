
# AWS Shared Responsibility Assessment Report

## 1. Executive Summary

This report evaluates the security responsibilities for a three-tier web application deployed on Amazon Web Services.

The application architecture consists of:

- Application Load Balancer
- EC2 instances in the web tier
- EC2 instances running Node.js in the application tier
- Amazon RDS PostgreSQL in the data tier
- Amazon S3 for object storage
- Amazon VPC for networking
- IAM for identity and access management
- CloudWatch for monitoring and logging

The assessment uses the AWS Shared Responsibility Model to identify which security controls are managed by AWS and which must be configured and maintained by the customer.

The assessment identified several important customer responsibilities, including operating system patching, IAM security, network configuration, S3 access control, encryption, application security, logging and backup management.

---

# 2. Architecture Overview

## Web Tier

The web tier contains:

- Application Load Balancer
- EC2 instances
- Security groups
- TLS configuration

The ALB receives external traffic and forwards requests to the application infrastructure.

## Application Tier

The application tier contains:

- EC2 instances
- Node.js application
- IAM roles
- Security groups

The application tier processes requests received from the web tier.

## Data Tier

The data tier contains:

- Amazon RDS PostgreSQL
- Private subnets
- Database security groups
- Automated backups
- Encryption

The database should not be directly accessible from the public Internet.

---

# 3. AWS Resource Inventory

The current AWS account inventory contains:

## S3

- `aws-config-bucket-1787621054`
- `ce-lab-archive-268717`
- `ce-lab-logs-268717`
- `m8-lab1-assets-193281220051-us-east-1`

The buckets were identified using the AWS CLI.

The `get-bucket-location` command returned `None` for each bucket, which represents the `us-east-1` region for S3.

## Networking

VPC:

- ID: `vpc-048d7048bd382d006`
- CIDR: `172.31.0.0/16`
- Default VPC: Yes

Security Group:

- ID: `sg-0abfbb4cc84203b8b`
- Name: `default`
- VPC: `vpc-048d7048bd382d006`

## IAM

Relevant IAM roles include:

- `m8-lab1-ec2-app-role`
- `LambdaExecutionRole`
- `CloudWatchAgentRole`
- `FinOpsLambdaRole`
- `flowlogsRole`
- `InsecureAppRole`
- `InstanceSchedulerRole`
- `AWSServiceRoleForConfig`
- `AWSServiceRoleForRDS`
- `AWSServiceRoleForElasticLoadBalancing`

## EC2

No EC2 instances were returned by the current AWS CLI query.

## RDS

No RDS database instances were returned by the current AWS CLI query.

The three-tier EC2/RDS architecture described in this report therefore represents the architecture specified by the lab scenario.

---

# 4. Service Model Classification

| Service | Model | Responsibility Level |
|---|---|---|
| EC2 | IaaS | High customer responsibility |
| RDS PostgreSQL | PaaS / Managed Database | Medium customer responsibility |
| S3 | Managed Cloud Storage | Medium customer responsibility |
| ALB | Managed Networking Service | Lower customer infrastructure responsibility |
| Lambda | FaaS / Serverless | Customer manages code and configuration |
| VPC | Managed Networking Service | Customer manages network configuration |
| IAM | Managed Identity Service | Customer manages identities and permissions |
| CloudWatch | Managed Monitoring Service | Customer configures monitoring |

---

# 5. Shared Responsibility Model

## AWS Responsibilities

AWS is responsible for security of the underlying cloud infrastructure.

Examples include:

- Physical data centers
- Physical security
- Hardware
- Networking infrastructure
- Hypervisor
- Managed service infrastructure
- RDS underlying operating system
- S3 storage infrastructure
- Lambda infrastructure
- ALB infrastructure

## Customer Responsibilities

The customer is responsible for security within the cloud.

Examples include:

- IAM users and roles
- IAM policies
- MFA
- EC2 guest operating system
- Application code
- Application dependencies
- Security groups
- Network ACLs
- S3 bucket policies
- S3 public access configuration
- Encryption configuration
- RDS access controls
- Database users
- Backup configuration
- Logging and monitoring configuration

---

# 6. Major Security Findings

The following security gaps were identified.

### 1. EC2 Operating System Patching

The customer must patch and harden EC2 guest operating systems.

### 2. IAM MFA

MFA should be enabled for human users.

### 3. IAM Least Privilege

IAM policies should grant only the permissions required to perform a task.

### 4. S3 Public Access

S3 Block Public Access should be enabled unless public access is explicitly required.

### 5. S3 Encryption

Sensitive S3 data should use appropriate encryption.

### 6. RDS Encryption

Sensitive database data should be encrypted at rest.

### 7. Security Groups

Security groups should allow only required network traffic.

### 8. Backup and Recovery

RDS backups should be configured and restoration should be tested periodically.

### 9. Application Security

Node.js dependencies and application code should be regularly reviewed and patched.

### 10. Monitoring

CloudWatch logging and alarms should be configured for security and operational visibility.

---

# 7. Recommendations

## Immediate

1. Enable MFA.
2. Review IAM policies.
3. Remove unnecessary permissions.
4. Enable S3 Block Public Access.
5. Review security group rules.

## Short Term

6. Enable S3 encryption.
7. Enable RDS encryption.
8. Implement EC2 patch management.
9. Configure CloudWatch logging.
10. Configure CloudWatch alarms.

## Medium Term

11. Enable S3 versioning for important data.
12. Test RDS restoration.
13. Implement dependency vulnerability scanning.
14. Review application security.
15. Perform periodic IAM and network security reviews.

---

# 8. Security Improvement Timeline

| Time | Action |
|---|---|
| Day 1 | Enable MFA |
| Day 1-2 | Review IAM permissions |
| Day 1-2 | Review security groups |
| Day 3 | Enable S3 Block Public Access |
| Day 3 | Enable S3 encryption |
| Week 1 | Implement EC2 patch management |
| Week 1 | Configure CloudWatch monitoring |
| Week 2 | Configure and test RDS backup/recovery |
| Week 2 | Review application dependencies |
| Monthly | Security configuration review |

---

# 9. Conclusion

The AWS Shared Responsibility Model divides security responsibilities between AWS and the customer.

AWS protects the infrastructure and services that run the cloud, while the customer must securely configure and operate the services they use.

The most important customer responsibilities identified in this assessment are IAM security, operating system patching, network security, data protection, encryption, application security, backup management and monitoring.

Implementing the recommended controls will significantly reduce the risk of unauthorized access, data exposure, configuration errors and security incidents.

---

# 10. References

- AWS Shared Responsibility Model
- AWS Security Best Practices
- AWS Identity and Access Management documentation
- Amazon EC2 security documentation
- Amazon S3 security documentation
- Amazon RDS security documentation
- Amazon VPC security documentation
- Amazon CloudWatch documentation
