# AWS

---

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
- `AWS CAF`
  - 組織がAWSクラウドへの移行を効果的に行うためのガイダンスとベストプラクティスを提供するフレームワーク
  - 6つの専門領域、すなわち ==ビジネス==, ==人材==, ==ガバナンス==, ==プラットフォーム==, ==セキュリティ==, ==オペレーション== に分かれている

---

## Cost

- `AWS Budgets`                             ==1 時間単位== / ==予防== / 特定のリソースにかかるコストや使用状況に対する予算を設定 / ==!3 予算目から課金==
- ==!AWS Cost Explorer==                       ==1 時間単位== / ==分析== / コスト分析と可視化
- `AWS Cost and Usage Reports`              ==1 時間単位== / ==詳細分析== / コストと使用状況の ==CSV/JSON== 形式で S3 に出力 / リソース ID 粒度 / ==!S3 使用料==
- `AWS Billing and Cost Management`         ==月単位== / ==請求管理== / 請求情報の表示、ダウンロード、支払い

---

## Account & Governance & Security

- `AWS Control Tower`                       1 時間以内に==Landing Zone==構築 / ベストプラクティス / ダッシュボード / SCP によるガードレール
  - `AWS Organizations`                     ==!Global== / 複数 AWS アカウントに Service Control Policy (==SCP==) を ==OU==（Organizational Unit）単位で適用
  - `AWS IAM Identity Center`               ==!Global== / 1回のログインで全アカウントにアクセス可能 / 一元的なアクセス管理 / 外部IDプロバイダー連携 (SSO)
  - `AWS IAM`                               ==!Global== / User Groups, User, Roles
  - `AWS Config`                            「どのリソースが、いつ、どう変更されたか」セキュリティとコンプライアンスのための構成監査
  ⏺ `Amazon CloudTrail`                     AWSアカウント内のAPI呼び出しとアクティビティを記録・監視するサービス
  - ==!AWS Security Hub==                      セキュリティーアラート / ==ダッシュボード== / ==CSPM==
    - `AWS Secrets Manager`                 機密情報を安全に管理し、自動ローテーション機能により運用負荷を削減
      - `AWS Key Management Service (KMS)`  データの暗号化・復号化に使用する暗号化キーのライフサイクル全体を管理
      - `AWS CloudHSM`                      専有の FIPS 140-2 Level 3 の ==Hardware Security Module== / 暗号鍵の生成、保管、管理
    - `AWS Firewall Manager`                AWS Organizations 全体でファイアウォールルールとセキュリティポリシーを一元管理
      - `AWS Shield`                        ==!Global== / ==DDoS==
      - `AWS WAF (WebApplicationFirewall)`  ==!Global== / ==SQLインジェクション、クロスサイトスクリプティング（XSS）==
    - `Amazon GuardDuty`                    ==悪意==のある異常な動作を継続的に監視・==検出== / ==マルウェア==
    - `Amazon Inspector`                    サービスの==脆弱性==に関する Best Pradctice の順守を==自動的に評価==
    - `Amazon Macie`                        ==Amazon S3== 内の機密データを自動的に検出・分類・保護
    - `Amazon Detective`                    セキュリティ上の問題が発生した際に、根本原因を特定するための探偵の役割
  - `AWS Service Catalog`                   組織で承認されたAWSリソース（CloudFormationテンプレート）をカタログとして提供
⏺ `AWS Health Dashboard`                    ==Service Health Dashboard== と ==Your Account Health== を可視化し、影響を通知 / Event Bridge で自動通知させると便利
- `AWS Service Quotas`                      AWSサービスのクォータ（制限値）を一元管理・表示・引き上げリクエストできるサービス
- `AWS Certificate Manager (ACM)`           SSL/TLS証明書を管理 / ==HTTPS通信== に必要な証明書を、無料で発行・更新・管理

- [AWS Control Tower 概要まとめ](https://zenn.dev/fusic/articles/a2592da23e3db5)
- [始めての AWS Control Tower](https://blog.serverworks.co.jp/2025/07/27/105833)
- [20分で分かる！Control Towerが実現できる効率的なマルチアカウント管理](https://dev.classmethod.jp/articles/cloud-security-fes-control-tower-basic/)
- [AWS Control Towerで実現するマルチアカウント管理の完全ガイド](https://qiita.com/mkydk/items/d56e0e8c742391ae0314)
- [【やってみた】AWS Control Towerワークショップ　その①（Control Towerセットアップ・ユーザー管理）](https://blog.serverworks.co.jp/2024/11/18/125830)

---

## Compliance

- `AWS Artifact`                            コンプライアンス関連ドキュメントへのセルフサービスアクセスを提供するサービス
- `AWS Audit Manager`                       ==監査==準備とコンプライアンス評価を自動化・簡素化するサービス
- `AWS License Manager`                     ソフトウェアライセンスの使用量管理と制限, 「ライセンスを何個使っているか、超過していないか」を管理

- [AWS Artifactってなんだろ？](https://zenn.dev/mn87/articles/de5840d73aec9d)
- [【AWSセキュリティ基礎】AWS Artifact](https://qiita.com/shihandai/items/1109f9d5717a76e11bf4)
- [AWS ArtifactでNDAなしでコンプライアンスレポートがダウンロード](https://dev.classmethod.jp/articles/aws-artiface-compliance-report-download-and-share/)
- [【AWS Audit Manager】フレームワーク、コントロールを継続的デプロイしてみた](https://dev.classmethod.jp/articles/continuous-compliance-monitoring-with-auditmanager/)
- [AWS Audit Managerで監査の準備をしよう](https://blog.serverworks.co.jp/AWS_AuditManager)
- [AWS Audit Managerの概要と主な用語とその関係](https://blog.serverworks.co.jp/overview-of-audit-manager)
- [re:Invent 2024: AWSでのコンプライアンス自動化 - Audit ManagerとConfigの活用](https://zenn.dev/kiiwami/articles/bf066633b1e3c00d)
- [AWS License Manager の新機能で SQL Server のライセンスを切り換えてみた](https://aws.taf-jp.com/blog/60314)

---

## Support

- `AWS Support`                             ==!Global== サービスの利用方法、トラブルシューティング、アーキテクチャガイダンスなど
  - `Basic`                                 ==!無料== / 技術サポートなし / カスタマーサービス（請求・アカウント関連）/ AWS Health Dashboard /AWS Trusted Advisor
  - `Developer`                             ==!MAX($29/M, AWS利用料の3%)== / 技術サポートメール / 個人開発者やスタートアップ向け / 1アカウントにつき1名の連絡先
  - `Business`                              ==!$100/M + α== / 365日技術サポート(chat,phone も) / 中規模のビジネス向け / AWS Trusted Advisorの==全機能==
  - `Enterprise On-Ramp`                    ==!$5,500/M + α== / アーキテクチャレビュー、運用レビュー / 本番システム停止: 30分以内 / 業務重大影響: 30分以内
  - `Enterprise`                            ==!$15,000/M + α== / 専任のTechnical Account Manager（TAM）/ 業務クリティカル停止: 15分以内 / 本番システム停止: 30分以内
- ==!AWS Trusted Advisor==                     ==!Global== / ==Best Practice== 基づき分析改善提案 / 不使用インスタンス /  ==SG チェック==
  - `セキュリティー`                        Basic / AWSのセキュリティー関連機能が有効化されているかどうか、アクセスキーが流出していないかなど、セキュリティーに関するチェック
  - `サービス制限（クォーター）`            Basic / AWSアカウントが作成できるストレージやロールなどのリソースの最大数を監視し、80％を超えた場合にはアラートを発出
  - `コスト最適化`                          Business / サービスや設定の使用状態をチェックし、活用されていないサービスを洗い出してコスト最適化の提案
  - `パフォーマンス`                        Business / AWSリソースのパフォーマンス向上のため、スループットや有効化すべき設定をチェック
  - `耐障害性`                              Business / 耐障害性、可用性や信頼性を向上させるため、オートスケーリングやヘルスチェック、その他有効／無効にすべき設定をチェック
  - `運用上の優秀性`                        Business / AWS上のサービスが安定して稼働していること、問題発生時に迅速な対応を行える状態であることを確認
- ==!AWS Compute Optimizer==                   直近 14 日間のコンピュータリソースの最適化提案 / EC2, Auto Scaling Groups, EBSボリューム, Lambda / ==!14日以上設定だと課金==
- `AWS Well-Architected Tool`               AWSワークロードをWell-Architectedフレームワークに基づいて==アーキテクチャの評価を提供==
- `Amazon QuickSight`                       ==BI==
⏺ ==!Amazon CloudWatch==                       リソースの監視・管理 / メトリクス収集、ログ管理、アラーム設定、ダッシュボード作成
⏺ ==!Amazon X-Ray==                            分散アプリケーションのパフォーマンス分析とデバッグを支援するサービス
⏺ `Amazon OpenSearch Service`               フルマネージド型の検索・分析サービス。OpenSearch, Elasticsearchをベースにした検索・分析エンジン

- [AWS サポートに技術的な問い合わせをする手順をまとめてみた](https://zenn.dev/kobayasd/articles/67b0058552336a)
- [AWS入門ブログリレー2024〜AWS Compute Optimizer編〜](https://dev.classmethod.jp/articles/introduction-2024-aws-compute-optimizer/)

---

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
- `AWS Resource Access Manager`             (RAM) マルチアカウント環境でリソースを効率的に共有し、重複を避ける
- `AWS Data Exchange`                       ==データマーケットプレイス== / ライセンス管理と課金 / データ更新の自動化
## CLI & IaC
- `AWS CLI`                                 アクセスキー
- `AWS Cloud Development Kit (CDK)`
- `AWS CloudFormation`
- `AWS Systems Manager (SSM)`               AWSとオンプレミスのインフラストラクチャを一元的に管理・運用するための統合サービス
- `AWS CodeBuild`                           コンパイル、テスト実行し、デプロイ可能なソフトウェアパッケージを生成する ==CI== サービス
- `AWS CodePipeline`                        ソフトウェアのリリースプロセスを自動化するフルマネージドな ==CD== サービス
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
⏺ `AWS Step Functions`                      複数のサービスを視覚的な Workflow / 分散 App や MicroService を構築, オーケストレーション
- `Amazon EMR (Elastic MapReduce)`          Big data processing platform, ==MapReduce (Spark/Hadoop/Presto/Hive)==
- `AWS Glue`                                ==ETL== / Source (S3, RDS, Redshift, DynamoDB, オンプレミス)
- `AWS Data Pipeline`                       サービス間でデータを自動的に移動 / スケジュール実行可能 / (S3,RDS,DynamoDB,Redshift,オンプレ) / EMR でデータ処理可能
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

---

- AWS Lake Formation
- Amazon Managed Streaming for Apache Kafka (Amazon MSK)
- Amazon AppFlow
- Saving Plans
- AWS Serverless Application Repository
- VMware Cloud on AWS
- Amazon ECS Anywhere
- Amazon EKS Anywhere
- Amazon EKS Distro
- Amazon Keyspaces (for Apache Cassandra)
- Amazon Quantum Ledger Database (Amazon QLDB)
- AWS Device Farm
- Amazon Pinpoint
- Amazon Forecast
- Amazon Fraud Detector
- Amazon Managed Grafana
- Amazon Managed Service for Prometheus
- AWS Proton
- Amazon Elastic Transcoder
- Amazon Kinesis Video Streams
- AWS Transfer Family
