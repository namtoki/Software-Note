# AWS

## Terminology
- AWS Management Console
- ARN (Amazon Resource Name):
  - format: `arn:partition:service:region:account-id:resource-type/resource-id`
    - `arn:aws:s3:::my-bucket/file.txt`
    - `arn:aws:ec2:us-east-1:123456789012:instance/i-1234567890abcdef0`
    - `arn:aws:iam::123456789012:user/john`
      - partition: 通常は aws（中国リージョンは aws-cn、GovCloudは aws-us-gov）
- `AWS Well-Architectedフレームワーク` ==お世辞パコ痔==
  - 目的: クラウドアーキテクチャを評価・改善するための一貫した基準を提供
  - `レビュープロセス`: 現状評価 → リスク特定 → 改善計画 → 継続的改善（3-6ヶ月ごと）
  1. ==オペレーショナルエクセレンス==（運用上の優秀性）
    - システムの運用プロセスとプロシージャを改善することを目指す
    - 運用の自動化、継続的なインフラストラクチャとアプリケーションの改善、およびチームの運用手順を文書化して共有する
    - **設計原則**: コードとしての運用 (IaC), 頻繁で小規模な変更, 運用手順の改善, 障害の予測と学習
    - **主要サービス**: CloudFormation, CloudWatch, X-Ray, Systems Manager
  2. ==セキュリティ==
    - システムを保護するための最善のプラクティスと戦略を提供
    - データの暗号化、アクセス制御、監視、およびセキュリティインシデントの対応が含まれる
    - **設計原則**: 強力なアイデンティティ基盤 (IAM), トレーサビリティ (CloudTrail), 全レイヤーセキュリティ, 自動化, データ保護
    - **主要サービス**: IAM, GuardDuty, Security Hub, KMS, WAF, Shield
  3. ==信頼性==
    - システムが障害に耐えられるようにするための指針を提供
    - 耐障害設計、データのバックアップ、およびリカバリー手順の実装が含まれる
    - **設計原則**: 障害からの自動復旧, 復旧手順のテスト, 水平スケーリング, キャパシティ推測の停止, 自動化による変更管理
    - **主要概念**: RTO (Recovery Time Objective), RPO (Recovery Point Objective)
    - **主要サービス**: Auto Scaling, Multi-AZ, Route 53, Backup, CloudWatch Alarms
  4. ==パフォーマンス効率==
    - システムが効率的に動作するようにするためのベストプラクティスを提供
    - 適切なリソースタイプの選択、スケーラビリティの設計、および最新のテクノロジーの活用が含まれる
    - **設計原則**: 先進技術の民主化, グローバル展開, サーバーレス活用, 頻繁な実験, メカニカルシンパシー
    - **最適化領域**: コンピューティング (EC2/Lambda/Fargate), ストレージ (S3/EBS/EFS), DB (RDS/DynamoDB/Redshift), ネットワーク (CloudFront)
  5. ==コスト最適化==
    - コストを抑えながらシステムのパフォーマンスを最適化するための指針を提供
    - リソースの効率的な利用、コストの監視と分析、およびコスト削減のための戦略の実装が含まれる
    - **設計原則**: クラウド財務管理, 消費モデルの採用, 全体効率の測定, 重労働の排除, 支出の分析
    - **主要サービス**: Cost Explorer, Budgets, Trusted Advisor, Compute Optimizer, Savings Plans/Reserved Instances
  6. ==持続可能性==
    - システムの設計と運用において環境への影響を最小限に抑えることを重視するもの
    - 持続可能なクラウドアーキテクチャを設計し、運用することで、環境への負担を軽減し、企業の持続可能な経営を実現
    - **設計原則**: 影響の理解, 持続可能性目標設定, 使用率最大化, 効率的HW/SW採用, マネージドサービス活用
    - **主要施策**: リージョン選択 (再生可能エネルギー), リソース適正サイジング, 不要データ削減, S3 Intelligent-Tiering
- `責任共有モデル` (Shared Responsibility Model)
  - **基本原則**: AWS とユーザー間でセキュリティとコンプライアンスの責任を分担
  - **AWS の責任**: "Security OF the Cloud" (クラウド自体のセキュリティ)
    - 物理的なインフラストラクチャ (ハードウェア、ソフトウェア、ネットワーク、施設)
    - グローバルインフラ (リージョン、AZ、エッジロケーション)
  - **ユーザーの責任**: "Security IN the Cloud" (クラウド内のセキュリティ)
    - データの管理と暗号化
    - OS、ネットワーク、ファイアウォール設定
    - アプリケーションのセキュリティ
    - IAM によるアクセス管理
  - **サービスタイプ別の責任範囲**:
    - `IaaS (EC2)`: ユーザーが OS パッチ適用、SG 設定、データ暗号化を管理
    - `PaaS (RDS, Elastic Beanstalk)`: AWS が OS パッチ適用、ユーザーがデータ管理・暗号化設定
    - `SaaS (S3, DynamoDB)`: AWS がサービス全体を管理、ユーザーがデータ・アクセス制御・暗号化設定
  - **重要ポイント**:
    - マネージドサービスでも、暗号化・アクセス制御・データ管理はユーザーの責任
    - IAM は常にユーザーの責任 (MFA、最小権限の原則)
    - データは常にユーザーの責任 (分類、暗号化、バックアップ)
- `AWS CAF`
  - 組織がAWSクラウドへの移行を効果的に行うためのガイダンスとベストプラクティスを提供するフレームワーク
  - 6つの専門領域、すなわち ==ビジネス==, ==人材==, ==ガバナンス==, ==プラットフォーム==, ==セキュリティ==, ==オペレーション== に分かれている

## Cost
- `AWS Budgets`                             特定のリソースにかかるコストや使用状況に対する予算を設定 / ==!3 予算目から課金==
- `AWS Cost Explorer`                       コスト分析と可視化
- `AWS Cost and Usage Reports`              CSV/Parquet 形式で S3 に出力 / 時間単位 / リソース ID 粒度 / ==!S3 使用料==
## Account
- `AWS Organizations`                       ==!Global==
- `AWS Control Tower`                       マルチアカウント環境を簡単にセットアップ / ==ベストプラクティス== / ダッシュボード / ガードレール
- `AWS IAM Identity Center`                 ==!Global== / シングルサインオン (SSO), マルチアカウント管理
- `AWS IAM`                                 ==!Global== / User Groups, User, Roles
## Governance
- `AWS Config`                              「どのリソースが、いつ、どう変更されたか」セキュリティとコンプライアンスのための構成監査
⏺ `Amazon CloudTrail`                       AWSアカウント内のAPI呼び出しとアクティビティを記録・監視するサービス
⏺ `AWS Health Dashboard`                    ==Service Health Dashboard== と ==Your Account Health== を可視化し、影響を通知
- `AWS Service Quotas`                      AWSサービスのクォータ（制限値）を一元管理・表示・引き上げリクエストできるサービス
## Security
- `AWS Security Hub`                        セキュリティーアラート / ==ダッシュボード== / ==CSPM==
  - `AWS Secrets Manager`                   機密情報を安全に管理し、自動ローテーション機能により運用負荷を削減
    - `AWS Key Management Service (AWS KMS)`データの暗号化・復号化に使用する暗号化キーのライフサイクル全体を管理
    - `AWS CloudHSM`                        専有の FIPS 140-2 Level 3 の ==Hardware Security Module== / 暗号鍵の生成、保管、管理
  - `AWS Firewall Manager`                  AWS Organizations 全体でファイアウォールルールとセキュリティポリシーを一元管理
    - `AWS Shield`                          ==!Global== / ==DDoS==
    - `AWS WAF (Web Application Firewall)`  ==!Global== / ==SQLインジェクション、クロスサイトスクリプティング（XSS）==
  - `Amazon GuardDuty`                      ==悪意==のある異常な動作を継続的に監視・==検出== / ==マルウェア==
  - `Amazon Inspector`                      サービスの==脆弱性==に関する Best Pradctice の順守を==自動的に評価==
  - `Amazon Macie`                          ==Amazon S3== 内の機密データを自動的に検出・分類・保護
  - `Amazon Detective`                      セキュリティ上の問題が発生した際に、根本原因を特定するための探偵の役割
- `AWS Certificate Manager (ACM)`           SSL/TLS証明書を管理 / ==HTTPS通信== に必要な証明書を、無料で発行・更新・管理
## Compliance
- `AWS Artifact`                            コンプライアンス関連ドキュメントへのセルフサービスアクセスを提供するサービス
- `AWS Audit Manager`                       ==監査==準備とコンプライアンス評価を自動化・簡素化するサービス
- `AWS License Manager`                     ソフトウェアライセンスの使用量管理と制限, 「ライセンスを何個使っているか、超過していないか」を管理
## Analytics
- `AWS Support`                             ==!Global== サービスの利用方法、トラブルシューティング、アーキテクチャガイダンスなど
  - `デベロッパー`                          ==テスト環境== / 個人開発者やスタートアップ向けのプラン。低料金で、基本的なサポート
  - `ビジネス`                              ==本番環境== / 中規模のビジネス向けのプラン / 高度なサポートとAWS Trusted Advisorの==全機能==が利用できる
  - `エンタープライズ On-Ramp`              中規模のビジネス向けのプラン。エンタープライズより制約があるが、コスト効率が高いプラン
  - `エンタープライズ`                      大規模な企業向けのプラン。最も高度なサポートと専任のテクニカルアカウントマネージャーが提供される
- `AWS Compute Optimizer`                   ==コンピュータリソースの最適化提案== / EC2, Auto Scaling Groups / 14日以上設定課金
- `AWS Trusted Advisor`                     ==!Global== / ==Best Practice== 基づき分析改善提案 / 不使用インスタンス /  ==SG チェック==
- `AWS Well-Architected Tool`               AWSワークロードをWell-Architectedフレームワークに基づいて==アーキテクチャの評価を提供==
- `Amazon QuickSight`                       ==BI==
⏺ `Amazon CloudWatch`                       リソースの監視・管理 / メトリクス収集、ログ管理、アラーム設定、ダッシュボード作成
⏺ `Amazon X-Ray`                            分散アプリケーションのパフォーマンス分析とデバッグを支援するサービス
⏺ `Amazon OpenSearch Service`               フルマネージド型の検索・分析サービス。OpenSearch, Elasticsearchをベースにした検索・分析エンジン
## Migration Services
- `Migration Evaluator`                     オンプレミス環境のデータを収集・分析 / AWS 移行時のコスト見積もりとビジネスケースを作成
- `AWS Migration Hub`                       複数の AWS およびパートナーツールを使用した移行を一元的に追跡・管理
  - `AWS Application Migration Service`     物理サーバー、仮想マシン、クラウドインスタンスを AWS に移行する
  - `AWS Application Discovery Service`     ==!us-west-2== / オンプレミス環境のアプリケーション間の依存関係を自動検出
- `AWS Schema Conversion Tool (AWS SCT)`    データベースのスキーマとコードを異なるデータベースエンジン間で変換する
- `AWS Snow Family`
  - `AWS Snowcone`                          ==!Hardware== / 8-14 TB Storage, 2 vCPUs, 4 GB Memory, ==Smallest== device, edge computing, 9 lbs
  - `AWS Snowball Edge Storage`             ==!Hardware== / 80 TB Storage, 40 vCPUs, 80 GB Memory, ==Large== data migrations
  - `AWS Snowball Edge Compute`             ==!Hardware== / 28 TB NVMe, 104 vCPUs, 416 GB Memory, ==GPU, ML, video processing==
  - `AWS Snowmobile`                        ==!Hardware== / 100 PB per truck, ==Exabyte-scale== migrations, 45-ft container
## Edge Computing
- `AWS Outposts`                            オンプレで AWS を利用できる / AWS が物理的なハードウェアを顧客のデータセンターや施設に設置
- `AWS Local Zones`                         リージョンの拡張 / 主要都市や人口密集地域に配置された小規模なデータセンター
- `AWS Wavelength`                          通信事業者の5Gネットワーク内に配置 / 5Gデバイスからインターネットを経由せずに直接AWSサービスにアクセス
## Availavility
- `Elastic Disaster Recovery (AWS DRS)`     災害復旧サービス / 物理、仮想、クラウドサーバーをAWSに継続的に複製し、迅速な復旧を可能に
## Tools
⏺ `Amazon AppStream 2.0`                    Windows Desktop App を Web ブラウザ経由でストリーミング配信
⏺ `Amazon WorkSpaces`                       フルマネージド型の仮想デスクトップ / ==DaaS== / ==Windows/Linux== デスクトップ環境を提供
- `Amazon WorkSpaces Secure Browser`        クラウド上で動作する専用ブラウザ環境を提供
⏺ `AWS Marketplace`                         ==!Global== AWS上で動作するソフトウェア、データ、サービスを検索・購入・デプロイできる==デジタルカタログ==
- `AWS Service Catalog`                     組織で承認されたAWSリソース（CloudFormationテンプレート）をカタログとして提供
- `AWS Resource Access Manager`             (RAM) マルチアカウント環境でリソースを効率的に共有し、重複を避ける
## CLI & IaC
- `AWS CLI`                                 アクセスキー
- `AWS Cloud Development Kit (CDK)`
- `AWS CloudFormation`
- `AWS Systems Manager (SSM)`               AWSとオンプレミスのインフラストラクチャを一元的に管理・運用するための統合サービス
- `AWS CodeBuild`                           コンパイル、テスト実行し、デプロイ可能なソフトウェアパッケージを生成する ==CI== サービス
- `AWS CodePipeline`                        ソフトウェアのリリースプロセスを自動化するフルマネージドな ==CD== サービス
⏺ `AWS Step Functions`                      複数のサービスを視覚的な Workflow / 分散 App や MicroService を構築, オーケストレーション
## All-in
- `Amazon Lightsail`                        ==VPS== / サーバー・ストレージ・データ転送・IPがパッケージ / 数クリックでデプロイ完了 / (WordPress、LAMP等)
- `AWS Elastic Beanstalk`                   ==PaaS== / ==バックエンド・Webアプリ特化== / 裏側でEC2・ELB・Auto Scaling等を自動構築
- `AWS Amplify`                             ==BaaS== / ==フロントエンド・モバイル特化== / ビルド、デプロイ、ホスティングを簡素化
## Networking
- `Amazon VPC`
  - `AWS PrivateLink`                       AWSサービス⇔ VPC間のプライベート接続
  - `Amazon VPN`
    - `AWS Site-to-Site VPN`                オンプレミス⇔ AWS VPC
  - `AWS Direct Connect`                    オンプレミス⇔ AWS専用線 (==専用物理回線==)
  - `AWS Client VPN`                        リモートユーザー(個人デバイス) ⇔ AWS VPC
  - `AWS Transit Gateway`                   複数のVPC、VPN、Direct Connectを相互接続するハブ。ネットワークトポロジーを簡素化
- `Amazon Route 53`                         ==!Global== / ルーティングポリシー (加重, IP ベース, レイテンシー, フェイルオーバー)
- `Amazon CloudFront`                       ==!Global== / 静的コンテンツ / HTTP/S / CDN
- `AWS Global Accelerator`                  ==!Global== / 動的コンテンツ / TCP/UDP / ==静的IPアドレス== / パフォーマンス向上 / (ALB,NLB,EC2,Elastic IP)
- `Amazon API Gateway`                      API 管理サービス / 開発者が RESTful API、HTTP API、WebSocket API を簡単に作成、公開、保守、監視、保護
- `AWS AppSync`                             ==GraphQL==  / Mobile, Web 向けの API を簡単に構築, DynamoDB,Lambda,RDS,HTTP Endpoint 様々なデータソースに接続
## Inter-Communication
- `Amazon SQS`                              (Amazon Simple Queue Service)
- `Amazon SNS`                              (Amazon Simple Notification Service)
- `Amazon MQ`                               Apache ActiveMQ とRabbitMQ のマネージド型メッセージブローカーサービス
- `Amazon Kinesis`                          リアルタイムのストリーミングデータを収集、処理、分析するための完全マネージド型サービス
⏺ `Amazon EventBridge`                      サービス間でイベントを簡単に接続し、イベント駆動型アーキテクチャを構築
## Computing
- `EC2`                                     AMI, Instance Type, Key Pair, Instance Store, User Data
  - `Option`  
    - `オンデマンドインスタンス`            時間単位
    - `リザーブドインスタンス`              (1 or 3 年) / 全額前払い, 一部前払い, 前払いなし
    - `スポットインスタンス`                余剰キャパシティを大幅な割引で使用 / 1 年間安定して稼働させるのには適していない
    - `Dedicated Hosts`                     物理的な EC2 サーバを専有 / 特定のライセンス要件の場合使用
  - `Instance Store`                        Temporary
  - `Auto Scaling`                          Auto Scaling Group (ASG), Scaling Policy
  - `Image Builder`
  - `Amazon Elastic Load Balancing`         レイヤ7
  - `Auto Scaling`
- `AWS Fargate`                             サーバーレスなコンテナ実行環境を提供するAWSのコンピューティングエンジン
- `ECS (Elastic Container Service)`
  - `ECR (Elastic Container Registry)`
  - `EKS (Elastic Kubernetes Service)`
- `Amazon EBS (Elastic Block Store)`        ==唯一 1 つのインスタンスに接続==
- `AWS Lambda`
- `AWS Batch`                               数十万規模のジョブを自動的にスケールし、最適なリソース (EC2/Fargate/Spot) を動的にプロビジョニング
## Storage
- `Amazon FSx`                              サードパーティ製ファイルシステム / Windows File Server, Lustre, NetApp, ONTAP, OpenZFS など
- `Amazon EFS (Elastic File System)`        複数のEC2インスタンスから同時にアクセス可能な、NFSv4 ファイルストレージサービス
- `Amazon S3`                               Bucket Name, Versioning, Encryption, Storage Class
  - `Amazon S3 Glacier`                     Long-term archival storage, Vault Name, Archive, Retrieval Options
  - `Amazon Athena`                         ==S3== に保存されたデータに対して ==SQLクエリ== を実行できる、サーバーレスなインタラクティブ分析サービス
- `Amazon RDS`                              ==Relational DB== / Engine (Aurora/MySQL/PostgreSQL/MariaDB/Oracle/SQL Server)
  - `Amazon Aurora`                         ==Relational DB== / 5x MySQL/3x PostgreSQL performance
- `Amazon ElastiCache`                      ==In-memory caching== service for performance / Engine (==Redis/Memcached==)
- `Amazon DynamoDB`                         ==NoSQL== key-value/document database
- `Amazon Redshift`                         ==Petabyte-scale data warehouse== for analytics
- `Amazon DocumentDB`                       ==MongoDB== のワークロードをAWSクラウドで簡単に実行、管理、スケール
- `Amazon Neptune`                          ==Graph database== for highly connected data
- `Amazon EMR (Elastic MapReduce)`          Big data processing platform, ==MapReduce (Spark/Hadoop/Presto/Hive)==
- `AWS Glue`                                ==ETL== / Source (S3, RDS, Redshift, DynamoDB, オンプレミス)
- `AWS DMS`                                 異なるデータベースエンジン間での移行、オンプレミスからクラウドへの移行、継続的なデータレプリケーション
- `AWS Backup`                              AWSサービス全体のバックアップを一元管理できるフルマネージド型のバックアップサービス
- `AWS Storage Gateway`                     オンプレと AWS ストレージをシームレスに接続するハイブリッドクラウドストレージサービス / ==物理テープも==
## AI / ML
⏺ `Amazon SageMaker AI`                     包括的な機械学習プラットフォーム。機械学習モデルの構築、トレーニング、デプロイまでのライフサイクル全体を管理
⏺ `Amazon Q`                                AWSが提供する生成AI搭載のビジネス向けアシスタント
- `Amazon Kendra`                           Googleのような検索体験を企業内データに対して提供する、==エンタープライズサーチ==のマネージドサービス
- `Amazon Lex`                              Chat
⏺ `Amazon Rekognition`                      画像・動画分析
⏺ `Amazon Textract`                         画像 --> Text
⏺ `Amazon Transcribe`                       Speech --> Text
⏺ `Amazon Translate`                        Text --> Text (翻訳)
⏺ `Amazon Comprehend`                       Text --> Text (要約、抽出)
⏺ `Amazon Polly`                            Text --> Speech
⏺ `Amazon CodeGuru`                         機械学習を使用してコードレビューとアプリケーションのパフォーマンス最適化を自動化するサービス
## Others
- `AWS Directory Service`                   ==Microsoft Active Directory (AD)== の機能を AWS クラウド内で提供するマネージドサービス
- `Amazon Cognito`                          Web/Mobile Application にユーザー認証・認可機能を簡単に追加できるマネージドサービス
- `Amazon Connect`                          電話対応。クラウドの柔軟性とAWSのAI/ML機能を活用できる、次世代のカスタマーサポートプラットフォーム
- `Amazon SES (Simple Email Service)`       Transaction mail から Marketing mail まで、あらゆるタイプのメール送信を低コストで実現
- `Amazon IoT Core`                         AWSが提供するフルマネージド型のIoTプラットフォームサービス
