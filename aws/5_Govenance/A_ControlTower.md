# AWS Control Tower

```
                    AWS Control Tower
                          |
    +---------------------+---------------------+
    |                     |                     |
Landing Zone        Account Factory        Controls
(マルチアカウント      (アカウント自動       (ガードレール)
 環境の自動構築)        プロビジョニング)
    |
    v
AWS Organizations (OU構造、SCP)
```

## Overview
- アカウント管理簡素化:   AWS Organizations 上に構築
  - ==Landing Zone==:         セットアップされるマルチアカウント環境 / ベストプラクティスに基づいた初期設定が自動適用
    - 自動作成されるもの:
      - `Root OU`:          組織のルート
      - `Security OU`:      Log Archive アカウント、Audit アカウント
      - `Sandbox OU`:       開発・テスト用（オプション）
  - `Controls`:             旧称: Guardrails / OU に適用するガバナンスルール
    | 種類 | 実装 | 説明 |
    |------|------|------|
    | `Preventive` | ==SCP== | 禁止されたアクションをブロック |
    | `Detective` | ==Config Rules== | 非準拠リソースを検出 |
    | `Proactive` | ==CloudFormation Hooks== | デプロイ前にテンプレートを検証 |
    ```
    Preventive（予防的）の例:
    「リージョンの制限」→ 許可されていないリージョンでの操作を SCP でブロック

    Detective（検出的）の例:
    「S3 バケットの公開禁止」→ 公開バケットを Config Rules で検出・通知
    ```
  - ==Account Factory==:      新しい AWS アカウントを自動プロビジョニング / ==Service Catalog== と統合
    - 自動適用内容:       OU に配置 / Controls が適用 / ベースライン設定が構成
