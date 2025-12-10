# Amazon ECS (Elastic Container Service)

```
+-------------------------------------------+
|                ECS Cluster                |
|  +-------------------------------------+  |
|  |               Service               |  |
|  |  +--------------+  +--------------+ |  |
|  |  |    Task      |  |    Task      | |  |
|  |  | +----------+ |  | +----------+ | |  |
|  |  | |Container | |  | |Container | | |  |
|  |  | +----------+ |  | +----------+ | |  |
|  |  +--------------+  +--------------+ |  |
|  +-------------------------------------+  |
+-------------------------------------------+
```

## Overview
- コンテナサービス:
  - 構成:
    - `Cluster`:                タスクやサービスの論理グループ
      - `Service`:              指定数のタスクを==常に維持== / ALB/NLBとの連携 / ==Rolling Update== / ==Auto Scaling==
        - `Task Definition`:    JSON (イメージ, CPU, メモリ, ポート等) / ==ネットワークモード== / ==Secrets 管理==
          - `Task`:             Task Definition から起動されるコンテナの実行単位
  - 起動タイプ:
    - `Fargate`:                ==!Task 単位の vCPU + メモリの秒単位課金== / サーバーレス / インフラ管理不要 / ==GPU非対応==
      - `Ephemeral Storage`:    タスクのライフサイクルに紐づく一時ストレージ / 永続性なし
      - `EFS`:                  複数タスク間で共有可能 / 永続性あり
    - `EC2`:                    フルコントロール / GPU対応 / RI,Spot活用可 / インフラ管理必要
      - `Docker Volume`:        EC2インスタンス上のDockerボリューム
      - `Bind Mount`:           ホストのディレクトリをマウント
    - `ECS Anywhere`:           オンプレミス/エッジで実行 / SSM Agent必須 / 常時AWS接続必須
  - IAMロール:
    - `Execution Role`:         ==Agent== / ECR からイメージをプル / CloudWatch Logs 送信 / Secrets Manager, Parameter Store
    - `Task Role`:              ==Task== / S3へのアクセス / DynamoDBへのアクセス / 他のAWSサービスへのアクセス
  - ネットワークモード:
    - `awsvpc`:                 ==Fargate必須== / Task ごとにENI割当 / Task ごとに IP / Task に SG 適用
    - `bridge`:                 EC2のみ / Host の ENI 共有 / Host の IP / Host に SG 適用 / 動的ポートマッピング
    - `host`:                   EC2のみ / Host の ENI 共有 / Host の IP / Host に SG 適用 / ホストのネットワーク直接使用
    - `none`:                   EC2のみ / 
  - Auto Scaling:
    - `Service Auto Scaling`:   ==タスク数を自動調整== / Target Tracking (CPU,メモリ) / Step Scaling / Scheduled (指定時間に)
    - `Capacity Provider`:      ==EC2 インスタンス数を自動調整 (ASG と連携)==
      - `Managed Scaling`:      タスクに必要な EC2 を自動追加/削除
      - `Target Capacity`:      EC2 使用率の目標値 (例: 80%)
  - `ECR`:                      Elastic Container Registry / フルマネージドコンテナレジストリ / Docker Hub 代替
    - セキュリティ:           イメージスキャン / 暗号化 / IAMによるアクセス制御
    - ライフサイクル:         古いイメージの自動削除ポリシー
  - ログ:
    - `awslogs`:                CloudWatch Logsへ送信 / Task Definition内で設定 / Execution Role必要
