# Amazon MQ

## Overview
- メッセージブローカー:                   ==ActiveMQ / RabbitMQ== のマネージドサービス / 既存アプリの移行向け

---

## SQS/SNS vs Amazon MQ (SAA 頻出)

| 項目 | ==SQS/SNS== | ==Amazon MQ== |
|------|------------|---------------|
| **タイプ** | AWS 独自 | ==業界標準プロトコル== |
| **プロトコル** | AWS SDK/API | ==AMQP, MQTT, STOMP, OpenWire== |
| **用途** | ==新規開発== | ==既存アプリの移行== |
| **スケーリング** | ==自動 (無制限)== | 手動 |
| **管理** | フルマネージド | 一部管理必要 |

---

## SAA 出題パターン

| シナリオ | 回答 |
|---------|------|
| 「==オンプレの ActiveMQ/RabbitMQ== を AWS に移行」 | ==Amazon MQ== |
| 「==MQTT / AMQP== プロトコルを使いたい」 | ==Amazon MQ== |
| 「既存アプリを==コード変更なし==で移行」 | ==Amazon MQ== |
| 「==新規開発==でメッセージキューが必要」 | ==SQS/SNS== (Amazon MQ ではない) |
