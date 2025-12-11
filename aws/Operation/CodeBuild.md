# AWS CodeBuild

```
Source (GitHub/S3/CodeCommit)
        ↓
┌─────────────────────┐
│    CodeBuild        │
│  ┌───────────────┐  │
│  │ Build 環境    │  │
│  │ (コンテナ)    │  │
│  └───────────────┘  │
└─────────────────────┘
        ↓
Artifact (S3)
```

## Overview
- フルマネージド CI:              ==ビルド・テスト== を実行するサーバーレスサービス
  - 特徴:
    - サーバー管理不要:           ビルドサーバーのプロビジョニング・スケーリング不要
    - 従量課金:                   ==ビルド時間== に応じた課金
    - `buildspec.yml`:            ビルド手順を定義するファイル
  - 入力:                         GitHub, CodeCommit, S3, Bitbucket
  - 出力:                         S3 (Artifact)

## CI/CD パイプライン
```
CodeCommit → CodeBuild → CodeDeploy
   (Source)    (Build)    (Deploy)
        ↓         ↓          ↓
   ┌──────────────────────────────┐
   │        CodePipeline          │
   │      (オーケストレーション)    │
   └──────────────────────────────┘
```

| サービス | 役割 |
|---------|------|
| CodeCommit | ソースコード管理 (Git) |
| **CodeBuild** | ==ビルド・テスト== (CI) |
| CodeDeploy | デプロイ (CD) |
| CodePipeline | 全体のオーケストレーション |

## SAA試験ポイント
| シナリオ | 解答 |
|---------|------|
| ビルド・テストの自動化 | ==CodeBuild== |
| CI/CD パイプライン構築 | ==CodePipeline + CodeBuild + CodeDeploy== |
| サーバーレスなビルド環境 | ==CodeBuild== |
