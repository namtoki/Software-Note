# Amazon MSK (Managed Streaming for Apache Kafka)

## Overview
- Kafka マネージド:                       ==Apache Kafka== のフルマネージドサービス / 既存 Kafka アプリの移行向け

---

## Kinesis vs MSK (SAA 頻出)

| 項目 | ==Kinesis Data Streams== | ==Amazon MSK== |
|------|-------------------------|----------------|
| **タイプ** | AWS 独自 | ==Apache Kafka== |
| **用途** | ==新規開発== | ==既存 Kafka アプリの移行== |
| **プロトコル** | AWS SDK/API | ==Kafka API== |
| **スケーリング** | シャード単位 | ブローカー/パーティション |
| **データ保持** | 最大 365 日 | ==無制限== |
| **管理** | フルマネージド | 一部管理必要 |

---

## SAA 出題パターン

| シナリオ | 回答 |
|---------|------|
| 「==オンプレの Kafka== を AWS に移行」 | ==MSK== |
| 「既存 ==Kafka アプリ==をそのまま使いたい」 | ==MSK== |
| 「==新規開発==でリアルタイムストリーミング」 | ==Kinesis== (MSK ではない) |
| 「Kafka API / エコシステムを使いたい」 | ==MSK== |
