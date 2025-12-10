# Amazon OpenSearch Service

## Associate Level
- 検索・分析エンジン:                     ==全文検索== / ==ログ分析== / 旧 Amazon Elasticsearch Service

---

## ユースケース

| ユースケース | 説明 |
|-------------|------|
| ==ログ分析== | CloudWatch Logs, VPC Flow Logs 等を分析 |
| ==全文検索== | アプリの検索機能 |
| ==リアルタイム分析== | ダッシュボード (Kibana/OpenSearch Dashboards) |

---

## よくある構成 (SAA 頻出)

```
CloudWatch Logs → Kinesis Data Firehose → OpenSearch → Dashboards
                        or
    S3 → Lambda → OpenSearch
```

---

## Kendra vs OpenSearch

| 項目 | ==Kendra== | ==OpenSearch== |
|------|-----------|----------------|
| **検索タイプ** | ==ML ベースの自然言語== | ==キーワード/全文検索== |
| **用途** | 企業内ドキュメント検索 | ログ分析、アプリ検索 |
| **クエリ例** | 「売上レポートはどこ？」 | キーワードマッチ |

---

## SAA 出題パターン

| シナリオ | 回答 |
|---------|------|
| 「==ログ分析==・可視化したい」 | ==OpenSearch== |
| 「アプリに==全文検索==機能を追加」 | ==OpenSearch== |
| 「CloudWatch Logs を==分析・ダッシュボード==化」 | ==OpenSearch== |
| 「==自然言語==で企業ドキュメント検索」 | ==Kendra== (OpenSearch ではない) |
