# AWS Glue

## Overview
- ETLサービス:                             ==Extract (抽出)・Transform (変換)・Load (ロード)==
- フルマネージド:                          ==サーバーレス== / インフラ管理不要
- 基盤:                                    Apache Spark

## Core Components

### Glue Data Catalog
- メタデータリポジトリ:                    テーブル定義、スキーマ、ロケーション情報を管理
- 共有:                                    ==Athena==, ==Redshift Spectrum==, ==EMR== で共通利用
- Hive互換:                                Hive Metastore として機能

### Glue Crawler
- スキーマ自動検出:                        S3, RDS, DynamoDB等をスキャン
- カタログ更新:                            ==自動でテーブル定義を作成・更新==
- スケジュール実行:                        定期的にスキーマ変更を検知

### Glue Job
- ETLスクリプト実行:                       Python (PySpark) / Scala
- ジョブタイプ:
  - `Spark`:                               大規模バッチ処理
  - `Streaming`:                           リアルタイムETL (Kinesis, Kafka)
  - `Python Shell`:                        軽量スクリプト

## Data Sources
| ソース | 種類 |
|-------|------|
| ストレージ | S3, DynamoDB |
| データベース | RDS, Redshift, Aurora |
| オンプレミス | JDBC接続 |

## Architecture Example
```
S3 (Raw Data)
     ↓
Glue Crawler → Data Catalog (スキーマ定義)
     ↓
Glue Job (ETL変換)
     ↓
S3 (Processed) → Athena / Redshift でクエリ
```

## Glue vs 他サービス
| サービス | ユースケース |
|---------|-------------|
| ==Glue== | サーバーレスETL / メタデータ管理 |
| ==EMR== | 大規模・複雑なビッグデータ処理 / カスタマイズ必要 |
| ==Data Pipeline== | EC2ベースのワークフロー (レガシー) |
| ==Kinesis Data Firehose== | ストリーミングデータのロード (変換は限定的) |

## SAA試験ポイント
- 「S3データをAthenaでクエリしたい」→ ==Glue Crawler== でカタログ作成
- 「サーバーレスETL」→ ==Glue==
- 「スキーマ自動検出」→ ==Glue Crawler==
- 「Athena, Redshift Spectrumで共通メタデータ」→ ==Glue Data Catalog==
- 「大規模で複雑なカスタム処理」→ ==EMR== (Glueでは不十分な場合)
