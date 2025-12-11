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
- サーバーレスクエリ:             S3 のデータに ==SQL で直接クエリ== / インフラ管理不要 (サーバーレス) / ==!$5/TB (スキャンしたデータ量)==
  - 構成要素:
    - データソース:               S3 (CSV, JSON, Parquet, TSV, ORC, Avro,,,)
    - `Glue Data Catalog`:          ==テーブル定義・スキーマ管理==
    - `Athena`:                     SQL 実行エンジン (Presto ベース)

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
