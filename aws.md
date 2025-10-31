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
- AWS Control Tower                     複数のリージョンにまたがってガバナンスを適用
- AWS Organizations                     ==Global==
- AWS IAM Identity Center               ==Global== シングルサインオン (SSO), マルチアカウント管理
- IAM                                   ==Global== User Groups, User, Roles
- Amazon WorkSpaces Secure Browser      フルマネージド型のセキュアWebブラウジングサービス。クラウド上で動作する専用ブラウザ環境を提供

## Cost & Budgets
- AWS Cost and Usage Reports
- AWS Cost Explorer

## Compliance
- AWS Artifact                     AWS のコンプライアンス関連ドキュメントへのセルフサービスアクセスを提供するサービス
- AWS Audit Manager                監査準備とコンプライアンス評価を自動化・簡素化するサービス

## CLI & IaC
- AWS CLI
- AWS Cloud Development Kit (CDK)
- AWS CloudFormation
- AWS Systems Manager (SSM)        AWSとオンプレミスのインフラストラクチャを一元的に管理・運用するための統合サービス
- AWS CodeBuild                    ソースコードをコンパイル、テスト実行し、デプロイ可能なソフトウェアパッケージを生成する CI サービス
- AWS CodePipeline                 ソフトウェアのリリースプロセスを自動化するフルマネージドな継続的デリバリー（CD）サービス
⏺ AWS Step Functions               複数の AWS サービスを組み合わせて、ワークフローを構築・管理するためのサーバーレスオーケストレーションサービス

## Resource Management
- AWS Support                           ==Global== インフラ、サービスの利用方法、トラブルシューティング、アーキテクチャガイダンスなど、サポートを提供
### 最適化提案
- AWS Compute Optimizer            EC2, Auto Scaling Groups, EBS volumes, Lambda, Aurora, RDS, ECS on Fargate, 14日以上設定課金
### 監査
- AWS Trusted Advisor                   ==Global== AWSのベストプラクティスに基づいてアカウントを分析し、改善提案を行う自動アドバイザリーサービス
- AWS Well-Architected Tool        AWSワークロードをWell-Architectedフレームワークに基づいて評価・改善するための無料のセルフサービスツール
- AWS Config                       「どのリソースが、いつ、どう変更されたか」を追跡, セキュリティとコンプライアンスのための構成監査
- AWS License Manager              ソフトウェアライセンスの使用量管理と制限, 「ライセンスを何個使っているか、超過していないか」を管理
### 統制＆コントロール
- AWS Resource Access Manager      (RAM) マルチアカウント環境でリソースを効率的に共有し、重複を避ける
- AWS Service Catalog              組織で承認されたAWSリソース（CloudFormationテンプレート）をカタログとして提供
- Service Quotas                   AWSサービスのクォータ（制限値）を一元管理・表示・引き上げリクエストできるサービス
### BaaS
- AWS Amplify                      フロントエンド開発者がフルスタックアプリを構築できるようにする統合プラットフォーム
### PaaS
- AWS Elastic Beanstalk
### Store
⏺ AWS Marketplace                       ==Global== Store
### BI
- QuickSight                       Business intelligence and data visualization service |
### Backup
⏺ AWS Elastic Disaster Recovery    (AWS DRS) 物理、仮想、Cloud Base Server を AWS に継続的にレプリケートし、迅速な災害復旧を実現するマネージドサービス

## Monitoring
⏺ Amazon CloudWatch                AWSリソースとアプリケーションの監視・管理。メトリクス収集、ログ管理、アラーム設定、ダッシュボード作成
⏺ Amazon OpenSearch Service        フルマネージド型の検索・分析サービス。OpenSearch, Elasticsearchをベースにした検索・分析エンジン
⏺ Amazon EventBridge               アプリケーション間でイベントを簡単に接続し、イベント駆動型アーキテクチャを構築
⏺ Amazon CloudTrail                AWSアカウント内のAPI呼び出しとアクティビティを記録・監視するサービス
⏺ Amazon X-Ray                     分散アプリケーションのパフォーマンス分析とデバッグを支援するサービス
⏺ AWS Health Dashboard             AWSのサービス状態とアカウント固有のイベントを監視するサービス

## Identity & Access
- AWS Directory Service            Microsoft Active Directory（AD）の機能を AWS クラウド内で提供するマネージドサービス
- Amazon Cognito                   Web/Mobile Application にユーザー認証・認可機能を簡単に追加できるマネージドサービス

## Localization
- AWS Outposts                          On-premises
- AWS Local Zones                       AWS サービスを主要都市圏の近くに配置するインフラストラクチャ
- AWS Wavelength                        AWSのコンピューティングとストレージサービスを5G通信事業者のネットワークエッジに組み込むサービス

## Global Player
- Amazon Route 53                       ==Global==
- Amazon CloudFront                     ==Global==
- Global Accelerator                    ==Global== TCP/UDPトラフィック向け、非HTTPアプリケーション対応
- AWS Shield                            ==Global== DDoS
- AWS WAF (Web Application Firewall)    ==Global== SQLインジェクション、クロスサイトスクリプティング（XSS）、DDoS攻撃など

## Regional Networking
- Amazon VPC
- AWS PrivateLink                  AWSサービス/VPC間のプライベート接続
- AWS Site-to-Site VPN             オンプレミス⇔ AWS VPC
- AWS Direct Connect               オンプレミス⇔ AWS専用線 (専用物理回線)
- AWS Client VPN                   リモートユーザー(個人デバイス) ⇔ AWS VPC
- AWS Transit Gateway              複数のVPC、VPN、Direct Connectを相互接続するハブ。ネットワークトポロジーを簡素化

## Inter-Communication
- Amazon SQS                       (Amazon Simple Queue Service)
- Amazon SNS                       (Amazon Simple Notification Service)
- Amazon MQ                        Apache ActiveMQ とRabbitMQ のマネージド型メッセージブローカーサービス
- Amazon Kinesis                   リアルタイムのストリーミングデータを収集、処理、分析するための完全マネージド型サービス

## Computing
- EC2                              AMI, Instance Type, Key Pair, Instance Store, User Data
  - Instance Store                        Temporary
  - Auto Scaling                          Auto Scaling Group (ASG), Scaling Policy
  - Image Builder
  - Load Balancer
  - Auto Scaling
- AWS Fargate                      サーバーレスなコンテナ実行環境を提供するAWSのコンピューティングエンジン
- ECS                              (Elastic Container Service)
  - ECR                                   (Elastic Container Registry)
  - EKS                                   (Elastic Kubernetes Service - Managed Kubernetes) Cluster, Node Groups, Fargate Profiles
- EBS                              (Elastic Block Store) Volume Type, Size, IOPS, Snapshot ID, Encryption
- Lambda                           Runtime, Memory, Timeout, Handler, Layers, Triggers
- Batch                            Managed batch processing - Runs jobs on EC2/Fargate/Spot
- Lightsail                        Simplified VPS - Bundled compute, storage, networking with predictable pricing

## Storage
- Amazon FSx                           Capacity
- Amazon EFS                           (Elastic File System) Auto-Scaling
- Amazon S3                        (Simple Storage Service) Bucket Name, Versioning, Encryption, Storage Class
- Amazon S3 Glacier                Long-term archival storage, Vault Name, Archive, Retrieval Options
- Amazon Macie                     Amazon S3内の機密データを自動的に検出・分類・保護
- [Physical] AWS Snowcone                   8-14 TB Storage, 2 vCPUs, 4 GB Memory, Smallest device, edge computing, 9 lbs
- [Physical] AWS Snowball Edge Storage      80 TB Storage, 40 vCPUs, 80 GB Memory, Large data migrations
- [Physical] AWS Snowball Edge Compute      28 TB NVMe, 104 vCPUs, 416 GB Memory, GPU, ML, video processing
- [Physical] AWS Snowmobile                 100 PB per truck, Exabyte-scale migrations, 45-ft container
- [Hybrid] AWS Storage Gateway              Bridge on-premises to AWS storage (S3/FSx/EBS/Glacier), Gateway Type (File/FSx/Volume/Tape)
- Amazon RDS                       (Relational Database Service) Engine (Aurora/MySQL/PostgreSQL/MariaDB/Oracle/SQL Server), Instance Class, Storage Type
- Amazon Aurora                    Cloud-native relational DB, 5x MySQL/3x PostgreSQL performance, Engine (MySQL/PostgreSQL), Deployment (Provisioned/Serverless v2/Global)
- Amazon ElastiCache               In-memory caching service for performance, Engine (Redis/Memcached), Node Type, Number of Nodes, Cluster Mode
- Amazon DynamoDB                  NoSQL key-value/document database, Table Name, Primary Key (Partition/Sort), Capacity Mode (On-Demand/Provisioned), Global Tables
- Amazon Redshift                  Petabyte-scale data warehouse for analytics, Cluster Type, Node Type, Number of Nodes, Database Name, Serverless/Provisioned
- Amazon DocumentDB                MongoDB-compatible document database, Cluster Configuration, Instance Class, Number of Replicas (up to 15), Storage Auto-Scaling
- Amazon Neptune                   Graph database for highly connected data, Cluster Configuration, Instance Class, Graph Model (Property/RDF), Query Language (Gremlin/SPARQL)
- Amazon EMR                       (Elastic MapReduce) Big data processing platform, Cluster Configuration, Framework (Spark/Hadoop/Presto/Hive), Instance Types, Auto-Scaling
- Amazon Athena                    Serverless SQL queries on S3 data, Workgroup, Data Catalog, Query Result Location (S3)
- AWS Glue                         Serverless ETL and data catalog service, Crawlers, Data Catalog, ETL Jobs, Job Triggers, Development Endpoints, DataBrew Recipes
- AWS DMS                          (Database Migration Service) Replication Instance, Source/Target Endpoints, Migration Tasks, CDC, Multi-AZ
- AWS Backup                       AWSサービス全体のバックアップを一元管理できるフルマネージド型のバックアップサービス

## API
- API Gateway                      API Type (REST/HTTP/WebSocket), Stages, Integrations, Authorizers, Usage Plans
- AWS AppSync                      GraphQLを使用して、 Mobile, Web App 向けの API を簡単に構築, DynamoDB,Lambda,RDS,HTTP Endpoint 様々なデータソースに接続

## Remote
⏺ Amazon AppStream 2.0             Windows Desktop App を Web ブラウザ経由でストリーミング配信するフルマネージド型のアプリケーション仮想化サービス
⏺ Amazon WorkSpaces                フルマネージド型の仮想デスクトップサービス（DaaS）。クラウド上でWindows/Linuxデスクトップ環境を提供
- Amazon WorkSpaces Secure Browser      フルマネージド型のセキュアWebブラウジングサービス。クラウド上で動作する専用ブラウザ環境を提供

## Business
- Amazon Connect                   電話対応。クラウドの柔軟性とAWSのAI/ML機能を活用できる、次世代のカスタマーサポートプラットフォーム
- Amazon SES                       (Simple Email Service) Transaction mail から Marketing mail まで、あらゆるタイプのメール送信を低コストで実現

## IoT
- Amazon IoT Core                  AWSが提供するフルマネージド型のIoTプラットフォームサービス

## AI / ML
⏺ Amazon SageMaker AI              包括的な機械学習プラットフォーム。機械学習モデルの構築、トレーニング、デプロイまでのライフサイクル全体を管理
⏺ Amazon Q                         AWSが提供する生成AI搭載のビジネス向けアシスタント
- Amazon Kendra                    Googleのような検索体験を企業内データに対して提供する、エンタープライズサーチのマネージドサービスです
- Amazon Lex                       Chat
⏺ Amazon Rekognition               画像・動画分析
⏺ Amazon Textract                  画像 --> Text
⏺ Amazon Transcribe                Speech --> Text
⏺ Amazon Translate                 Text --> Text (翻訳)
⏺ Amazon Comprehend                Text --> Text (要約、抽出)
⏺ Amazon Polly                     Text --> Speech
⏺ Amazon CodeGuru                  機械学習を使用してコードレビューとアプリケーションのパフォーマンス最適化を自動化するサービス

## Migration Services
- [us-west-2] Application Discovery Service オンプレミス環境のサーバー、アプリケーション、依存関係を自動検出し、AWS移行計画を支援するサービス
- AWS Application Migration Service
- AWS Migration Hub
- AWS Schema Conversion Tool (AWS SCT)
- Migration Evaluator

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
