# AWS WAF (Web Application Firewall)

==Webアプリケーション==を一般的な攻撃から保護するファイアウォール。

## 保護対象 (デプロイ先)
- `CloudFront`
- `ALB`
- `API Gateway`
- `AppSync`

## コンポーネント
- `Web ACL`:                           ルールのコンテナ / リソースに関連付け
- `Rule`:                              条件とアクション (Allow / Block / Count)
- `Rule Group`:                        再利用可能なルールのセット

## ルールタイプ
- `マネージドルール`:                  ==AWS/マーケットプレイス提供== / すぐに使える
  - AWS Managed Rules:                 SQLi, XSS, 悪意のあるIP等
  - 有料マネージドルール:              セキュリティベンダー提供
- `カスタムルール`:                    独自の条件を定義

## 保護できる攻撃
- `SQLインジェクション`
- `クロスサイトスクリプティング (XSS)`
- `悪意のあるIPからのアクセス`
- `特定の国からのアクセス (Geo制限)`
- `レートベース制限 (DDoS緩和)`

## WAF vs Shield vs Firewall Manager

| サービス | 用途 |
|---------|------|
| `WAF` | ==Layer 7== (アプリケーション層) 保護 / SQLi, XSS等 |
| `Shield` | ==Layer 3/4== (ネットワーク層) / ==DDoS保護== |
| `Firewall Manager` | ==複数アカウント==のWAF/Shield/SGを一元管理 |

## SAA試験ポイント
- ==SQLi, XSS 対策== → WAF
- ==DDoS 保護== → Shield (WAFではない)
- ==CloudFront/ALB/API Gateway 保護== → WAF
- ==レートベース制限== → WAF (Rule)
