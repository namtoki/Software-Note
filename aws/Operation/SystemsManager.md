# AWS Systems Manager (SSM)

```
+------------------------------------------------------------------+
|                    AWS Systems Manager                            |
|  +------------------------------------------------------------+  |
|  |  Operations Management  |  Application Management          |  |
|  |  - OpsCenter            |  - Parameter Store               |  |
|  |  - Incident Manager     |  - AppConfig                     |  |
|  +------------------------------------------------------------+  |
|  |  Change Management      |  Node Management                 |  |
|  |  - Automation           |  - Session Manager               |  |
|  |  - Change Calendar      |  - Run Command                   |  |
|  |  - Maintenance Windows  |  - Patch Manager                 |  |
|  |                         |  - State Manager                 |  |
|  +------------------------------------------------------------+  |
+------------------------------------------------------------------+
```

## Prerequisites
- `SSM Agent`:                             EC2にインストール必須 / Amazon Linux, Ubuntu等は==プリインストール==
- `IAM Role`:                              ==AmazonSSMManagedInstanceCore== ポリシーをEC2にアタッチ
- `ネットワーク`:                          Systems Manager エンドポイントへの接続が必要
  - Public:                                インターネットゲートウェイ経由
  - Private:                               ==VPC Endpoint== (推奨) または NAT Gateway

## Node Management

### Session Manager
- `Session Manager`:                       ==SSH/RDP不要==でEC2にシェルアクセス / ブラウザ or CLI
  - メリット:
    - ==ポート22/3389を開ける必要なし== (Security Group)
    - ==Bastion Host 不要==
    - ==キーペア管理不要==
    - セッションログをS3/CloudWatch Logsに保存可
    - IAMでアクセス制御
  - ユースケース:                          セキュアなリモートアクセス, 監査要件, Bastion排除

### Run Command
- `Run Command`:                           複数EC2に==リモートでコマンド実行== / エージェント経由
  - 特徴:
    - SSHなしで実行
    - ==複数インスタンスに同時実行==
    - ドキュメント (コマンド定義) を指定
    - レート制御 (同時実行数, エラー閾値)
  - 組み込みドキュメント例:
    - `AWS-RunShellScript`:                Linux シェルコマンド
    - `AWS-RunPowerShellScript`:           Windows PowerShell
    - `AWS-UpdateSSMAgent`:                SSM Agent 更新

### Patch Manager
- `Patch Manager`:                         OS/アプリケーションの==パッチ適用自動化==
  - コンポーネント:
    - `Patch Baseline`:                    適用するパッチのルール定義 (重要度, 分類, 自動承認日数)
      - AWS管理:                           OS別のデフォルトベースライン
      - カスタム:                          独自ルールを定義可
    - `Patch Group`:                       ==タグベース==でインスタンスをグループ化 (`Patch Group` タグ)
    - `Maintenance Window`:                パッチ適用のスケジュール
  - ユースケース:                          コンプライアンス, セキュリティ自動化

### State Manager
- `State Manager`:                         インスタンスを==望ましい状態に維持==
  - 機能:
    - 定期的に設定を適用 (ドリフト修正)
    - ブートストラップ (初期設定)
    - ソフトウェアインストール維持
  - Association:                           ドキュメント + ターゲット + スケジュール

### Inventory
- `Inventory`:                             ==メタデータ収集== / インストール済みソフトウェア, ネットワーク設定等
  - 収集データ:                            アプリケーション, ファイル, ネットワーク設定, Windowsロール等
  - 統合:                                  Athena/QuickSight で分析可

## Application Management

### Parameter Store
- `Parameter Store`:                       ==設定値・シークレットを安全に保存==
  - タイプ:
    - `String`:                            プレーンテキスト
    - `StringList`:                        カンマ区切りリスト
    - `SecureString`:                      ==KMSで暗号化== (APIキー, パスワード等)
  - 階層構造:                              `/app/prod/db/password` のようなパス形式
  - バージョニング:                        履歴管理, ロールバック可能
  - Tier:
    - `Standard`:                          ==無料== / 10,000パラメータ / 4KB
    - `Advanced`:                          有料 / 100,000パラメータ / 8KB / ポリシー対応
  - vs Secrets Manager:
    | 機能 | Parameter Store | Secrets Manager |
    |-----|-----------------|-----------------|
    | 料金 | ==Standard無料== | 有料 |
    | 自動ローテーション | なし | ==あり== |
    | クロスアカウント | なし | あり |
    | RDS統合 | 手動 | ==ネイティブ== |
    | ユースケース | 設定値, 簡易シークレット | DB認証情報, APIキー |

## Change Management

### Automation
- `Automation`:                            ==運用タスクの自動化== / Runbook (ドキュメント) を実行
  - ユースケース:
    - AMI作成の自動化
    - インスタンスの起動/停止
    - 障害復旧の自動化
    - 承認ワークフロー
  - AWS提供 Runbook:
    - `AWS-CreateImage`:                   AMI作成
    - `AWS-StopEC2Instance`:               インスタンス停止
    - `AWS-RestartEC2Instance`:            インスタンス再起動

### Maintenance Windows
- `Maintenance Windows`:                   ==定期メンテナンスのスケジュール==
  - 構成:
    - スケジュール:                        cron/rate 式
    - ターゲット:                          インスタンス/タグ
    - タスク:                              Run Command, Automation, Lambda, Step Functions
  - ユースケース:                          パッチ適用, バックアップ, スクリプト実行

## Operations Management

### OpsCenter
- `OpsCenter`:                             ==運用問題(OpsItem)を一元管理==
  - 機能:
    - 問題の集約・追跡
    - 関連リソースの表示
    - Runbook との連携
  - 統合:                                  CloudWatch Alarms, EventBridge, Config

## Hybrid & Multi-Cloud
- `Hybrid Activation`:                     ==オンプレミス/他クラウドのサーバーをSSMで管理==
  - 手順:
    1. Activation を作成 (コード + ID を取得)
    2. サーバーに SSM Agent をインストール
    3. Activation コードで登録
  - 管理対象:                              `mi-` プレフィックス (Managed Instance)

## SAA試験頻出ポイント
- Session Manager:                         ==Bastion不要==, ==ポート開放不要==, 監査ログ
- Parameter Store vs Secrets Manager:      ==無料 vs 有料==, ==ローテーション有無==
- Patch Manager:                           ==Patch Group タグ==, Maintenance Window
- Run Command:                             複数インスタンスへの同時コマンド実行
- 前提条件:                                ==SSM Agent==, ==IAM Role==, ネットワーク接続
