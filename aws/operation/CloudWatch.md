# CloudWatch

- [AWSブログリレー：Amazon CloudWatchとは？無料枠で始めるAWSシステム監視のメリットと使い方](https://iret.media/172240)

## Terminology
- `Metrics`:                数値データの時系列データ（CPU使用率等）
  - `標準メトリクス`:       AWSが自動収集（無料）
  - `カスタムメトリクス`    独自に送信（有料）
  - 補足
    - EC2 標準メトリクスに含まれない:
      - メモリ使用率 ← カスタムメトリクスで取得
      - ディスク使用率 ← CloudWatch Agent が必要
- `Logs` | ログデータの収集・保存・分析 |
- `Alarms` | メトリクスの閾値監視・通知 |
- `Events / EventBridge` | イベント駆動のアクション実行 |
- `Dashboards` | 可視化ダッシュボード |

### 料金

| 項目 | 料金 |
|-----|------|
| 基本メトリクス（5分間隔） | 多くのAWSサービスで無料 |
| 詳細メトリクス（1分間隔） | 有料 |
| カスタムメトリクス | メトリクス数に応じた課金 |
| ログ | データ取り込み量と保存量に応じた課金 |
| ダッシュボード | 月額 $3/ダッシュボード（最初の3つは無料） |


### メトリクス解像度

| 解像度 | 間隔 | 用途 |
|-------|------|------|
| **Standard** | 5分 | デフォルト（無料） |
| **Detailed** | 1分 | 詳細モニタリング（有料） |
| **High Resolution** | 1秒 | カスタムメトリクスのみ |

## Logs（ログ）

### 構成要素

```
Log Groups（ログループ）
    └── Log Streams（ログストリーム）
            └── Log Events（ログイベント）
```

### ログの収集元

| ソース | 方法 |
|-------|------|
| EC2 | CloudWatch Agent |
| Lambda | 自動 |
| API Gateway | 設定で有効化 |
| VPC Flow Logs | VPC設定 |
| CloudTrail | 設定で有効化 |
| Route 53 | DNSクエリログ |

### 重要機能

| 機能 | 説明 |
|-----|------|
| **Metric Filters** | ログからメトリクスを生成 |
| **Subscription Filters** | ログをリアルタイム転送 |
| **Log Insights** | ログのクエリ・分析 |
| **保持期間** | 1日〜無期限（設定可能） |

### ログのエクスポート先

```
CloudWatch Logs
    ├── S3（バッチエクスポート）
    ├── Kinesis Data Firehose（リアルタイム）
    ├── Kinesis Data Streams（リアルタイム）
    ├── Lambda（リアルタイム処理）
    └── OpenSearch（分析）
```

## Alarms（アラーム）

### アラーム状態

| 状態 | 説明 |
|-----|------|
| **OK** | 閾値内 |
| **ALARM** | 閾値超過 |
| **INSUFFICIENT_DATA** | データ不足 |

### アラームアクション

```yaml
ALARM 状態になったら:
  - SNS 通知
  - Auto Scaling アクション
  - EC2 アクション（停止/終了/再起動/復旧）
```

### Composite Alarms（複合アラーム）

```
複数のアラームを AND/OR で組み合わせ

Alarm A (CPU > 80%) AND Alarm B (Memory > 90%)
    → 両方 ALARM の時だけ通知
```

## CloudWatch Agent

### 用途

| 機能 | 説明 |
|-----|------|
| **メモリ使用率** | 標準メトリクスにないため必要 |
| **ディスク使用率** | 標準メトリクスにないため必要 |
| **カスタムログ** | アプリケーションログの収集 |

### 設定ファイル

```
SSM Parameter Store に保存 → 複数EC2で共有可能
```

## EventBridge（旧 CloudWatch Events）

### イベント駆動アーキテクチャ

```
イベントソース → EventBridge → ターゲット
    │                              │
  EC2状態変化              Lambda, SNS, SQS,
  S3イベント               Step Functions等
  スケジュール
```

### スケジュール実行

```
cron(0 12 * * ? *)  → 毎日12時に実行
rate(5 minutes)     → 5分ごとに実行
```

## Container Insights

| 対象 | 説明 |
|-----|------|
| **ECS** | コンテナレベルのメトリクス |
| **EKS** | Kubernetes メトリクス |
| **Fargate** | サーバーレスコンテナ |

## 試験での出題パターン

| シナリオ | 解答 |
|---------|------|
| EC2のメモリ使用率を監視したい | **CloudWatch Agent** + カスタムメトリクス |
| CPU 80%超で通知したい | **CloudWatch Alarms** + SNS |
| ログからエラー数をカウント | **Metric Filters** |
| ログをリアルタイムで処理 | **Subscription Filters** + Lambda/Kinesis |
| 複数条件でアラート | **Composite Alarms** |
| 定期的にLambdaを実行 | **EventBridge** スケジュール |
| コンテナのメトリクス監視 | **Container Insights** |
| ログを長期保存・分析 | S3 エクスポート + Athena |

## 類似サービスとの使い分け

| サービス | 用途 |
|---------|------|
| **CloudWatch** | メトリクス・ログ・アラーム |
| **CloudTrail** | API呼び出し履歴（監査） |
| **X-Ray** | 分散トレーシング |
| **AWS Config** | リソース構成変更の追跡 |
