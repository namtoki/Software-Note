# Amazon ECS (Elastic Container Service)

```
+----------------------------------------------------------+
|                      ECS Cluster                         |
|  +----------------------------------------------------+  |
|  |                     Service                        |  |
|  |  +--------------+  +--------------+                |  |
|  |  |    Task      |  |    Task      | <- 同一定義    |  |
|  |  | +----------+ |  | +----------+ |                |  |
|  |  | |Container | |  | |Container | |                |  |
|  |  | +----------+ |  | +----------+ |                |  |
|  |  +--------------+  +--------------+                |  |
|  +----------------------------------------------------+  |
+----------------------------------------------------------+
```

## Functions
- 構成:
  - `Cluster`:                  タスクやサービスの論理グループ
    - `Service`:                指定数のタスクを==常に維持== / ALB/NLBとの連携 / Rolling Update / ==Auto Scaling==
      - `Task Definition`:      コンテナの設定を定義するJSON (イメージ, CPU, メモリ, ポート等)
        - `Task`:               Task Definitionから起動されるコンテナの実行単位
- 起動タイプ:
  - `Fargate`:                  サーバーレス / インフラ管理不要 / タスク単位課金 / GPU非対応
    - `Ephemeral Storage`:      タスクのライフサイクルに紐づく一時ストレージ / 永続性なし
    - `EFS`:                    複数タスク間で共有可能 / ==永続性あり==
  - `EC2`:                      フルコントロール / GPU対応 / RI,Spot活用可 / インフラ管理必要
    - `Docker Volume`:          EC2インスタンス上のDockerボリューム
    - `Bind Mount`:             ホストのディレクトリをマウント
  - `ECS Anywhere`:             オンプレミス/エッジで実行 / SSM Agent必須 / 常時AWS接続必須
- IAMロール:
  ```
  +--------------------------------------+
  |              ECS Task                |
  |  +-------------------------------+   |
  |  |     Container (アプリ)         |   |
  |  |        |                      |   |
  |  |        v Task Role            |   |
  |  |    +----------------+         |   |
  |  |    | S3, DynamoDB等 |         |   |
  |  |    +----------------+         |   |
  |  +-------------------------------+   |
  |                                      |
  |  ECS Agent <- Execution Role         |
  +--------------------------------------+
  ```
  - `Execution Role`:           ==ECR==からイメージをプル / CloudWatch Logs 送信 / Secrets Manager, Parameter Store
  - `Task Role`:                S3へのアクセス / DynamoDBへのアクセス / 他のAWSサービスへのアクセス
- ネットワークモード:
  - `awsvpc`:                   ==Fargate必須== / タスクごとにENI割当 / Security Group適用可
  - `bridge`:                   EC2のみ / Dockerのデフォルト / 動的ポートマッピング
  - `host`:                     EC2のみ / ホストのネットワーク直接使用
- ロードバランサー連携:
  - `ALB`:                      パスベース/ホストベースルーティング / ==動的ポートマッピング== / 複数ターゲットグループ
  - `NLB`:                      TCP/UDP / 低レイテンシー / 固定IP
- Auto Scaling:
  - `Service Auto Scaling`:     ==タスク数==を調整 / Target Tracking (CPU,メモリ) / Step Scaling / Scheduled
  - `Capacity Provider`:        EC2起動タイプ時 / ASGと連携 / マネージドスケーリング
- ECR (Elastic Container Registry):
  - 概要:                     フルマネージドコンテナレジストリ / Docker Hub代替
  - セキュリティ:             ==イメージスキャン== / 暗号化 / IAMによるアクセス制御
  - ライフサイクル:           古いイメージの自動削除ポリシー
- Secrets管理:
  - `Secrets Manager`:          DB認証情報等 / 自動ローテーション / Task Definition内で参照
  - `Parameter Store`:          設定値 / SecureString (KMS暗号化) / 階層構造
- ログ:
  - `awslogs`:                  CloudWatch Logsへ送信 / Task Definition内で設定 / Execution Role必要
