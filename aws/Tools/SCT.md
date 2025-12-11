# AWS Schema Conversion Tool (SCT)

異種データベース間の==スキーマ変換==を行うツール。

## 特徴
- `スキーマ変換`:                      ソースDBのスキーマをターゲットDBに変換
- `コード変換`:                        ストアドプロシージャ、ビュー、関数等も変換
- `評価レポート`:                      変換の複雑さ、手動対応が必要な箇所を表示

## 対応する変換例
| ソース | ターゲット |
|-------|-----------|
| Oracle | Aurora PostgreSQL, RDS PostgreSQL |
| SQL Server | Aurora MySQL, RDS MySQL |
| Oracle | Aurora MySQL, RDS MySQL |

## DMS との関係
```
[ソースDB] → [SCT] → [スキーマ変換] → [ターゲットDB]
                            ↓
            [DMS] → [データ移行]
```
- `SCT`:                               ==スキーマ (構造)== を変換
- `DMS`:                               ==データ== を移行

## SAA試験ポイント
- ==異種DB間のスキーマ変換== → SCT
- ==データ移行== → DMS (SCTではない)
- ==同種DB間== → SCT不要 (DMSのみでOK)
