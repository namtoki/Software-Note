# AWS

## Terminology
- AWS Management Console
- ARN (Amazon Resource Name):
  - format: `arn:partition:service:region:account-id:resource-type/resource-id`
    - `arn:aws:s3:::my-bucket/file.txt`
    - `arn:aws:ec2:us-east-1:123456789012:instance/i-1234567890abcdef0`
    - `arn:aws:iam::123456789012:user/john`
      - partition: 通常は aws（中国リージョンは aws-cn、GovCloudは aws-us-gov）

## Account
- [Region] AWS Control Tower                ホームリージョンで管理しますが、複数のリージョンにまたがってガバナンスを適用できます
- [Global] AWS Organizations                複数アカウント
- [Global] AWS IAM Identity Center          シングルサインオン (SSO), マルチアカウント管理
- [Global] AWS IAM                          (Identity and Access Management) User Groups, User, Roles

## Cost & Budgets
- [Global] AWS Cost and Usage Reports
- [Global] AWS Cost Explorer

## Compliance
- [Global] AWS Artifact                     AWS のコンプライアンス関連ドキュメントへのセルフサービスアクセスを提供するサービス
- [Global] AWS Audit Manager                監査準備とコンプライアンス評価を自動化・簡素化するサービス

## CLI & IaC
- [Region] AWS CLI
- [Region] AWS Cloud Development Kit (CDK)
- [Region] AWS CloudFormation
- [Region] AWS Systems Manager (SSM)        AWSとオンプレミスのインフラストラクチャを一元的に管理・運用するための統合サービス
- [Region] AWS CodeBuild                    ソースコードをコンパイル、テスト実行し、デプロイ可能なソフトウェアパッケージを生成する CI サービス
- [Region] AWS CodePipeline                 ソフトウェアのリリースプロセスを自動化するフルマネージドな継続的デリバリー（CD）サービス
⏺ [Region] AWS Step Functions               複数の AWS サービスを組み合わせて、ワークフローを構築・管理するためのサーバーレスオーケストレーションサービス

## Resource Management
## Support
- [Global] AWS Support                      インフラ、サービスの利用方法、トラブルシューティング、アーキテクチャガイダンスなど、様々なレベルのサポートを提供
### 最適化提案
- [Global] AWS Compute Optimizer            EC2, Auto Scaling Groups, EBS volumes, Lambda, Aurora, RDS, ECS on Fargate, 14日以上設定課金
### 監査
- [Global] AWS Trusted Advisor              AWSのベストプラクティスに基づいてアカウントを分析し、改善提案を行う自動アドバイザリーサービス
- [Global] AWS Well-Architected Tool        AWSワークロードをWell-Architectedフレームワークに基づいて評価・改善するための無料のセルフサービスツール
- [Region] AWS Config                       「どのリソースが、いつ、どう変更されたか」を追跡, セキュリティとコンプライアンスのための構成監査
- [Region] AWS License Manager              ソフトウェアライセンスの使用量管理と制限, 「ライセンスを何個使っているか、超過していないか」を管理
### 統制＆コントロール
- [Region] AWS Resource Access Manager      (RAM) マルチアカウント環境でリソースを効率的に共有し、重複を避ける
- [Region] AWS Service Catalog              組織で承認されたAWSリソース（CloudFormationテンプレート）をカタログとして提供
- [Region] Service Quotas                   AWSサービスのクォータ（制限値）を一元管理・表示・引き上げリクエストできるサービス
### BaaS
- [Region] AWS Amplify                      フロントエンド開発者がフルスタックアプリを構築できるようにする統合プラットフォーム
### PaaS
- [Region] AWS Elastic Beanstalk
### Store
⏺ [Global] AWS Marketplace                  AWS 上で実行する Software を検索/購入/Deploy できるデジタルカタログ。サードパーティベンダー製品を簡単に調達・利用
### BI
- [Region] QuickSight                       Business intelligence and data visualization service |
### Backup
⏺ [Region] AWS Elastic Disaster Recovery    (AWS DRS) 物理、仮想、Cloud Base Server を AWS に継続的にレプリケートし、迅速な災害復旧を実現するマネージドサービス

## Monitoring
⏺ [Region] Amazon OpenSearch Service        AWSが提供するフルマネージド型の検索・分析サービス。OpenSearch, Elasticsearchをベースにした検索・分析エンジン

## Identity & Access
- [Region] AWS Directory Service            Microsoft Active Directory（AD）の機能を AWS クラウド内で提供するマネージドサービス
- [Region] Amazon Cognito                   Web/Mobile Application にユーザー認証・認可機能を簡単に追加できるマネージドサービス

## Localization
- [-] AWS Outposts                          On-premises
- [-] AWS Local Zones                       AWS サービスを主要都市圏の近くに配置するインフラストラクチャ
- [-] AWS Wavelength                        AWSのコンピューティングとストレージサービスを5G通信事業者のネットワークエッジに組み込むサービス

## Global Player
- [Global] Amazon Route 53
- [Global] Amazon CloudFront
- [Global] Global Accelerator               TCP/UDPトラフィック向け、非HTTPアプリケーション対応
- [Global] AWS Shield                       DDoS
- [Global] AWS WAF                          (Web Application Firewall) SQLインジェクション、クロスサイトスクリプティング（XSS）、DDoS攻撃など

## Regional Networking
- [Region] Amazon VPC
- [Region] AWS PrivateLink                  AWSサービス/VPC間のプライベート接続
- [Region] AWS Site-to-Site VPN             オンプレミス⇔ AWS VPC
- [Region] AWS Direct Connect               オンプレミス⇔ AWS専用線 (専用物理回線)
- [Region] AWS Client VPN                   リモートユーザー(個人デバイス) ⇔ AWS VPC
- [Region] AWS Transit Gateway              複数のVPC、VPN、Direct Connectを相互接続するハブ。ネットワークトポロジーを簡素化

## Inter-Communication
- [Region] Amazon SQS                       (Amazon Simple Queue Service)
- [Region] Amazon SNS                       (Amazon Simple Notification Service)
- [Region] Amazon MQ                        Apache ActiveMQ とRabbitMQ のマネージド型メッセージブローカーサービス
- [Region] Amazon Kinesis                   リアルタイムのストリーミングデータを収集、処理、分析するための完全マネージド型サービス

## Computing
- [Region] EC2                              AMI, Instance Type, Key Pair, Instance Store, User Data
  - Instance Store                        Temporary
  - Auto Scaling                          Auto Scaling Group (ASG), Scaling Policy
  - Image Builder
  - Load Balancer
  - Auto Scaling
- [Region] AWS Fargate                      サーバーレスなコンテナ実行環境を提供するAWSのコンピューティングエンジン
- [Region] ECS                              (Elastic Container Service)
  - ECR                                   (Elastic Container Registry)
  - EKS                                   (Elastic Kubernetes Service - Managed Kubernetes) Cluster, Node Groups, Fargate Profiles
- [Region] EBS                              (Elastic Block Store) Volume Type, Size, IOPS, Snapshot ID, Encryption
- [Region] Lambda                           Runtime, Memory, Timeout, Handler, Layers, Triggers
- [Region] Batch                            Managed batch processing - Runs jobs on EC2/Fargate/Spot
- [Region] Lightsail                        Simplified VPS - Bundled compute, storage, networking with predictable pricing

## Storage
- [AZ] Amazon FSx                           Capacity
- [AZ] Amazon EFS                           (Elastic File System) Auto-Scaling
- [Region] Amazon S3                        (Simple Storage Service) Bucket Name, Versioning, Encryption, Storage Class
- [Region] Amazon S3 Glacier                Long-term archival storage, Vault Name, Archive, Retrieval Options
- [Region] Amazon Macie                     Amazon S3内の機密データを自動的に検出・分類・保護
- [Physical] AWS Snowcone                   8-14 TB Storage, 2 vCPUs, 4 GB Memory, Smallest device, edge computing, 9 lbs
- [Physical] AWS Snowball Edge Storage      80 TB Storage, 40 vCPUs, 80 GB Memory, Large data migrations
- [Physical] AWS Snowball Edge Compute      28 TB NVMe, 104 vCPUs, 416 GB Memory, GPU, ML, video processing
- [Physical] AWS Snowmobile                 100 PB per truck, Exabyte-scale migrations, 45-ft container
- [Hybrid] AWS Storage Gateway              Bridge on-premises to AWS storage (S3/FSx/EBS/Glacier), Gateway Type (File/FSx/Volume/Tape)
- [Region] Amazon RDS                       (Relational Database Service) Engine (Aurora/MySQL/PostgreSQL/MariaDB/Oracle/SQL Server), Instance Class, Storage Type
- [Region] Amazon Aurora                    Cloud-native relational DB, 5x MySQL/3x PostgreSQL performance, Engine (MySQL/PostgreSQL), Deployment (Provisioned/Serverless v2/Global)
- [Region] Amazon ElastiCache               In-memory caching service for performance, Engine (Redis/Memcached), Node Type, Number of Nodes, Cluster Mode
- [Region] Amazon DynamoDB                  NoSQL key-value/document database, Table Name, Primary Key (Partition/Sort), Capacity Mode (On-Demand/Provisioned), Global Tables
- [Region] Amazon Redshift                  Petabyte-scale data warehouse for analytics, Cluster Type, Node Type, Number of Nodes, Database Name, Serverless/Provisioned
- [Region] Amazon DocumentDB                MongoDB-compatible document database, Cluster Configuration, Instance Class, Number of Replicas (up to 15), Storage Auto-Scaling
- [Region] Amazon Neptune                   Graph database for highly connected data, Cluster Configuration, Instance Class, Graph Model (Property/RDF), Query Language (Gremlin/SPARQL)
- [Region] Amazon EMR                       (Elastic MapReduce) Big data processing platform, Cluster Configuration, Framework (Spark/Hadoop/Presto/Hive), Instance Types, Auto-Scaling
- [Region] Amazon Athena                    Serverless SQL queries on S3 data, Workgroup, Data Catalog, Query Result Location (S3)
- [Region] AWS Glue                         Serverless ETL and data catalog service, Crawlers, Data Catalog, ETL Jobs, Job Triggers, Development Endpoints, DataBrew Recipes
- [Region] AWS DMS                          (Database Migration Service) Replication Instance, Source/Target Endpoints, Migration Tasks, CDC, Multi-AZ
- [Region] AWS Backup                       AWSサービス全体のバックアップを一元管理できるフルマネージド型のバックアップサービス

## API
- [Region] API Gateway                      API Type (REST/HTTP/WebSocket), Stages, Integrations, Authorizers, Usage Plans
- [Region] AWS AppSync                      GraphQLを使用して、 Mobile, Web App 向けの API を簡単に構築, DynamoDB,Lambda,RDS,HTTP Endpoint 様々なデータソースに接続

## Remote
⏺ [Resion] Amazon AppStream 2.0             Windows Desktop App を Web ブラウザ経由でストリーミング配信するフルマネージド型のアプリケーション仮想化サービス
⏺ [Region] Amazon WorkSpaces                フルマネージド型の仮想デスクトップサービス（DaaS）。クラウド上でWindows/Linuxデスクトップ環境を提供
- [-] Amazon WorkSpaces Secure Browser      フルマネージド型のセキュアWebブラウジングサービス。クラウド上で動作する専用ブラウザ環境を提供

## Others
- [Region] Amazon Connect                   電話対応。クラウドの柔軟性とAWSのAI/ML機能を活用できる、次世代のカスタマーサポートプラットフォーム
- [Region] Amazon SES                       (Simple Email Service) Transaction mail から Marketing mail まで、あらゆるタイプのメール送信を低コストで実現できる
- [Region] Amazon IoT Core                  AWSが提供するフルマネージド型のIoTプラットフォームサービス
⏺ [Region] Amazon Polly                     AWSが提供するテキスト読み上げ（Text-to-Speech, TTS）サービス
⏺ [Region] Amazon Translate                 AWSが提供するニューラル機械翻訳サービス
⏺ [Region] Amazon Q                         AWSが提供する生成AI搭載のビジネス向けアシスタント
- [Region] Amazon Lex                       Alexaの技術を活用した、スケーラブルで高性能な会話型AIプラットフォーム。
- [Region] Amazon Kendra                    Googleのような検索体験を企業内データに対して提供する、エンタープライズサーチのマネージドサービスです
⏺ [Region] Amazon Transcribe                AWSが提供する自動音声認識（ASR: Automatic Speech Recognition）サービスです。

---

## Security
- AWS Certificate Manager (ACM)
- AWS CloudHSM
- AWS Firewall Manager
- AWS Key Management Service (AWS KMS)
- AWS Secrets Manager
- AWS Security Hub
- Amazon Detective
- Amazon GuardDuty
- Amazon Inspector
## Monitoring
- Amazon CloudWatch
- Amazon EventBridge
- AWS CloudTrail
- AWS X-Ray
- AWS CodeGuru
- AWS Health Dashboard
## AI/ML & Natural Language
- Amazon Comprehend
- Amazon Rekognition
- Amazon SageMaker AI
- Amazon Textract
## Migration Services
- AWS Application Discovery Service
- AWS Application Migration Service
- AWS Migration Hub
- AWS Schema Conversion Tool (AWS SCT)
- Migration Evaluator
