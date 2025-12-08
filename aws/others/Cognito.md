# Amazon Cognito

Web/モバイルアプリの==認証・認可==サービス。

## User Pools (認証)
- `User Pools`:                        ==ユーザー認証== / サインアップ・サインイン機能
  - 機能:
    - ユーザー名/パスワード認証
    - MFA (多要素認証)
    - ソーシャルログイン (Google, Facebook, Amazon, Apple)
    - SAML / OIDC フェデレーション
  - 発行:                              ==JWT トークン== (ID, Access, Refresh)
  - 連携:                              ==API Gateway==, ==ALB== の認証に使用

## Identity Pools (認可)
- `Identity Pools`:                    ==AWS認証情報の発行== / AWSリソースへのアクセス
  - 機能:
    - User Pools / ソーシャルIdP / SAML から認証後
    - ==一時的なAWS認証情報 (STS)== を発行
    - S3, DynamoDB 等に直接アクセス可能
  - ゲストアクセス:                    ==未認証ユーザー==にも制限付き認証情報を発行可能

## User Pools vs Identity Pools
| 機能 | User Pools | Identity Pools |
|------|-----------|----------------|
| 目的 | ==認証== (誰か確認) | ==認可== (AWS権限付与) |
| 発行 | JWT トークン | ==AWS一時認証情報== |
| 用途 | API Gateway/ALB認証 | S3/DynamoDB直接アクセス |

## SAA試験ポイント
- ==ユーザー認証==が必要 → User Pools
- ==AWSリソースへ直接アクセス==が必要 → Identity Pools
- ==API Gateway認証== → User Pools + API Gateway Authorizer
- ==ALB認証== → User Pools + ALB統合
- ==ソーシャルログイン== → User Pools (Google, Facebook等)
