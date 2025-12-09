# AWS Billing and Cost Management

```
┌─────────────────────────────────────────────────────────┐
│            Billing and Cost Management                  │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐        │
│  │   Budgets   │ │Cost Explorer│ │     CUR     │        │
│  │  予算管理   │ │分析・可視化 │ │ 詳細レポート│        │
│  └─────────────┘ └─────────────┘ └─────────────┘        │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐        │
│  │ Cost Anomaly│ │Cost Allocati│ │  Billing    │        │
│  │  Detection  │ │    Tags     │ │   Alerts    │        │
│  └─────────────┘ └─────────────┘ └─────────────┘        │
└─────────────────────────────────────────────────────────┘
```

## Overview
- 請求・コスト管理の統合コンソール
  - `請求書確認`:               月次
  - [Budgets](/aws/4_Govenance/1_Budgets.md)
  - [Cost Explorer](/aws/4_Govenance/2_CostExplorer.md)
  - [Cost And Usage Reports](/aws/4_Govenance/3_CostAndUsageReports.md)
  - `Cost Anomaly Detection`:   ML で異常検知 / ==無料==
  - `Cost Allocation Tags`:     タグ別にコストを追跡
  - `Free Tier`:                無料利用枠の使用状況
    - types:
      - `12ヶ月無料`:           アカウント作成から12ヶ月
        - EC2:                t2.micro/t3.micro 750時間/月
        - S3:                 5GB
        - RDS:                db.t2.micro/db.t3.micro 750時間/月
        - ELB:                750時間/月
        - CloudFront:         50GB転送/月
        - EBS:                30GB
      - `常に無料`:             永久
        - Lambda:             ==100万リクエスト/月== + ==40万GB秒==
        - DynamoDB:           ==25GB== + ==25 WCU/RCU==
        - SQS:                ==100万リクエスト/月==
        - SNS:                ==100万リクエスト/月==
        - CloudWatch:         基本モニタリング + ==10アラーム==
        - Budgets:            ==2つの予算==
        - Cost Explorer:      基本機能
      - `トライアル`:           サービスごとに異なる短期間
        - Inspector:          15日間
        - Lightsail:          3ヶ月
        - QuickSight:         30日間

## IAM と請求情報
| 設定 | 説明 |
|-----|------|
| ==IAMアクセス有効化== | ルートユーザー以外が請求情報にアクセス |
| 必須設定 | アカウント設定で「IAM User and Role Access to Billing」を有効化 |


## Organizations との統合
| 機能 | 説明 |
|-----|------|
| ==一括請求== | 管理アカウントで全アカウントの請求を集約 |
| ==ボリューム割引== | 組織全体の使用量でティア割引適用 |
| ==RI/SP共有== | 組織内でRI/Savings Plansを共有 |


## コスト最適化オプション
- `Savings Plans`:                  ==1年 or 3年== のコミットメントで ==最大72%割引==
  - types:
    - `Compute Savings Plans`:      ==最も柔軟== / EC2, Fargate, Lambda に適用 / リージョン・インスタンスファミリー変更可
    - `EC2 Instance Savings Plans`: 特定リージョン・インスタンスファミリーに固定 / ==より高い割引率==
    - `SageMaker Savings Plans`:    SageMaker インスタンスに適用
  - 支払いオプション:
    - `全額前払い`:                 ==最大割引==
    - `一部前払い`:                 中間
    - `前払いなし`:                 最小割引
- `Reserved Instances (RI)`:        ==1年 or 3年== の予約で割引
  - 対象サービス:                 EC2, RDS, ElastiCache, Redshift, OpenSearch
  - types:
    - `Standard RI`:                ==最大72%割引== / 変更制限あり
    - `Convertible RI`:             ==最大66%割引== / インスタンスタイプ変更可
