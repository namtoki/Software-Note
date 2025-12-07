# AWS Lambda

```
+------------------------------------------------------------------+
|                        AWS Lambda                                 |
|  +------------------------------------------------------------+  |
|  |                    Lambda Function                         |  |
|  |  +------------------+  +------------------+                |  |
|  |  |   Handler Code   |  |   Runtime        |                |  |
|  |  +------------------+  +------------------+                |  |
|  |  +------------------+  +------------------+                |  |
|  |  |   Memory (RAM)   |  |   Timeout        |                |  |
|  |  |   128MB - 10GB   |  |   max 15 min     |                |  |
|  |  +------------------+  +------------------+                |  |
|  |  +----------------------------------------------+          |  |
|  |  |              Event Source (Trigger)          |          |  |
|  |  +----------------------------------------------+          |  |
|  +------------------------------------------------------------+  |
+------------------------------------------------------------------+
```

## Core Concepts
- `Serverless`:                            サーバー管理不要 / 自動スケール / 使用した分だけ課金
- `Function`:                              コードをデプロイして実行 / ステートレス
- `Event-driven`:                          イベントをトリガーに実行

## Configuration
- Memory:
  - 範囲:                                  ==128MB〜10,240MB (10GB)== / 1MB単位
  - vCPU:                                  ==メモリに比例して自動割り当て== (1,769MBで1vCPU相当)
- Timeout:                                 ==最大15分 (900秒)== / デフォルト3秒
- Ephemeral Storage (`/tmp`):              ==512MB〜10,240MB== / 一時ファイル用
- Environment Variables:                   キーバリューペア / ==KMSで暗号化==

## Deployment
- Package Size:
  - ZIP (直接アップロード):               ==50MB (圧縮)==
  - ZIP (S3経由):                         ==250MB (解凍後)==
  - Container Image:                      ==10GB==
- `Lambda Layers`:                         共通ライブラリを共有 / ==最大5レイヤー== / 合計250MB制限
- `Versions`:                              イミュータブルなスナップショット / $LATEST は常に最新
- `Alias`:                                 バージョンへのポインタ / ==加重トラフィック分散可== (カナリアデプロイ)

## Invocation
- `Synchronous (同期)`:                    呼び出し元が応答を待つ / API Gateway, ALB, CloudFront
- `Asynchronous (非同期)`:                 呼び出し元は即座に戻る / ==2回リトライ== / S3, SNS, EventBridge
  - `Destinations`:                        成功/失敗時の宛先設定 (SQS, SNS, Lambda, EventBridge)
  - `Dead Letter Queue (DLQ)`:             失敗イベントをSQS/SNSに送信 (非推奨、Destinations推奨)
- `Event Source Mapping`:                  ストリーム/キューをポーリング / SQS, Kinesis, DynamoDB Streams
  - Batch Size:                            一度に処理するレコード数
  - Batch Window:                          バッチを収集する最大時間

## Triggers (Event Sources)
| サービス | 呼び出しタイプ | ユースケース |
|---------|---------------|-------------|
| API Gateway | 同期 | REST/HTTP API |
| ALB | 同期 | HTTP リクエスト処理 |
| S3 | 非同期 | オブジェクト作成/削除時の処理 |
| SNS | 非同期 | Pub/Sub メッセージング |
| EventBridge | 非同期 | スケジュール実行、イベント駆動 |
| SQS | Event Source Mapping | キューメッセージ処理 |
| Kinesis | Event Source Mapping | ストリームデータ処理 |
| DynamoDB Streams | Event Source Mapping | テーブル変更検知 |
| Cognito | 同期 | 認証フロー カスタマイズ |

## Concurrency
- `Concurrent Executions`:                 同時に実行できる関数インスタンス数
  - リージョンデフォルト:                  ==1,000== (引き上げ可能)
  - `Reserved Concurrency`:                ==特定関数用に確保== / 他関数の影響を防ぐ / ==無料==
  - `Provisioned Concurrency`:             ==事前にウォーム状態を維持== / Cold Start回避 / ==有料==
- Throttling:                              上限超過時は ==429 エラー== / 非同期は自動リトライ

## Cold Start vs Warm Start
- `Cold Start`:                            新規インスタンス起動 / 初期化に時間がかかる
  - 要因:                                  初回実行, スケールアウト時, コード更新後
  - 対策:                                  ==Provisioned Concurrency==, メモリ増加, 軽量ランタイム
- `Warm Start`:                            既存インスタンス再利用 / 高速

## VPC Lambda
- `VPC 接続`:                              プライベートリソース (RDS, ElastiCache等) にアクセス
  - 設定:                                  VPC, Subnet, Security Group を指定
  - ENI:                                   ==Hyperplane ENI== を使用 (従来より高速)
  - インターネットアクセス:                ==NAT Gateway 必須== (Public Subnet不可)
  - AWSサービスアクセス:                   ==VPC Endpoint 推奨==

## Edge Computing
- `Lambda@Edge`:                           CloudFront エッジで実行 / ==Node.js, Python のみ==
  - 実行ポイント:                          Viewer Request/Response, Origin Request/Response
  - メモリ:                                128MB〜10GB (Viewer), 128MB〜10GB (Origin)
  - タイムアウト:                          ==5秒 (Viewer), 30秒 (Origin)==
  - ユースケース:                          A/Bテスト, 認証, ヘッダー操作, URL書き換え
- `CloudFront Functions`:                  より軽量・高速 / ==JavaScript のみ==
  - 実行ポイント:                          ==Viewer Request/Response のみ==
  - 実行時間:                              ==1ms未満==
  - ユースケース:                          キャッシュキー正規化, ヘッダー操作, URL リダイレクト

## Monitoring & Logging
- `CloudWatch Logs`:                       自動でログ出力 / ==実行ロールに権限必須==
- `CloudWatch Metrics`:                    Invocations, Duration, Errors, Throttles, ConcurrentExecutions
- `X-Ray`:                                 分散トレーシング / ==Active Tracing を有効化==

## Security
- `Execution Role`:                        Lambda が他AWSサービスにアクセスするための ==IAM Role==
- `Resource-based Policy`:                 他アカウント/サービスからのアクセス許可
- `KMS`:                                   環境変数の暗号化
- `Secrets Manager`:                       認証情報の安全な管理 (ハードコード禁止)
- `Code Signing`:                          署名されたコードのみデプロイ許可

## Pricing
- `リクエスト数`:                          100万リクエストあたり $0.20
- `実行時間`:                              GB-秒 単位 / メモリ × 実行時間
- `Free Tier`:                             ==100万リクエスト/月, 40万GB-秒/月==

## Best Practices (SAA試験頻出)
- ステートレス設計:                        状態はS3, DynamoDB等に保存
- 環境変数活用:                            設定値をコードから分離
- 接続再利用:                              ハンドラー外でDB接続を初期化
- 最小権限の原則:                          実行ロールに必要最小限の権限
- エラーハンドリング:                      DLQ/Destinations で失敗を捕捉
