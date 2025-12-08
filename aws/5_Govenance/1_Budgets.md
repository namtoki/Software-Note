# AWS Budgets

```
予算設定 (例: $1,000/月)
      ↓
閾値設定 (例: 80%, 100%)
      ↓ 超過時
通知: SNS, Email, Chatbot
      +
自動アクション (オプション)
```

## Overview
- コスト管理サービス:             ==予算を設定し、超過時にアラート== / ==1 時間単位== / ==!3 予算目から$0.02/日/予算==
  - types (追跡対象):             コスト、使用量、RI/Savings Plans カバレッジ
    - `Cost Budget`:                金額ベースの予算 (例: 月$1,000)
    - `Usage Budget`:               使用量ベースの予算 (例: EC2 100時間)
    - `RI Utilization`:             RI の利用率を監視
    - `RI Coverage`:                RI でカバーされている割合を監視
    - `Savings Plans`:              Savings Plans の利用率/カバレッジ
  - Actions:
    - `Alerts`:
      - `Email`:                    最大10アドレス
      - `SNS`:                      Lambda 連携等
      - `Chatbot`:                  Slack, Teams
    - `Budget Actions`:             ==予算超過時に自動でアクションを実行==
      - `IAMポリシー適用`:          特定のリソース作成を禁止
      - `SCPアタッチ`:              Organizations で制限
      - `EC2/RDS停止`:              インスタンスを停止
