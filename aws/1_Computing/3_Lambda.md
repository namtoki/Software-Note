# AWS Lambda

```
+----------------------------------------------------------+
|                    AWS Lambda                            |
|  +----------------------------------------------------+  |
|  |               Lambda Function                      |  |
|  |  +------------------+  +------------------+        |  |
|  |  |   Handler Code   |  |   Runtime        |        |  |
|  |  +------------------+  +------------------+        |  |
|  |  +------------------+  +------------------+        |  |
|  |  |   Memory (RAM)   |  |   Timeout        |        |  |
|  |  |   128MB - 10GB   |  |   max 15 min     |        |  |
|  |  +------------------+  +------------------+        |  |
|  |  +----------------------------------------------+  |  |
|  |  |              Event Source (Trigger)          |  |  |
|  |  +----------------------------------------------+  |  |
|  +----------------------------------------------------+  |
+----------------------------------------------------------+
```

## Overview
- Serverless Function:
  - Memory:                       128MB〜10,240MB (==10GB==) / 1MB単位
  - vCPU:                         ==メモリに比例して自動割り当て== (1,769MBで1vCPU相当)
  - Timeout:                      ==最大15分 (900秒)== / デフォルト3秒
  - Ephemeral Storage (/tmp):     512MB〜10,240MB / 一時ファイル用
  - 環境変数:                     キーバリューペア / ==KMSで暗号化==
    - 保存時の暗号化:             ==デフォルトでAWS管理キーで自動暗号化==
    - カスタマー管理キー (CMK):   ==独自のKMSキー== を指定可能 / より厳密なアクセス制御
    - 転送中の暗号化:             コンソール表示時は復号 / ==Secrets Helperで追加暗号化可==
    - 機密情報:                   Secrets Manager または Parameter Store 推奨
  - Source Code (Deployment):
    - type:
      - ZIP (直接アップロード):   50MB (圧縮)
      - ZIP (S3経由):             250MB (解凍後)
      - Container Image:          10GB
    - `Lambda Layers`:              共有 / ==最大5個== / 合計250MB制限 / ==/opt== に展開 / ==Container は不可==
    - `Versions`:                   イミュータブルなスナップショット / $LATEST は常に最新
    - `Alias`:                      バージョンへのポインタ / ==加重トラフィック分散可 (カナリアデプロイ)==
  - Invocation:
    - Synchronous (同期):         呼び出し元が応答を待つ / API Gateway, ALB, CloudFront, Cognito
    - Asynchronous (非同期):      呼び出し元は即座に戻る / ==2回リトライ== / S3, SNS, EventBridge
      - Destinations:             成功/失敗時の宛先設定 (SQS, SNS, Lambda, EventBridge)
      - `Dead Letter Queue (DLQ)`:  失敗イベントをSQS/SNSに送信 (非推奨、Destinations推奨)
    - `Event Source Mapping`:       ストリーム/キューをポーリング / SQS, Kinesis, DynamoDB Streams
      - Batch Size:               一度に処理するレコード数
      - Batch Window:             バッチを収集する最大時間

## Options
- `Concurrent Executions`:          同時に実行できる関数インスタンス数 / Region Default: ==1,000== (引き上げ可能)
  - `Reserved Concurrency`:         ==特定関数用に確保== / 他関数の影響を防ぐ / ==無料==
  - `Provisioned Concurrency`:      ==事前にウォーム状態を維持== / Cold Start回避 / ==!有料==
    - `Cold Start`:                 新規インスタンス起動 / 初期化に時間がかかる
      - 要因:                     初回実行, スケールアウト時, コード更新後
      - 対策:                     ==Provisioned Concurrency==, メモリ増加, 軽量ランタイム
    - `Warm Start`:                 既存インスタンス再利用 / 高速
  - `Throttling`:                   上限超過時は ==429 エラー== / 非同期は自動リトライ
- `VPC Lambda`:                     プライベートリソース (RDS, ElastiCache等) にアクセス
  - 設定:                         VPC, Subnet, Security Group を指定
  - ENI:                          ==Hyperplane ENI== を使用 (従来より高速)
  - インターネットアクセス:       ==NAT Gateway 必須== (Public Subnet不可)
  - AWSサービスアクセス:          ==VPC Endpoint 推奨==
- `Execution Role`:                 Lambda が他AWSサービスにアクセスするための ==IAM Role==
- `Resource-based Policy`:          他アカウント/サービスからのアクセス許可
- `Code Signing`:                   署名されたコードのみデプロイ許可
