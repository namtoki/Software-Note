# AWS Directory Service

AWS上で==Active Directory==を利用するためのマネージドサービス。

## タイプ比較 (SAA頻出)

| タイプ | 説明 | ユースケース |
|-------|------|-------------|
| `AWS Managed Microsoft AD` | ==フル機能AD== / 信頼関係構築可 | 本格的なAD環境、オンプレADとの信頼関係 |
| `AD Connector` | ==オンプレADへのプロキシ== / ユーザー情報==保存しない== | 既存オンプレADを活用、AWS上にユーザー不要 |
| `Simple AD` | ==軽量AD互換== (Samba) / 小規模向け | 基本的なAD機能のみ必要、低コスト |

## AWS Managed Microsoft AD
- フル機能の Microsoft AD
- ==オンプレADと信頼関係==構築可能
- マルチAZ配置 (高可用性)
- グループポリシー、LDAP、Kerberos対応

## AD Connector
- オンプレADへの==プロキシ (リダイレクト)==
- ==AWS上にユーザー情報を保存しない==
- VPN / Direct Connect でオンプレ接続必須
- MFA対応 (RADIUS)

## Simple AD
- Samba 4 ベースの軽量AD
- ==信頼関係構築不可==
- 小規模 (最大500ユーザー) / 大規模 (最大5000ユーザー)

## SAA試験ポイント
- ==フルAD機能 + 信頼関係== → AWS Managed Microsoft AD
- ==オンプレAD活用 + AWS保存不要== → AD Connector
- ==基本機能 + 低コスト== → Simple AD
- ==WorkSpaces/RDS認証== → いずれも連携可能
