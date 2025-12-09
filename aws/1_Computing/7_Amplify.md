# AWS Amplify

```
┌────────────────────────────────────────────────────────┐
│                    AWS Amplify                         │
│  ┌─────────────────────────────────────────────────┐   │
│  │              Amplify Hosting                    │   │
│  │         静的サイト / SSR アプリ                 │   │
│  └─────────────────────────────────────────────────┘   │
│  ┌─────────────────────────────────────────────────┐   │
│  │              Amplify Backend                    │   │
│  │   認証 (Cognito) / API (AppSync/API Gateway)    │   │
│  │   データ (DynamoDB) / ストレージ (S3)           │   │
│  └─────────────────────────────────────────────────┘   │
└────────────────────────────────────────────────────────┘
```

## Associate Level
- フルスタック開発プラットフォーム:   Web/モバイルアプリを ==素早く構築・デプロイ== / ==フロントエンド開発者== 向け
  - フレームワーク対応:               React, Next.js, Vue, Angular, Flutter 等
  - Components:
    - `Amplify Hosting`:                静的サイト (==S3 + CloudFront 相当==) / SSR (Server-Side Rendering) アプリのホスティング
    - `Amplify Backend`:                認証、API、DB、ストレージを自動構築
      | 機能 | 使用サービス |
      |-----|-------------|
      | 認証 | ==Cognito== |
      | API (GraphQL) | ==AppSync== |
      | API (REST) | ==API Gateway + Lambda== |
      | データベース | ==DynamoDB== |
      | ストレージ | ==S3== |
      | 関数 | ==Lambda== |
    - `Amplify Studio`:                 ビジュアルでバックエンド/UI を構築
    - `Amplify Libraries`:              フロントエンド用 SDK
