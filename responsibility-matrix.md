
# AWS Security Responsibility Matrix

## 1. Introduction

This document classifies security controls according to the AWS Shared Responsibility Model.

The lab scenario consists of a three-tier web application:

- Web tier: Application Load Balancer and EC2
- Application tier: EC2 instances running Node.js
- Data tier: Amazon RDS PostgreSQL
- Supporting services: Amazon S3, VPC, IAM, CloudWatch

AWS is responsible for security **of** the cloud, including the physical infrastructure, facilities, networking infrastructure, and managed-service infrastructure.

The customer is responsible for security **in** the cloud, including identity and access management, data, applications, guest operating systems where applicable, network configuration, and service-specific security settings.

---

# 2. Service Model Classification

| Service | Service Model | Customer Responsibility |
|---|---|---|
| Amazon EC2 | IaaS | Guest OS, applications, data, IAM, network configuration |
| Amazon RDS PostgreSQL | PaaS / Managed Database | Database configuration, data, access control, encryption configuration |
| Amazon S3 | Managed Cloud Storage | Data, bucket policies, access control, encryption configuration |
| Application Load Balancer | Managed Networking Service | Listeners, routing, TLS configuration, security groups |
| AWS Lambda | FaaS / Serverless | Function code, dependencies, IAM permissions, environment variables |
| Amazon VPC | Managed Networking Service | VPC architecture, subnets, routes, security groups, NACLs |
| IAM | Managed Identity Service | Users, roles, policies, MFA, credentials |
| CloudWatch | Managed Monitoring Service | Logs, metrics, alarms, dashboards and retention configuration |

---

# 3. Security Responsibility Matrix

| # | Control | Service | AWS Responsibility | Customer Responsibility | Status |
|---|---|---|---|---|---|
| 1 | Physical data center security | All | Secure AWS facilities, buildings and physical access | None | AWS Managed |
| 2 | Physical hardware security | EC2 | Protect and maintain physical servers | None | AWS Managed |
| 3 | Physical network infrastructure | VPC | Operate and protect underlying networking infrastructure | None | AWS Managed |
| 4 | Hypervisor security | EC2 | Maintain and secure the virtualization layer | None | AWS Managed |
| 5 | EC2 guest OS patching | EC2 | None | Install security patches and updates | TODO |
| 6 | EC2 OS hardening | EC2 | None | Harden operating system configuration | TODO |
| 7 | EC2 antivirus / endpoint protection | EC2 | Provide underlying infrastructure | Configure endpoint protection where required | TODO |
| 8 | Application security | EC2 | None | Secure Node.js application and dependencies | TODO |
| 9 | Application dependency updates | EC2 | None | Update vulnerable packages and libraries | TODO |
| 10 | EC2 IAM instance role | EC2/IAM | Provide IAM infrastructure | Configure least-privilege role policies | Review Needed |
| 11 | Security groups | VPC/EC2 | Provide network security functionality | Configure inbound and outbound rules | Review Needed |
| 12 | Network ACLs | VPC | Provide NACL functionality | Configure appropriate rules | Review Needed |
| 13 | VPC architecture | VPC | Operate networking infrastructure | Design VPC, subnets and routing | Customer Managed |
| 14 | Route tables | VPC | Provide routing infrastructure | Configure routes | Customer Managed |
| 15 | Internet gateway configuration | VPC | Provide Internet Gateway infrastructure | Attach/configure it appropriately | Customer Managed |
| 16 | DDoS protection | AWS Shield | Shield Standard infrastructure protection | Configure additional protections if required | Review Needed |
| 17 | IAM user access | IAM | Maintain IAM service | Create and manage appropriate users | Review Needed |
| 18 | IAM least privilege | IAM | Provide IAM policy engine | Apply least-privilege permissions | TODO |
| 19 | IAM MFA | IAM | Provide MFA capability | Enable MFA for human users | TODO |
| 20 | IAM access key management | IAM | Secure IAM infrastructure | Rotate, protect and remove unused keys | TODO |
| 21 | IAM role permissions | IAM | Provide IAM role infrastructure | Configure role policies | Review Needed |
| 22 | RDS physical infrastructure | RDS | Manage database infrastructure | None | AWS Managed |
| 23 | RDS operating system patching | RDS | Patch underlying managed OS | None | AWS Managed |
| 24 | RDS database engine patching | RDS | Provide database engine maintenance | Select maintenance windows and test updates | AWS/Customer Shared |
| 25 | RDS database access | RDS | Provide database service | Configure users, passwords and access controls | Customer Managed |
| 26 | RDS encryption at rest | RDS | Provide encryption/KMS infrastructure | Enable encryption and manage keys | TODO |
| 27 | RDS network security | RDS/VPC | Provide networking infrastructure | Configure private subnets and security groups | Review Needed |
| 28 | RDS backups | RDS | Provide backup functionality | Configure retention and verify recovery | TODO |
| 29 | RDS restore testing | RDS | Provide restore functionality | Periodically test restoration | TODO |
| 30 | S3 storage infrastructure | S3 | Maintain durability, redundancy and infrastructure | None | AWS Managed |
| 31 | S3 encryption at rest | S3 | Provide encryption infrastructure | Configure default encryption and keys where required | TODO |
| 32 | S3 bucket policies | S3 | Provide policy enforcement mechanism | Configure secure bucket policies | Review Needed |
| 33 | S3 Block Public Access | S3 | Provide Block Public Access functionality | Enable and verify settings | TODO |
| 34 | S3 object permissions | S3 | Provide access-control infrastructure | Control access to objects | TODO |
| 35 | S3 versioning | S3 | Provide versioning functionality | Enable versioning for important data | TODO |
| 36 | S3 lifecycle management | S3 | Provide lifecycle functionality | Configure retention and deletion policies | Review Needed |
| 37 | ALB infrastructure | ALB | Operate load-balancer infrastructure | None | AWS Managed |
| 38 | ALB security groups | ALB/VPC | Provide security-group infrastructure | Restrict allowed traffic | TODO |
| 39 | ALB listeners | ALB | Provide listener functionality | Configure listeners correctly | TODO |
| 40 | ALB TLS configuration | ALB/ACM | Provide TLS/ACM infrastructure | Select and configure certificates | TODO |
| 41 | ALB routing | ALB | Provide routing functionality | Configure target groups and routing | Customer Managed |
| 42 | Lambda infrastructure | Lambda | Manage servers, OS and runtime infrastructure | None | AWS Managed |
| 43 | Lambda function code | Lambda | None | Secure function code | TODO |
| 44 | Lambda dependencies | Lambda | Maintain managed runtime infrastructure | Update application dependencies | TODO |
| 45 | Lambda execution role | Lambda/IAM | Provide IAM service | Configure least-privilege permissions | TODO |
| 46 | CloudWatch infrastructure | CloudWatch | Operate monitoring infrastructure | None | AWS Managed |
| 47 | CloudWatch log configuration | CloudWatch | Provide logging platform | Configure log groups and retention | TODO |
| 48 | CloudWatch alarms | CloudWatch | Provide monitoring functionality | Configure appropriate alarms | TODO |
| 49 | Security logging | CloudWatch/CloudTrail | Provide logging infrastructure | Enable and monitor relevant events | TODO |
| 50 | Security monitoring | CloudWatch/Security Hub | Provide security services | Review findings and respond to incidents | TODO |

---

# 4. Responsibility by Application Tier

## Web Tier

The web tier consists of:

- Application Load Balancer
- EC2 instances
- Security groups
- TLS certificates

### AWS Responsibilities

- Physical infrastructure
- Hardware
- Hypervisor
- Underlying networking
- ALB managed infrastructure

### Customer Responsibilities

- EC2 operating system
- OS patching
- Application security
- Security group configuration
- ALB listeners
- TLS configuration
- Routing
- IAM permissions

---

## Application Tier

The application tier consists of:

- EC2 instances
- Node.js application
- IAM roles
- Security groups

### AWS Responsibilities

- Physical infrastructure
- Hardware
- Hypervisor
- Underlying AWS networking

### Customer Responsibilities

- Operating system
- OS patches
- Node.js application
- Application dependencies
- Application secrets
- IAM permissions
- Security groups
- Logging and monitoring

---

## Data Tier

The data tier consists of:

- RDS PostgreSQL
- Private subnets
- Security groups
- Backups
- Encryption

### AWS Responsibilities

- Physical infrastructure
- Database service infrastructure
- Managed operating system
- Database service availability
- Database engine maintenance mechanisms

### Customer Responsibilities

- Database access configuration
- Database users
- Passwords
- Network access
- Encryption configuration
- Backup retention configuration
- Restore testing
- Data protection

---

# 5. Summary

The assessment identified more than 20 security controls across:

- Physical security
- Compute
- Networking
- IAM
- Database security
- Storage security
- Load balancing
- Serverless computing
- Monitoring and logging

The customer remains responsible for configuring and securely operating the services that AWS provides.
