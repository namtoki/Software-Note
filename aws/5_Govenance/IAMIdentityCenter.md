# AWS IAM Identity Center (旧 AWS SSO)

複数AWSアカウント・アプリケーションへの==シングルサインオン (SSO)==を提供。

## 特徴
- `一元管理`:                          複数アカウントへのアクセスを==単一ポータル==で管理
- `SSO`:                               一度のログインで複数アカウント/アプリにアクセス
- `Organizations統合`:                 AWS Organizations と連携

## ID ソース
- `Identity Center ディレクトリ`:      デフォルト / IAM Identity Center 内でユーザー管理
- `Active Directory`:                  AWS Managed AD / AD Connector 経由
- `外部 IdP`:                          SAML 2.0 (Okta, Azure AD 等)

## 権限セット
- `Permission Set`:                    ==IAMポリシーのテンプレート== / アカウントに割り当て
- `AWS管理ポリシー`:                   事前定義済み (AdministratorAccess等)
- `カスタムポリシー`:                  独自の権限を定義

## SAA試験ポイント
- ==複数アカウントへのSSO== → IAM Identity Center
- ==Organizations + SSO== → IAM Identity Center
- ==外部IdP連携 (SAML)== → IAM Identity Center
- ==単一アカウントのフェデレーション== → IAM (SAML/OIDC)
