# AWS Cost and Usage Reports (CUR)

```
AWS Cost and Usage Reports
      ↓ 自動出力
S3 バケット (CSV / Parquet)
      ↓ 分析
Athena / QuickSight / Redshift
```

## Overview
- 最も詳細なコストデータ:         ==リソースレベル== の使用量・コスト / ==無料== (S3保存料金のみ) 
  - 対象:
    - リソースID:                 個別リソースのコスト追跡
    - タグ:                       ==コスト配分タグ==でフィルタ可能
    - 粒度:                       時間単位 / 日単位 / 月単位
  - 出力:
    - 出力先:                     ==S3 バケット==
    - 形式:                       ==CSV== または ==Parquet==
    - 更新頻度:                   1日1〜3回

## Options
- Athena, QuickSight, Redshift と連携
```
CUR → S3 → Athena → QuickSight
              ↓
      SQLで自由にクエリ
      「特定タグのEC2コストを集計」
```
