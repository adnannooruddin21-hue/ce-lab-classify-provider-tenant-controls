# AWS Resource Inventory

## AWS Account and Region

- AWS Account: `128529977749`
- Primary CLI Region: `eu-north-1`

## Compute

No EC2 instances were returned by the current AWS CLI query.

- EC2 Instances: None currently detected

## Database

No RDS database instances were returned by the current AWS CLI query.

- RDS PostgreSQL: None currently detected

## Storage

The following S3 buckets were detected:

- `aws-config-bucket-1787621054`
- `ce-lab-archive-268717`
- `ce-lab-logs-268717`
- `m8-lab1-assets-193281220051-us-east-1`

## Networking

### VPC

- VPC ID: `vpc-048d7048bd382d006`
- CIDR: `172.31.0.0/16`
- Type: Default VPC

### Security Group

- Security Group ID: `sg-0abfbb4cc84203b8b`
- Name: `default`
- VPC: `vpc-048d7048bd382d006`

## IAM Roles

Relevant IAM roles detected include:

- `m8-lab1-ec2-app-role`
- `LambdaExecutionRole`
- `CloudWatchAgentRole`
- `FinOpsLambdaRole`
- `flowlogsRole`
- `Grafana`
- `Grafana-Role`
- `InsecureAppRole`
- `InstanceSchedulerRole`
- `AWSServiceRoleForConfig`
- `AWSServiceRoleForRDS`
- `AWSServiceRoleForElasticLoadBalancing`
- `AWSServiceRoleForAmazonGuardDuty`
- `AWSServiceRoleForAmazonInspector2`
- `AWSServiceRoleForSecurityHub`
- `AWSServiceRoleForComputeOptimizer`

## AWS Security and Monitoring Services

The account also contains service-linked roles associated with:

- AWS Config
- Amazon GuardDuty
- Amazon Inspector
- AWS Security Hub
- AWS Compute Optimizer
- IAM Access Analyzer
- Elastic Load Balancing
- Amazon RDS