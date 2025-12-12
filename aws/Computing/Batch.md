# AWS Batch

```
Job Definition (ジョブ定義)
        ↓
    Job Queue (ジョブキュー)
        ↓
Compute Environment (コンピューティング環境)
        ↓
    EC2 / Fargate (実行)
```

## Overview
- バッチ処理サービス:     フルマネージド / ジョブの Scheduling・実行 / ==ジョブ数に応じて自動スケール== / 実行時間無制限
  - `Job Definition`:       ジョブ定義 / ==Dockerイメージ== / インスタンス / 環境変数 / ==Multi-node== (並列処理)
  - `Job Queue`:            複数キューに==優先順位==設定可 / 1つ以上の Compute Environment に紐付け
  - `Compute Environment`:
    - `Managed`:            AWSが自動管理（推奨）
    - `Unmanaged`:          ユーザーが EC2 を管理
    - `インスタンスタイプ`: EC2 On-Demand (安定性重視) / Spot / Fargate
