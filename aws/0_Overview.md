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

---

## Operation
  - `AWS Service Catalog`                   組織で承認されたAWSリソース（CloudFormationテンプレート）をカタログとして提供

## Govenance
  - `AWS Organizations`                     ==!Global== / 複数 AWS アカウントに Service Control Policy (==SCP==) を ==OU==（Organizational Unit）単位で適用
  - `AWS IAM Identity Center`               ==!Global== / 1回のログインで全アカウントにアクセス可能 / 一元的なアクセス管理 / 外部IDプロバイダー連携 (SSO)
  - ==!AWS Security Hub==                      セキュリティーアラート / ==ダッシュボード== / ==CSPM==
    - `AWS Firewall Manager`                AWS Organizations 全体でファイアウォールルールとセキュリティポリシーを一元管理
      - `AWS Shield`                        ==!Global== / ==DDoS==
      - `AWS WAF (WebApplicationFirewall)`  ==!Global== / ==SQLインジェクション、クロスサイトスクリプティング（XSS）==
    - `Amazon GuardDuty`                    ==悪意==のある異常な動作を継続的に監視・==検出== / ==マルウェア==
    - `Amazon Inspector`                    サービスの==脆弱性==に関する Best Pradctice の順守を==自動的に評価==
    - `Amazon Macie`                        ==Amazon S3== 内の機密データを自動的に検出・分類・保護
    - `Amazon Detective`                    セキュリティ上の問題が発生した際に、根本原因を特定するための探偵の役割
    - `Amazon Fraud Detector`               ==不正検出== / 機械学習を活用して、オンライン詐欺や不正行為をリアルタイムで検出

## Tools
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
