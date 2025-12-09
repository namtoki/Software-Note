# Amazon SageMaker

```
+-------------+     +-------------+     +-------------+     +-------------+
|   データ    | --> |   構築      | --> | トレーニング| --> |   デプロイ  |
|   準備      |     | (Notebook)  |     |  (Training) |     | (Endpoint)  |
+-------------+     +-------------+     +-------------+     +-------------+
```

## Associate Level
- 機械学習開発基盤:               ==機械学習モデル==の構築・トレーニング・デプロイを行うフルマネージドサービス

## Specialty Level
- 主要コンポーネント:
  - `SageMaker Studio`:             ==統合開発環境 (IDE)== / Notebook, 実験管理, デプロイ
  - `Notebook Instance`:            Jupyter Notebook 環境 / モデル開発・実験
  - `Training Job`:                 モデルのトレーニング / ==マネージドインフラ==
  - `Endpoint`:                     ==リアルタイム推論== / オートスケーリング対応
  - `Batch Transform`:              ==バッチ推論== / 大量データの一括処理
- データ準備:
  - `Ground Truth`:                 ==データラベリング== / 人間 + 機械学習でアノテーション
  - `Data Wrangler`:                データ前処理・変換
- デプロイオプション:
  - `Real-time Endpoint`:           リアルタイム推論 (低レイテンシー)
  - `Batch Transform`:              バッチ推論 (大量データ)
  - `Serverless Inference`:         間欠的なトラフィック (コスト最適化)
