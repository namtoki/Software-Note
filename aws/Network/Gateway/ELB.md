# Elastic Load Balancing (ELB)

```
【ALB】 Layer 7 - HTTP/HTTPS ルーティング
Client → ALB → /api/*     → API Server
              → /images/* → Image Server
              → /*        → Web Server

【NLB】 Layer 4 - TCP/UDP 高速転送
Client → NLB (静的IP) → Server1
                      → Server2
                      → Server3

【GWLB】 Layer 3 - セキュリティアプライアンス経由
Client → GWLB → Firewall/IDS (検査) → GWLB → Server
```

## Overview
- ロードバランサー:               トラフィックを複数のターゲットに==自動分散==する
  - `ALB`:                          Layer 7 (HTTP/HTTPS) / 静的 IP なし (DNS) / WebSocket あり / ==Lambda ターゲット== → ALB のみ
    - ルーティング:
      - パスベース:               `/api/*` → API サーバー
      - ホストベース:             `api.example.com` → API サーバー
      - HTTPヘッダー/メソッド:    条件に応じて振り分け
    - `認証代行`:                   Cognito / OIDC 統合
    - `スティッキーセッション`:     ==同じユーザーを常に同じターゲットに振り分ける== / Cookie ベース
      - なぜ必要？:
        | ケース            | 理由                 |
        |----------------|--------------------|
        | セッション情報をローカル保持 | ログイン状態がサーバーのメモリにある |
        | ショッピングカート      | カート情報がサーバーに保存      |
      - 推奨される代替策:
        | 方法              | 説明            |
        |-----------------|---------------|
        | ==ElastiCache== | セッション情報を外部に保存 |
        | ==DynamoDB==    | セッション情報を外部に保存 |
    - ユースケース:               Webアプリ、マイクロサービス
  - `NLB`:                          Layer 4 (TCP/UDP/TLS) / WebSocket あり
    - 静的IP:                     ==AZごとに固定IP== / Elastic IP 割り当て可
    - ユースケース:               ==超低レイテンシ、静的IP== / ゲーム、IoT、金融取引
  - `GWLB (Gateway LB)`:            Layer 3 (IP) / ==全トラフィックを検査アプライアンス経由==
    - `GENEVE`:                     6081番ポート
    - 構成:                       GWLB → セキュリティアプライアンス (検査) → 戻す
    - ユースケース:               ==サードパーティアプライアンス== (ファイアウォール、IDS/IPS)
  - 共通機能:
    - `ヘルスチェック`:             ターゲットの正常性を監視
    - `クロスゾーン負荷分散`:       AZ間で均等に分散 (ALB: デフォルトON, NLB: デフォルトOFF)
    - `SSL/TLS終端`:                ALB/NLB で SSL オフロード
    - `Connection Draining`:        登録解除時に既存接続を完了させる
