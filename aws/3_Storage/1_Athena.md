# Amazon Athena

```
S3 (データ)
      ↓
Glue Data Catalog (スキーマ定義)
      ↓
Athena (SQL クエリ)
      ↓
結果 (S3 に保存)
```

## Overview
- サーバーレスクエリ:                S3 のデータに ==SQL で直接クエリ==
- インフラ管理:                      ==不要== (サーバーレス)
- 課金:                              ==スキャンしたデータ量== ($5/TB)

## Architecture
| コンポーネント | 説明 |
|--------------|------|
| S3 | データソース (CSV, JSON, Parquet, ORC等) |
| ==Glue Data Catalog== | テーブル定義・スキーマ管理 |
| Athena | SQL 実行エンジン (Presto ベース) |

## Supported Formats
| 形式 | 特徴 |
|-----|------|
| CSV, JSON, TSV | 行指向 (読みやすい) |
| ==Parquet==, ==ORC== | ==列指向== (クエリ高速・コスト削減) |
| Avro | スキーマ進化に対応 |

## Cost Optimization
| 方法 | 効果 |
|-----|------|
| ==列指向フォーマット== (Parquet/ORC) | スキャン量削減 (最大90%) |
| ==圧縮== (gzip, snappy) | スキャン量削減 |
| ==パーティション== | 必要なデータのみスキャン |

### パーティション例
```
s3://bucket/logs/year=2024/month=12/day=08/
                 ↓
WHERE year=2024 AND month=12 でスキャン量削減
```

## Athena vs Redshift vs EMR
| サービス | ユースケース |
|---------|-------------|
| ==Athena== | アドホッククエリ、簡単な分析、サーバーレス |
| ==Redshift== | 大規模DWH、複雑な分析、常時稼働 |
| ==EMR== | 大規模データ処理、カスタムジョブ |

## Federated Query
- 概要:                              S3以外のデータソースにもクエリ可能
- 対応:                              RDS, DynamoDB, Redshift, オンプレミス等
- 仕組み:                            Lambda コネクタ経由

## SAA試験ポイント
| シナリオ | 解答 |
|---------|------|
| S3のログをSQLで分析 | ==Athena== |
| サーバーレスでS3を分析 | ==Athena== |
| クエリコストを削減したい | ==Parquet/ORC== + ==パーティション== |
| スキーマを自動検出 | ==Glue Crawler== → Athena |
| アドホック分析 (都度クエリ) | ==Athena== |
| 大規模DWH、複雑な分析 | ==Redshift== |
| CloudTrailログを分析 | ==Athena== (直接クエリ可) |
