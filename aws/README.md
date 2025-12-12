# AWS Notes

AWS SAA (Solutions Architect Associate) 学習ノート

## ディレクトリ構成

aws/
├── Overview.md
│
├── AI/
│   ├── SageMakerAI.md             # ML プラットフォーム
│   ├── Forecast.md                # 時系列予測
│   ├── Kendra.md                  # エンタープライズ検索
│   ├── Q.md                       # AI アシスタント
│   ├── Lex.md                     # チャットボット
│   ├── Rekognition.md             # 画像/動画分析
│   ├── Textract.md                # Text 抽出
│   ├── Transcribe.md              # Voice -> Text
│   ├── Comprehend.md              #          Text 要約
│   ├── Translate.md               #          Text -> Text
│   └── Polly.md                   #                  Text -> Voice
│
├── Compliance/
│   ├── Artifact.md                # AWS のコンプライアンスレポート (SOC, PCI, ISO 等) / AWS との契約 (BAA, NDA 等) の確認・同意
│   ├── AuditManager.md            # 監査管理自動化
│   └── LicenseManager.md          # ライセンス管理
│
├── Computing/                     # コンピューティング
│   ├── Amplify.md                 # フルスタック開発
│   ├── Batch.md                   # バッチ処理 / ==Job Definition -> Job Queue -> Compute Environment / ジョブ数に応じて自動スケール==
│   ├── Cognito.md                 # 認証/認可 / ==JWT トークン== / ==一時的な AWS 認証情報 (STS)==
│   ├── EC2.md                     # 仮想サーバー
│   ├── ECS.md                     # コンテナ (Docker)
│   ├── EKS.md                     # コンテナ (Kubernetes)
│   ├── EVS.md                     # VMware 環境
│   ├── ElasticBeanstalk.md        # PaaS
│   ├── Lambda.md                  # サーバーレス関数
│   └── LightSail.md               # シンプル VPS
│
├── Database/                      # データベース
│   ├── EMR.md                     # ビッグデータ処理
│   ├── LakeFormation.md           # データレイク管理
│   ├── Redshift.md                # データウェアハウス
│   ├── NoSQL/
│   │   ├── DocumentDB.md          # MongoDB 互換
│   │   ├── DynamoDB.md            # キーバリュー
│   │   ├── ElastiCache.md         # インメモリキャッシュ
│   │   ├── Keyspaces.md           # Cassandra 互換
│   │   ├── Neptune.md             # グラフDB
│   │   └── QLDB.md                # 台帳DB
│   ├── RDB/
│   │   ├── Aurora.md              # 高性能 RDB
│   │   └── RDS.md                 # マネージド RDB
│   └── Xfer/
│       ├── DMS.md                 # DB 移行
│       └── SCT.md                 # スキーマ変換
│
├── Govenance/                     # ガバナンス
│   ├── CertificateManager.md      # SSL/TLS 証明書
│   ├── ServiceQuotas.md           # サービス制限
│   ├── Account/
│   │   ├── ControlTower.md        # マルチアカウント設定
│   │   ├── IAMIdentityCenter.md   # SSO
│   │   ├── Organization.md        # マルチアカウント管理
│   │   └── RAM.md                 # リソース共有
│   ├── Cost/
│   │   ├── BillingAndCostManagement.md
│   │   ├── Budgets.md             # 予算アラート
│   │   ├── CostAndUsageReports.md # 詳細レポート
│   │   └── CostExplorer.md        # コスト分析
│   └── Security/
│       ├── CloudHSM.md            # 専用 HSM
│       ├── HealthDashboard.md     # サービス状態
│       ├── KMS.md                 # キー管理
│       ├── SecretsManager.md      # シークレット管理
│       └── SecurityHub.md         # セキュリティ統合
│
├── Network/                       # ネットワーク
│   ├── VPC.md                     # 仮想ネットワーク
│   ├── Bridge/
│   │   ├── AppFlow.md             # SaaS 連携
│   │   ├── EventBridge.md         # イベントバス
│   │   ├── MQ.md                  # メッセージブローカー
│   │   ├── SNS.md                 # Pub/Sub
│   │   └── SQS.md                 # メッセージキュー
│   ├── Edge/
│   │   ├── CloudFront.md          # CDN
│   │   ├── IoTCore.md             # IoT
│   │   ├── LocalZones.md          # ローカルゾーン
│   │   ├── Outposts.md            # オンプレ AWS
│   │   └── WaveLength.md          # 5G エッジ
│   └── Gateway/
│       ├── APIGateway.md          # API 管理
│       ├── AppSync.md             # GraphQL
│       ├── ELB.md                 # ロードバランサー
│       ├── GlobalAccelerator.md   # グローバル高速化
│       ├── Route53.md             # DNS
│       └── StorageGateway.md      # ハイブリッドストレージ
│
├── Operation/                     # 運用
│   ├── AWSProton.md               # コンテナ/サーバーレステンプレート
│   ├── CloudFormation.md          # IaC
│   ├── CloudTrail.md              # API 監査ログ
│   ├── CloudWatch.md              # モニタリング
│   ├── CodePipeline.md            # CI/CD
│   ├── Config.md                  # 構成管理
│   ├── DataExchange.md            # データマーケット
│   ├── ManagedGrafana.md          # 可視化
│   ├── Marketplace.md             # ソフトウェア購入
│   ├── ServerlessApplicationRepository.md
│   ├── ServiceCatalog.md          # 製品カタログ
│   ├── StepFunctions.md           # ワークフロー
│   ├── SystemsManager.md          # 運用管理
│   └── Advice/
│       ├── ComputeOptimizer.md    # リソース最適化
│       ├── TrustedAdvisor.md      # ベストプラクティス
│       └── WellArchitectedTool.md # 設計レビュー
│
├── Storage/                       # ストレージ
│   ├── Backup.md                  # バックアップ
│   ├── DirectoryService.md        # AD 連携
│   ├── File/
│   │   ├── EFS.md                 # NFS ファイルシステム
│   │   └── FSx.md                 # Windows/Lustre
│   ├── Object/
│   │   ├── Athena.md              # S3 クエリ
│   │   ├── MediaConvert.md        # 動画変換
│   │   └── S3.md                  # オブジェクトストレージ
│   └── Xfer/
│       ├── DataPipeline.md        # データ移動
│       ├── DataSync.md            # データ同期
│       ├── SnowFamily.md          # 物理デバイス移行
│       └── TransferFamily.md      # SFTP/FTP
│
├── Tools/                         # その他ツール
│   ├── ApacheKafka.md             # ストリーミング
│   ├── AppStream.md               # アプリストリーミング
│   ├── DeviceFarm.md              # モバイルテスト
│   ├── ElasticDisasterRecovery.md # DR
│   ├── Glue.md                    # ETL
│   ├── Kinesis.md                 # リアルタイムストリーミング
│   ├── MigrationEvaluator.md      # 移行評価
│   ├── MigrationHub.md            # 移行管理
│   ├── OpenSearch.md              # 検索/分析
│   ├── QuickSight.md              # BI
│   ├── WorkSpaces.md              # 仮想デスクトップ
│   └── X-Ray.md                   # 分散トレーシング
│
└── others/                        # その他
    ├── Connect.md                 # コンタクトセンター
    ├── Pinpoint.md                # マーケティング
    └── SES.md                     # メール送信
