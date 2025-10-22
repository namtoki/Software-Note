# AWS

## Terminology
- ARN (Amazon Resource Name):
  - format: `arn:partition:service:region:account-id:resource-type/resource-id`
    - `arn:aws:s3:::my-bucket/file.txt`
    - `arn:aws:ec2:us-east-1:123456789012:instance/i-1234567890abcdef0`
    - `arn:aws:iam::123456789012:user/john`
      - partition: 通常は aws（中国リージョンは aws-cn、GovCloudは aws-us-gov）

## Account
- [Region] AWS Control Tower                ホームリージョンで管理しますが、複数のリージョンにまたがってガバナンスを適用できます
- [Global] AWS Organizations                複数アカウント
- [Global] AWS IAM                          (Identity and Access Management) User Groups, User, Roles

## Resource Management
- [Global] AWS Compute Optimizer            EC2, Auto Scaling Groups, EBS volumes, Lambda, Aurora, RDS, ECS on Fargate, 14日以上設定課金
- [Region] AWS Config                       「どのリソースが、いつ、どう変更されたか」を追跡, セキュリティとコンプライアンスのための構成監査
- [Region] AWS License Manager              ソフトウェアライセンスの使用量管理と制限, 「ライセンスを何個使っているか、超過していないか」を管理
- [Region] AWS Resource Access Manager      (RAM) マルチアカウント環境でリソースを効率的に共有し、重複を避ける

| AWS Service Catalog
| AWS Trusted Advisor
| AWS Well-Architected Tool
| Service Quotas

## Security & Compliance
| AWS Artifact
| AWS Audit Manager
| AWS Certificate Manager (ACM)
| AWS CloudHSM
| AWS Firewall Manager
| AWS Key Management Service (AWS KMS)
| AWS Secrets Manager
| AWS Security Hub
| Amazon Detective
| Amazon GuardDuty
| Amazon Inspector
| Amazon Macie

## Development & Deployment
| AWS Amplify
| AWS CLI
| AWS Management Console

## Identity & Access
| AWS Directory Service
| Amazon Cognito


## IaC
- AWS Cloud Development Kit (CDK)
- AWS CloudFormation

## PaaS
- AWS Elastic Beanstalk

## Organization
| Service | Where | Parameters | VPC | Security Group | IAM Role | Note |
| - | - | - | - | - | - | - |
| Budgets | Global | Budgets | - | - | - |  |


| AWS Systems Manager (SSM)
| AWS CodeBuild
| AWS CodePipeline

## Computing

| Service | Where | Parameters | VPC | Security Group | IAM Role | Note |
| - | - | - | - | - | - | - |
| EC2 | AZ | AMI, Instance Type, Key Pair, Instance Store, User Data  | ✔️| ✔️| ✔️|  |
| ECS | AZ | Image | ✔️| ✔️| ✔️| Elastic Container Service |
| + Instance Store | AZ |  | | | | Temporary |
| + EBS | AZ | Volume Type, Size, IOPS, Snapshot ID, Encryption | | | | Elastic Block Store |
| + Auto Scaling | Region | Auto Scaling Group (ASG), Scaling Policy | | | |  |
| + Image Builder | Region |  | | | |  |
| + Load Balancer | Region |  | ✔️| ✔️| |  |
| + Auto Scaling | Region |  | ✔️| ✔️| |  |
| + ECR |  |  |  |  | |  Elastic Container Registry |
| + EKS | Region | Cluster, Node Groups, Fargate Profiles | ✔️| ✔️| ✔️| Elastic Kubernetes Service - Managed Kubernetes |
| ★ Lambda | Region | Runtime, Memory, Timeout, Handler, Layers, Triggers | Optional | Optional | ✔️| Serverless compute - Event-driven, pay per invocation |
| Batch | Region | Job Definitions, Job Queues, Compute Environments, Scheduling Policies | ✔️| ✔️| ✔️| Managed batch processing - Runs jobs on EC2/Fargate/Spot |
| ★ API Gateway | Region | API Type (REST/HTTP/WebSocket), Stages, Integrations, Authorizers, Usage Plans | Optional | - | ✔️| Managed API service - Routing, throttling, auth, caching |
| Lightsail | Region | Instance Plans, Blueprints, Static IP, Snapshots, Load Balancer, Databases | VPC Peering | Firewall | Limited | Simplified VPS - Bundled compute, storage, networking with predictable pricing |

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
| RDS | Region | Engine (Aurora/MySQL/PostgreSQL/MariaDB/Oracle/SQL Server), Instance Class, Storage Type | ✔️ | ✔️ | ✔️ | Relational Database Service - Managed database |
| Aurora | Region | Engine (MySQL/PostgreSQL), Deployment (Provisioned/Serverless v2/Global), Instance Class, Replicas | ✔️ | ✔️ | ✔️ | Cloud-native relational DB, 5x MySQL/3x PostgreSQL performance |
| ElastiCache | Region | Engine (Redis/Memcached), Node Type, Number of Nodes, Cluster Mode | ✔️ | ✔️ | ✔️ | In-memory caching service for performance |
| DynamoDB | Region | Table Name, Primary Key (Partition/Sort), Capacity Mode (On-Demand/Provisioned), Global Tables | ✔️ | - | ✔️ | NoSQL key-value/document database |
| Redshift | Region | Cluster Type, Node Type, Number of Nodes, Database Name, Serverless/Provisioned | ✔️ | ✔️ | ✔️ | Petabyte-scale data warehouse for analytics |
| DocumentDB | Region | Cluster Configuration, Instance Class, Number of Replicas (up to 15), Storage Auto-Scaling | ✔️ | ✔️ | ✔️ | MongoDB-compatible document database |
| Neptune | Region | Cluster Configuration, Instance Class, Graph Model (Property/RDF), Query Language (Gremlin/SPARQL) | ✔️ | ✔️ | ✔️ | Graph database for highly connected data |
| EMR | Region | Cluster Configuration, Framework (Spark/Hadoop/Presto/Hive), Instance Types, Auto-Scaling | ✔️ | ✔️ | ✔️ | Elastic MapReduce - Big data processing platform |
| Athena | Region | Workgroup, Data Catalog, Query Result Location (S3) | - | - | ✔️ | Serverless SQL queries on S3 data |
| Glue | Region | Crawlers, Data Catalog, ETL Jobs, Job Triggers, Development Endpoints, DataBrew Recipes | ✔️ | ✔️ | ✔️ | Serverless ETL and data catalog service |
| DMS | Region | Replication Instance, Source/Target Endpoints, Migration Tasks, CDC, Multi-AZ | ✔️ | ✔️ | ✔️ | Database Migration Service |

## BI
| Service | Where | Parameters | VPC | Security Group | IAM Role | Note |
| - | - | - | - | - | - | - |
| QuickSight | Region | Dashboards, Datasets, SPICE Capacity, Edition (Standard/Enterprise) | ✔️ | - | ✔️ | Business intelligence and data visualization service |


## Monitoring
| Amazon CloudWatch
| Amazon EventBridge
| AWS CloudTrail
| AWS X-Ray
| AWS CodeGuru
| AWS Health Dashboard

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
| AWS PrivateLink
| AWS VPN
| AWS Site-to-Site VPN
| AWS Client VPN
| AWS Direct Connect
| AWS Transit Gateway

| AWS Shield
| AWS WAF

| AWS IAM Identity Center
| AWS Fargate
| AWS Cost and Usage Reports
| AWS Cost Explorer

---

## AI/ML & Natural Language
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

## Migration Services
| AWS Application Discovery Service
| AWS Application Migration Service
| AWS Migration Hub
| AWS Schema Conversion Tool (AWS SCT)
| Migration Evaluator

## End-User Computing
| Amazon AppStream 2.0
| Amazon WorkSpaces
| Amazon WorkSpaces Secure Browser

## Disaster Recovery & Backup
| AWS Backup
| AWS Elastic Disaster Recovery

## API & Integration
| AWS AppSync
| AWS Step Functions

## Communication
| Amazon Simple Email Service (Amazon SES)
| Amazon Connect

## Other
| AWS IoT Core
| AWS Marketplace
| AWS Support
| Amazon OpenSearch Service
