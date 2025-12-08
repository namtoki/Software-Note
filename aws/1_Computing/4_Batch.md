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
- バッチ処理サービス:                 ==フルマネージド== / ジョブの Scheduling・実行 / ジョブ数に応じて ==自動スケール==
  - 実行環境:                         ==EC2== または ==Fargate== / 実行時間無制限
  - 構成要素:
    - `Job Definition`:                 ジョブの実行方法を定義 / ==Dockerイメージ==, vCPU, メモリ, コマンド, 環境変数
      - types:
        - ==Container== (EC2/Fargate)
        - ==Multi-node== (並列処理)
    - `Job Queue`:                      複数キューに ==優先順位== 設定可 / 1つ以上のCompute Environmentに紐付け
    - `Compute Environment`:
      - ==Managed==:                      AWSが自動管理（推奨）
      - ==Unmanaged==:                    ユーザーが EC2 を管理
      - `インスタンスタイプ`:           EC2 On-Demand (安定性重視) / ==Spot (最大90%コスト削減)== / Fargate
