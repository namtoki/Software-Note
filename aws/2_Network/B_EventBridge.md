# Amazon EventBridge

```
イベントソース                     ターゲット
┌─────────────┐                  ┌──────────────┐
│ AWS サービス│                  │   Lambda     │
│ (S3, EC2等) │                  │   SQS/SNS    │
├─────────────┤  → EventBridge → │Step Functions│
│    SaaS     │     (ルール)     │   Kinesis    │
│ (Zendesk等) │                  │   API GW     │
├─────────────┤                  │     etc.     │
│ カスタムApp │                  └──────────────┘
└─────────────┘
```

## Overview
- イベント駆動アーキテクチャ:     AWS, SaaS, カスタムアプリからのイベントをルーティング
  - 構成:
    - `イベントソース`:             AWS サービス (EC2, S3等) / SaaS (Zendesk等) / カスタムアプリ
    - `イベントバス`:               イベントを受信するパイプライン (default / カスタム / パートナー)
    - `ルール`:                     イベントをフィルタリングしてターゲットに送信
      - `イベントパターン`:         イベント内容でマッチ (例: EC2 停止時)
      - `スケジュール`:             cron/rate 式で定期実行 (例: 毎日 9:00)
    - `ターゲット`:                 Lambda / SQS / SNS / Step Functions / API Gateway 等 (最大 5個/ルール)
