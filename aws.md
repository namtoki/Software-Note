# AWS

## Terminology
- ARN (Amazon Resource Name):
  - format: `arn:partition:service:region:account-id:resource-type/resource-id`
    - `arn:aws:s3:::my-bucket/file.txt`
    - `arn:aws:ec2:us-east-1:123456789012:instance/i-1234567890abcdef0`
    - `arn:aws:iam::123456789012:user/john`
      - partition: 通常は aws（中国リージョンは aws-cn、GovCloudは aws-us-gov）

## Organization
| Service | Where | Parameters | VPC | Security Group | IAM Role | Note |
| - | - | - | - | - | - | - |
| IAM | Global | User Groups, User, Roles,,, | - | - | - | AWS Identity and Access Management |
| Budgets | Global | Budgets | - | - | - |  |

## Instance

| Service | Where | Parameters | VPC | Security Group | IAM Role | Note |
| - | - | - | - | - | - | - |
| EC2 | AZ | AMI, Instance Type, Key Pair, Instance Store, User Data  | ✔️| ✔️| ✔️|  |
| + Instance Store | AZ |  | | | | Temporary |
| + EBS | AZ | Volume Type, Size, IOPS, Snapshot ID, Encryption | | | | Elastic Block Store |
| + Auto Scaling | Region | Auto Scaling Group (ASG), Scaling Policy | | | |  |
| + Image Builder | Region |  | | | |  |
| + Load Balancer | Region |  | ✔️| ✔️| |  |
| + Auto Scaling | Region |  | ✔️| ✔️| |  |
| ECS | AZ | Image | ✔️| ✔️| ✔️| Elastic Container Service |
| + ECR |  |  |  |  | |  Elastic Container Registry |

## Storage
| Service | Where | Parameters | VPC | Security Group | IAM Role | Note |
| - | - | - | - | - | - | - |
| FSx | AZ | Capacity | ✔️| ✔️|  | Amazon FSx |
| EFS | AZ | Auto-Scaling | ✔️| ✔️|  | Amazon Elastic File System |
| S3 | Region | Bucket Name, Versioning, Encryption, Storage Class | - | - | Bucket Policy | Simple Storage Service |
| S3 Glacier | Region | Vault Name, Archive, Retrieval Options | - | - | Vault Access Policy | Long-term archival storage |
| + Snowcone | Physical | 8-14 TB Storage, 2 vCPUs, 4 GB Memory | - | - | - | Smallest device, edge computing, 9 lbs |
| + Snowball Edge Storage | Physical | 80 TB Storage, 40 vCPUs, 80 GB Memory | - | - | - | Large data migrations |
| + Snowball Edge Compute | Physical | 28 TB NVMe, 104 vCPUs, 416 GB Memory, GPU | - | - | - | ML, video processing |
| + Snowmobile | Physical | 100 PB per truck | - | - | - | Exabyte-scale migrations, 45-ft container |
| + Storage Gateway | Hybrid | Gateway Type (File/FSx/Volume/Tape) | ✔️ | ✔️ | ✔️ | Bridge on-premises to AWS storage (S3/FSx/EBS/Glacier) |

| Amazon RDS
| Amazon ElastiCache
| Amazon DynamoDB
| Amazon Redshift
| Amazon EMR
| Amazon Athena
| Amazon QuickSight
| Amazon DocumentDB
| Amazon Neptune
| AWS Glue

| Amazon Aurora

## Monitoring
| Amazon CloudWatch
| Amazon EventBridge
| AWS CloudTrail
| AWS X-Ray
| AWS CodeGuru
| AWS Health Dashboard

## Deployment
AWS Cloud Development Kit (CDK)
| AWS CloudFormation
| AWS Elastic Beanstalk    PaaS
| AWS Systems Manager (SSM)
| AWS CodeBuild
| AWS CodePipeline

## Global
| Amazon Route 53
| Amazon CloudFront
| AWS Global Accelerator
| AWS Outposts
| AWS WaveLength
| AWS Local Zones

## Comm
| Amazon Simple Queue Service (Amazon SQS)
| Amazon Kinesis
| Amazon Simple Notification Service (Amazon SNS)
| Amazon MQ

| Amazon VPC

| Amazon Elastic Kubernetes Service (Amazon EKS)
| Amazon API Gateway
| AWS Batch
| Amazon Lightsail
| AWS IAM Identity Center
| AWS Fargate
| AWS Lambda
| AWS Cost and Usage Reports
| AWS Cost Explorer

---

| Amazon OpenSearch Service
| AWS Step Functions
| Amazon Connect
| Amazon Simple Email Service (Amazon SES)
| AWS Marketplace
| AWS Support
| AWS CLI
| Amazon AppStream 2.0
| Amazon WorkSpaces
| Amazon WorkSpaces Secure Browser
| AWS Amplify
| AWS AppSync
| AWS IoT Core
| Amazon Comprehend
| Amazon Kendra
| Amazon Lex
| Amazon Polly
| Amazon Q
| Amazon Rekognition
| Amazon SageMaker AI
| Amazon Textract
| Amazon Transcribe
| Amazon Translate
| AWS Compute Optimizer
| AWS Config
| AWS Control Tower
| AWS License Manager
| AWS Management Console
| AWS Organizations
| AWS Service Catalog
| Service Quotas
| AWS Trusted Advisor
| AWS Well-Architected Tool
| AWS Application Discovery Service
| AWS Application Migration Service
| AWS Database Migration Service (AWS DMS)
| Migration Evaluator
| AWS Migration Hub
| AWS Schema Conversion Tool (AWS SCT)
| AWS Direct Connect
| AWS PrivateLink
| AWS Transit Gateway
| AWS VPN
| AWS Site-to-Site VPN
| AWS Client VPN
| AWS Artifact
| AWS Audit Manager
| AWS Certificate Manager (ACM)
| AWS CloudHSM
| Amazon Cognito
| Amazon Detective
| AWS Directory Service
| AWS Firewall Manager
| Amazon GuardDuty
| Amazon Inspector
| AWS Key Management Service (AWS KMS)
| Amazon Macie
| AWS Resource Access Manager (AWS RAM)
| AWS Secrets Manager
| AWS Security Hub
| AWS Shield
| AWS WAF
| AWS Backup
| AWS Elastic Disaster Recovery

---

  1. Serverless Architecture (Most Common for Modern Apps)

  Mobile App
      ↓ (HTTPS/REST)
  Amazon API Gateway
      ↓
  AWS Lambda Functions
      ↓
  ├─→ Amazon RDS/Aurora (relational data)
  ├─→ DynamoDB (NoSQL data)
  ├─→ S3 (file storage)
  ├─→ ElastiCache (caching)
  └─→ Other AWS Services

  Key Components:
  - API Gateway: Entry point, handles routing, throttling, authentication
  - Lambda: Serverless compute for business logic
  - DynamoDB/RDS: Data persistence
  - S3: Media/file storage
  - Cognito: User authentication/authorization
  - CloudFront: CDN for static assets
  - SQS/SNS: Async messaging and notifications

  Advantages:
  - Pay per request (cost-effective)
  - Auto-scaling
  - No server management
  - High availability built-in

  2. Container-based Microservices

  Mobile App
      ↓ (HTTPS/REST)
  Application Load Balancer
      ↓
  ECS/EKS (Docker containers)
      ↓
  ├─→ Microservice 1 (User Service)
  ├─→ Microservice 2 (Content Service)
  ├─→ Microservice 3 (Payment Service)
      ↓
  RDS/DynamoDB/S3

  Key Components:
  - ECS/EKS: Container orchestration
  - ALB: Load balancing
  - ECR: Container registry
  - RDS/Aurora: Database clusters
  - ElastiCache: Redis/Memcached for caching

  Use when: Higher traffic, complex services, need more control

  3. Hybrid Architecture (Very Common)

  Combines serverless for lightweight operations with containers for heavier
  workloads:

  Mobile App
      ↓
  API Gateway + ALB
      ↓
  ├─→ Lambda (auth, simple CRUD)
  └─→ ECS/Fargate (complex processing, long-running tasks)
      ↓
  Shared data layer (RDS, DynamoDB, S3)

  Common Patterns Across All Architectures:

  Security Layer:
  - WAF (Web Application Firewall)
  - Cognito User Pools or custom auth
  - IAM roles and policies
  - Secrets Manager for credentials

  Observability:
  - CloudWatch (logs, metrics, alarms)
  - X-Ray (distributed tracing)
  - CloudTrail (audit logs)

  Data Layer:
  - Primary DB: RDS (PostgreSQL/MySQL) or Aurora
  - NoSQL: DynamoDB for high-scale key-value data
  - Cache: ElastiCache (Redis)
  - Storage: S3 for media files

  Additional Services:
  - SES (email)
  - SNS (push notifications via FCM/APNS)
  - SQS (job queues)
  - EventBridge (event-driven workflows)

  Best Practice: Multi-Environment Setup

