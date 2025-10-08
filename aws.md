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
| ECS | AZ | Image | ✔️| ✔️| ✔️| Elastic Container Service |
| + ECR |  |  |  |  | |  Elastic Container Registry |

| Amazon Elastic File System (Amazon EFS)

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

| Amazon Elastic Kubernetes Service (Amazon EKS)
| Amazon API Gateway
| AWS Batch
| Amazon Lightsail
| Amazon Aurora
| Amazon DocumentDB
| Amazon DynamoDB
| Amazon ElastiCache
| Amazon Neptune
| Amazon RDS
| AWS Glue
| Amazon QuickSight
| Amazon Redshift
| Amazon Athena
| Amazon S3
| Amazon S3 Glacier
| AWS Storage Gateway
| AWS IAM Identity Center
| AWS Fargate
| AWS Lambda
| AWS Cost and Usage Reports
| AWS Cost Explorer

---

| Amazon EMR
| Amazon OpenSearch Service
| Amazon EventBridge
| AWS Step Functions
| Amazon Connect
| Amazon Simple Email Service (Amazon SES)
| AWS Marketplace
| AWS Support
| AWS CLI
| AWS X-Ray
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
| AWS CloudTrail
| Amazon CloudWatch
| AWS Compute Optimizer
| AWS Config
| AWS Control Tower
| AWS Health Dashboard
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
| AWS Snow Family
| AWS Direct Connect
| AWS PrivateLink
| AWS Transit Gateway
| Amazon VPC
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
| Amazon FSx
