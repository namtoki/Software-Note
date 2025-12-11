# AWS Organizations

複数のAWSアカウントを==一元管理==するサービス。

## 構成
```
Root
├── OU (Organizational Unit)
│   ├── アカウント A
│   └── アカウント B
└── OU
    └── アカウント C
```

## 特徴
- `一括請求 (Consolidated Billing)`:   ==全アカウントの請求を統合== / ボリュームディスカウント
- `OU (Organizational Unit)`:          アカウントをグループ化 / 階層構造
- `SCP (Service Control Policy)`:      ==アカウントの権限を制限== / 許可リスト or 拒否リスト

## SCP (Service Control Policy)
- `目的`:                              OU/アカウントで使用できるサービス・アクションを制限
- `特徴`:
  - ==IAMより優先== (SCPで拒否 → IAMで許可しても実行不可)
  - 管理アカウントには適用==されない==
  - 権限を与えるのではなく==制限する==
- `例`:                                特定リージョン以外の使用禁止、EC2特定タイプのみ許可

## 機能
- `All Features`:                      全機能 (SCP等) / 推奨
- `Consolidated Billing Only`:         請求統合のみ

## SAA試験ポイント
- ==複数アカウント一元管理== → Organizations
- ==アカウントの権限制限== → SCP
- ==一括請求 / ボリュームディスカウント== → Consolidated Billing
- ==SCPはIAMより優先== → SCPで拒否されたら実行不可
