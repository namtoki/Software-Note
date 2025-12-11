# Amazon Cognito

## Overview
- 認証・認可サービス:     Web / モバイルアプリのユーザー認証とAWSリソースへのアクセス制御
  - `User Pools`:           認証 (==ユーザーの身元確認==)
    - 機能:               サインアップ・サインイン / MFA / ソーシャルログイン / SAML・OIDC フェデレーション
    - 発行:               ==JWT トークン== (ID, Access, Refresh)
    - 連携:               ==API Gateway, ALB の認証に使用==
  - `Identity Pools`:       認可 (==AWS 権限付与==)
    - 機能:               User Pools / ソーシャル IdP / SAML から認証後、==一時的な AWS 認証情報 (STS)== を発行
    - アクセス:           S3, DynamoDB 等に直接アクセス可能
    - ゲストアクセス:     ==未認証ユーザー==にも制限付き認証情報を発行可能
