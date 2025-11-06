# AWS

## Terminology
- AWS Management Console
- ARN (Amazon Resource Name):
  - format: `arn:partition:service:region:account-id:resource-type/resource-id`
    - `arn:aws:s3:::my-bucket/file.txt`
    - `arn:aws:ec2:us-east-1:123456789012:instance/i-1234567890abcdef0`
    - `arn:aws:iam::123456789012:user/john`
      - partition: 通常は aws（中国リージョンは aws-cn、GovCloudは aws-us-gov）
- `AWS Well-Architectedフレームワーク`
  1. ==オペレーショナルエクセレンス==（運用上の優秀性）
    - システムの運用プロセスとプロシージャを改善することを目指す
    - 運用の自動化、継続的なインフラストラクチャとアプリケーションの改善、およびチームの運用手順を文書化して共有する
  2. ==セキュリティ==
    - システムを保護するための最善のプラクティスと戦略を提供
    - データの暗号化、アクセス制御、監視、およびセキュリティインシデントの対応が含まれる
  3. ==信頼性==
    - システムが障害に耐えられるようにするための指針を提供
    - 耐障害設計、データのバックアップ、およびリカバリー手順の実装が含まれる
  4. ==パフォーマンス効率==
    - システムが効率的に動作するようにするためのベストプラクティスを提供
    - 適切なリソースタイプの選択、スケーラビリティの設計、および最新のテクノロジーの活用が含まれる
  5. ==コスト最適化==
    - コストを抑えながらシステムのパフォーマンスを最適化するための指針を提供
    - リソースの効率的な利用、コストの監視と分析、およびコスト削減のための戦略の実装が含まれる
  6. ==持続可能性==
    - システムの設計と運用において環境への影響を最小限に抑えることを重視するもの
    - 持続可能なクラウドアーキテクチャを設計し、運用することで、環境への負担を軽減し、企業の持続可能な経営を実現
- マネージドサービスにおいても、ユーザがセキュリティ設定を行う必要がある

## Cost
- `AWS Budgets`                             特定のリソースにかかるコストや使用状況に対する予算を設定 / ==!3 予算目から課金==
- `AWS Cost Explorer`                       コスト分析と可視化
- `AWS Cost and Usage Reports`              CSV/Parquet 形式で S3 に出力 / 時間単位 / リソース ID 粒度 / ==!S3 使用料==

## Account
- `AWS Organizations`                       ==!Global==
- `AWS Control Tower`                       マルチアカウント環境を簡単にセットアップ / AWS のベストプラクティス / ダッシュボード
- `AWS IAM Identity Center`                 ==!Global== / シングルサインオン (SSO), マルチアカウント管理
- `AWS IAM`                                 ==!Global== / User Groups, User, Roles

## Governance
- `AWS Config`                              「どのリソースが、いつ、どう変更されたか」セキュリティとコンプライアンスのための構成監査
⏺ `Amazon CloudTrail`                       AWSアカウント内のAPI呼び出しとアクティビティを記録・監視するサービス
⏺ `AWS Health Dashboard`                    ==Service Health Dashboard== と ==Your Account Health== を可視化し、影響を通知

## Compliance
- `AWS Artifact`                            コンプライアンス関連ドキュメントへのセルフサービスアクセスを提供するサービス
- `AWS Audit Manager`                       ==監査==準備とコンプライアンス評価を自動化・簡素化するサービス

## Migration Services
- `Migration Evaluator`                     オンプレミス環境のデータを収集・分析 / AWS 移行時のコスト見積もりとビジネスケースを作成
- `AWS Migration Hub`                       複数の AWS およびパートナーツールを使用した移行を一元的に追跡・管理
  - `AWS Application Migration Service`     物理サーバー、仮想マシン、クラウドインスタンスを AWS に移行する
  - `AWS Application Discovery Service`     ==!us-west-2== / オンプレミス環境のアプリケーション間の依存関係を自動検出
- `AWS Schema Conversion Tool (AWS SCT)`    データベースのスキーマとコードを異なるデータベースエンジン間で変換する
- [Physical] AWS Snowcone                   8-14 TB Storage, 2 vCPUs, 4 GB Memory, Smallest device, edge computing, 9 lbs
- [Physical] AWS Snowball Edge Storage      80 TB Storage, 40 vCPUs, 80 GB Memory, Large data migrations
- [Physical] AWS Snowball Edge Compute      28 TB NVMe, 104 vCPUs, 416 GB Memory, GPU, ML, video processing
- [Physical] AWS Snowmobile                 100 PB per truck, Exabyte-scale migrations, 45-ft container

## Availavility
- `Elastic Disaster Recovery (AWS DRS)`     災害復旧サービス / 物理、仮想、クラウドサーバーをAWSに継続的に複製し、迅速な復旧を可能に

## Security
- `AWS Security Hub`                        セキュリティーアラート / ==ダッシュボード==
  - `AWS Secrets Manager`                   機密情報を安全に管理し、自動ローテーション機能により運用負荷を削減
    - `AWS Key Management Service (AWS KMS)`データの暗号化・復号化に使用する暗号化キーのライフサイクル全体を管理
    - `AWS CloudHSM`                        専有の FIPS 140-2 Level 3 の ==Hardware Security Module== / 暗号鍵の生成、保管、管理
  - `AWS Firewall Manager`                  AWS Organizations 全体でファイアウォールルールとセキュリティポリシーを一元管理
    - `AWS Shield`                          ==!Global== / ==DDoS==
    - `AWS WAF (Web Application Firewall)`  ==!Global== / ==SQLインジェクション、クロスサイトスクリプティング（XSS）==
  - `Amazon GuardDuty`                      ==悪意==のある異常な動作を継続的に監視・==検出==
  - `Amazon Inspector`                      サービスの==脆弱性==に関する Best Pradctice の順守を==自動的に評価==
  - `Amazon Macie`                          ==Amazon S3== 内の機密データを自動的に検出・分類・保護
  - `Amazon Detective`                      セキュリティ上の問題が発生した際に、根本原因を特定するための探偵の役割
- `AWS Certificate Manager (ACM)`           SSL/TLS証明書を管理 / ==HTTPS通信== に必要な証明書を、無料で発行・更新・管理

## Analytics
- `AWS Support`                             ==!Global== サービスの利用方法、トラブルシューティング、アーキテクチャガイダンスなど
- `AWS Compute Optimizer`                   ==最適化提案== / EC2, Auto Scaling Groups / 14日以上設定課金
- `AWS Trusted Advisor`                     ==!Global== / AWSの ==Best Practice== に基づきアカウントを分析改善提案 / ==SG チェック==
- `Amazon QuickSight`                       ==BI==
⏺ `Amazon CloudWatch`                       リソースの監視・管理 / メトリクス収集、ログ管理、アラーム設定、ダッシュボード作成
⏺ `Amazon X-Ray`                            分散アプリケーションのパフォーマンス分析とデバッグを支援するサービス

## Tools
- `AWS Elastic Beanstalk`                   ==PaaS==
⏺ `Amazon AppStream 2.0`                    Windows Desktop App を Web ブラウザ経由でストリーミング配信
⏺ `Amazon WorkSpaces`                       フルマネージド型の仮想デスクトップ / ==DaaS== / ==Windows/Linux== デスクトップ環境を提供
- `Amazon WorkSpaces Secure Browser`        クラウド上で動作する専用ブラウザ環境を提供
- AWS Well-Architected Tool        AWSワークロードをWell-Architectedフレームワークに基づいて評価・改善するための無料のセルフサービスツール
- AWS License Manager              ソフトウェアライセンスの使用量管理と制限, 「ライセンスを何個使っているか、超過していないか」を管理
### 統制＆コントロール
- AWS Resource Access Manager      (RAM) マルチアカウント環境でリソースを効率的に共有し、重複を避ける
- `AWS Service Catalog`   組織で承認されたAWSリソース（CloudFormationテンプレート）をカタログとして提供
- Service Quotas                   AWSサービスのクォータ（制限値）を一元管理・表示・引き上げリクエストできるサービス
### BaaS
- AWS Amplify                      フロントエンド開発者がフルスタックアプリを構築できるようにする統合プラットフォーム
### Store
⏺ AWS Marketplace                       ==Global== Store

## Regional Networking
- `Amazon VPC`
  - `AWS PrivateLink`                       AWSサービス⇔ VPC間のプライベート接続
  - `AWS Site-to-Site VPN`                  オンプレミス⇔ AWS VPC
  - `AWS Direct Connect`                    オンプレミス⇔ AWS専用線 (==専用物理回線==)
  - `AWS Client VPN`                        リモートユーザー(個人デバイス) ⇔ AWS VPC
  - `AWS Transit Gateway`                   複数のVPC、VPN、Direct Connectを相互接続するハブ。ネットワークトポロジーを簡素化

## CLI & IaC
- `AWS CLI`                                 アクセスキー
- `AWS Cloud Development Kit (CDK)`
- `AWS CloudFormation`
- `AWS Systems Manager (SSM)`               AWSとオンプレミスのインフラストラクチャを一元的に管理・運用するための統合サービス
- `AWS CodeBuild`                           コンパイル、テスト実行し、デプロイ可能なソフトウェアパッケージを生成する ==CI== サービス
- `AWS CodePipeline`                        ソフトウェアのリリースプロセスを自動化するフルマネージドな ==CD== サービス
⏺ `AWS Step Functions`                      複数のサービスを視覚的な Workflow / 分散 App や MicroService を構築, オーケストレーション

## Monitoring
⏺ Amazon OpenSearch Service        フルマネージド型の検索・分析サービス。OpenSearch, Elasticsearchをベースにした検索・分析エンジン

## Others
- `AWS Directory Service`                   ==Microsoft Active Directory (AD)== の機能を AWS クラウド内で提供するマネージドサービス
- `Amazon Cognito`                          Web/Mobile Application にユーザー認証・認可機能を簡単に追加できるマネージドサービス

## Localization
- AWS Outposts                          On-premises
- AWS Local Zones                       AWS サービスを主要都市圏の近くに配置するインフラストラクチャ
- AWS Wavelength                        AWSのコンピューティングとストレージサービスを5G通信事業者のネットワークエッジに組み込むサービス

## Global Player
- `Amazon Route 53`                         ==!Global== / ルーティングポリシー (加重, IP ベース, レイテンシー, フェイルオーバー)
- `Amazon CloudFront`                       ==!Global== / CDN
- Global Accelerator                      ==Global== TCP/UDPトラフィック向け、非HTTPアプリケーション対応

## Inter-Communication
- `Amazon SQS`                              (Amazon Simple Queue Service)
- Amazon SNS                       (Amazon Simple Notification Service)
- Amazon MQ                        Apache ActiveMQ とRabbitMQ のマネージド型メッセージブローカーサービス
- `Amazon Kinesis`                          リアルタイムのストリーミングデータを収集、処理、分析するための完全マネージド型サービス
⏺ `Amazon EventBridge`                      サービス間でイベントを簡単に接続し、イベント駆動型アーキテクチャを構築

## Computing
- `EC2`                                     AMI, Instance Type, Key Pair, Instance Store, User Data
  - `Option`  
    - `オンデマンドインスタンス`            時間単位
    - `リザーブドインスタンス`              (1 or 3 年) / 全額前払い, 一部前払い, 前払いなし
    - `スポットインスタンス`                余剰キャパシティを大幅な割引で使用 / 1 年間安定して稼働させるのには適していない
    - `Dedicated Hosts`                     物理的な EC2 サーバを専有 / 特定のライセンス要件の場合使用
  - Instance Store                        Temporary
  - Auto Scaling                          Auto Scaling Group (ASG), Scaling Policy
  - Image Builder
  - `Amazon Elastic Load Balancing`         レイヤ7
  - `Auto Scaling`
- `AWS Fargate`                             サーバーレスなコンテナ実行環境を提供するAWSのコンピューティングエンジン
- ECS                              (Elastic Container Service)
  - ECR                                   (Elastic Container Registry)
  - EKS                                   (Elastic Kubernetes Service - Managed Kubernetes) Cluster, Node Groups, Fargate Profiles
- `Amazon EBS`                              (Elastic Block Store)
- `AWS Lambda`  Runtime, Memory, Timeout, Handler, Layers, Triggers
- Batch                            Managed batch processing - Runs jobs on EC2/Fargate/Spot
- `Amazon Lightsail`                        Simplified VPS - Bundled compute, storage, networking with predictable pricing

## Storage
- Amazon FSx                           Capacity
- `Amazon EFS (Elastic File System)`        複数のEC2インスタンスから同時にアクセス可能な、NFSv4 ファイルストレージサービス
- `Amazon S3`                               Bucket Name, Versioning, Encryption, Storage Class
- `Amazon S3 Glacier`                       Long-term archival storage, Vault Name, Archive, Retrieval Options
- `Amazon RDS`                              ==Relational DB== / Engine (Aurora/MySQL/PostgreSQL/MariaDB/Oracle/SQL Server)
  - `Amazon Aurora`                         ==Relational DB== / 5x MySQL/3x PostgreSQL performance
- `Amazon ElastiCache`                      ==In-memory caching== service for performance / Engine (==Redis/Memcached==)
- `Amazon DynamoDB`                         ==NoSQL== key-value/document database
- Amazon Redshift                  Petabyte-scale data warehouse for analytics, Cluster Type, Node Type, Number of Nodes, Database Name, Serverless/Provisioned
- Amazon DocumentDB                MongoDB-compatible document database, Cluster Configuration, Instance Class, Number of Replicas (up to 15), Storage Auto-Scaling
- `Amazon Neptune`                          ==Graph database== for highly connected data
- `Amazon EMR (Elastic MapReduce)`          Big data processing platform, ==MapReduce (Spark/Hadoop/Presto/Hive)==
- Amazon Athena                    Serverless SQL queries on S3 data, Workgroup, Data Catalog, Query Result Location (S3)
- `AWS Glue`                                ==ETL== / Source (S3, RDS, Redshift, DynamoDB, オンプレミス)
- AWS DMS                          (Database Migration Service) Replication Instance, Source/Target Endpoints, Migration Tasks, CDC, Multi-AZ
- `AWS Backup`                              AWSサービス全体のバックアップを一元管理できるフルマネージド型のバックアップサービス
- `AWS Storage Gateway`                     オンプレと AWS ストレージをシームレスに接続するハイブリッドクラウドストレージサービス

## API
- API Gateway                      API Type (REST/HTTP/WebSocket), Stages, Integrations, Authorizers, Usage Plans
- AWS AppSync                      GraphQLを使用して、 Mobile, Web App 向けの API を簡単に構築, DynamoDB,Lambda,RDS,HTTP Endpoint 様々なデータソースに接続

## AI / ML
⏺ `Amazon SageMaker AI`  包括的な機械学習プラットフォーム。機械学習モデルの構築、トレーニング、デプロイまでのライフサイクル全体を管理
⏺ Amazon Q              AWSが提供する生成AI搭載のビジネス向けアシスタント
- `Amazon Kendra`        Googleのような検索体験を企業内データに対して提供する、==エンタープライズサーチ==のマネージドサービス
- `Amazon Lex`           Chat
⏺ `Amazon Rekognition`   画像・動画分析
⏺ `Amazon Textract`      画像 --> Text
⏺ `Amazon Transcribe`    Speech --> Text
⏺ `Amazon Translate`     Text --> Text (翻訳)
⏺ `Amazon Comprehend`    Text --> Text (要約、抽出)
⏺ `Amazon Polly`         Text --> Speech
⏺ Amazon CodeGuru       機械学習を使用してコードレビューとアプリケーションのパフォーマンス最適化を自動化するサービス

## Business
- Amazon Connect                   電話対応。クラウドの柔軟性とAWSのAI/ML機能を活用できる、次世代のカスタマーサポートプラットフォーム
- Amazon SES                       (Simple Email Service) Transaction mail から Marketing mail まで、あらゆるタイプのメール送信を低コストで実現

## IoT
- Amazon IoT Core                  AWSが提供するフルマネージド型のIoTプラットフォームサービス
