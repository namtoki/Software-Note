# AWS Config

```
AWS リソース
    |
    v
AWS Config が構成を記録
    |
    +---> 構成履歴（いつ、何が変わったか）
    +---> 構成スナップショット（ある時点の全体像）
    +---> Config Rules（ルール違反を検知）
```

```
CloudTrail との違い
例: セキュリティグループの変更

CloudTrail: 「ユーザーAが AuthorizeSecurityGroupIngress を実行した」
AWS Config: 「ポート22が 0.0.0.0/0 から許可された状態になった」
```

## Functions
- `構成スナップショット`:   ==$0.003 / 構成項目== / 定期的に全リソースの状態を保存 (S3 バケット)
- `Config Rules`:           リソースがルールに準拠しているかを評価
  - 種類:
    - `AWS Managed Rule`:   AWS が提供する事前定義ルール（150以上）
    - `Custom Rule`:        ==Lambda== で独自ロジックを実装
  - 評価トリガー:         ==$0.001 / 評価== / 適合パックの評価は ==$0.001 / 評価==
    - `構成変更時`:         リソースが変更されたときに評価
    - `定期的`:             1時間、3時間、6時間、12時間、24時間ごと
  - ```txt
    Config Rule の例:
    「セキュリティグループで 0.0.0.0/0 からの SSH を許可していないこと」
    
    評価結果:
      sg-aaa: COMPLIANT（準拠）
      sg-bbb: NON_COMPLIANT（違反）← アラート
    ```
- `Remediation`:            ルール違反を自動的に修復
  - 種類:
    - `手動修復`:           違反を通知、手動で対応
    - `自動修復`:           `SSM Automation` で自動対応
- `Conformance Packs`:      複数 Rules パッケージ化 / コンプラ要件（PCI DSS、HIPAA など）に対応
- `Aggregator`:             複数アカウント・リージョンの Config データを集約

## Organizations 連携
- 組織全体で Config を有効化
- 組織の適合パック: 全アカウントに一括適用
- 組織のアグリゲータ: 全アカウントのデータを集約
