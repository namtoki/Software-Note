# AWS CodePipeline

```
┌─────────────────────────────────────────────────────────────┐
│                      CodePipeline                           │
│  ┌──────────┐   ┌──────────┐   ┌──────────┐   ┌──────────┐  │
│  │  Source  │ → │  Build   │ → │  Test    │ → │  Deploy  │  │
│  │CodeCommit│   │CodeBuild │   │CodeBuild │   │CodeDeploy│  │
│  └──────────┘   └──────────┘   └──────────┘   └──────────┘  │
└─────────────────────────────────────────────────────────────┘
```

## Overview
- フルマネージド CD:              リリースプロセス全体を ==自動化・オーケストレーション==
  - 特徴:
    - ステージ構成:               Source → Build → Test → Deploy
    - 自動トリガー:               コード変更で ==自動的にパイプライン実行==
    - 柔軟な統合:                 AWS サービス + サードパーティ (GitHub, Jenkins 等)

## ステージと連携サービス
| ステージ | AWS サービス | サードパーティ |
|---------|-------------|---------------|
| Source | CodeCommit, S3, ECR | GitHub, Bitbucket |
| Build | CodeBuild | Jenkins |
| Test | CodeBuild | - |
| Deploy | CodeDeploy, ECS, EB, Lambda, S3 | - |

## デプロイ先
| サービス | 用途 |
|---------|------|
| EC2 / オンプレ | CodeDeploy 経由 |
| ECS | コンテナデプロイ |
| Lambda | サーバーレス |
| Elastic Beanstalk | PaaS |
| S3 | 静的サイト |

## SAA試験ポイント
| シナリオ | 解答 |
|---------|------|
| CI/CD パイプライン構築 | ==CodePipeline== |
| コード変更で自動デプロイ | ==CodePipeline== |
| リリースプロセスの自動化 | ==CodePipeline== |
| ビルド・テストのみ | CodeBuild |
