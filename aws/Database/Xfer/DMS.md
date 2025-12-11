# AWS DMS (Database Migration Service)

## Associate Level
- DB 移行サービス:                        オンプレ/クラウドから AWS への DB 移行 / ==ソース稼働中でも移行可能==

---

## 移行タイプ

| タイプ | 説明 |
|--------|------|
| ==同種移行== | MySQL → MySQL, Oracle → Oracle |
| ==異種移行== | Oracle → Aurora, SQL Server → PostgreSQL |

---

## SCT (Schema Conversion Tool)

| 移行 | SCT |
|------|-----|
| **同種移行** | ==不要== |
| **異種移行** | ==必要== (スキーマ変換) |

```
【同種移行】
Oracle → DMS → Oracle (RDS)

【異種移行】
Oracle → SCT (スキーマ変換) → DMS (データ移行) → PostgreSQL (RDS)
```

---

## 継続的レプリケーション (CDC)

| 機能 | 説明 |
|------|------|
| **Full Load** | 既存データを一括移行 |
| **CDC** | ==変更データを継続的に同期== |
| **Full Load + CDC** | 一括移行後、継続同期 |

→ ==ダウンタイム最小化==で移行可能

---

## 主なソース/ターゲット

| ソース | ターゲット |
|--------|-----------|
| オンプレ DB (Oracle, MySQL, SQL Server 等) | RDS, Aurora |
| EC2 上の DB | DynamoDB, Redshift |
| RDS | S3 |
| S3 | - |

---

## SAA 出題パターン

| シナリオ | 回答 |
|---------|------|
| 「オンプレ DB を AWS に移行」 | ==DMS== |
| 「==異種== DB 間の移行 (Oracle → Aurora)」 | ==SCT + DMS== |
| 「==ダウンタイム最小==で移行」 | ==DMS (CDC)== |
| 「DB を S3 に継続的にエクスポート」 | ==DMS== |
| 「同種 DB 移行 (MySQL → RDS MySQL)」 | ==DMS のみ== (SCT 不要) |
