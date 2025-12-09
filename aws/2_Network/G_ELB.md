# Elastic Load Balancing (ELB)

トラフィックを複数のターゲットに==自動分散==するロードバランサー。

## タイプ比較 (SAA頻出)

| 項目 | ALB | NLB | GLB |
|-----|-----|-----|-----|
| レイヤー | ==Layer 7== (HTTP/HTTPS) | ==Layer 4== (TCP/UDP) | Layer 3 (IP) |
| 用途 | Webアプリ、マイクロサービス | 超低レイテンシ、静的IP | サードパーティアプライアンス |
| パスルーティング | ==あり== | なし | なし |
| 静的IP | なし (DNS) | ==あり== | なし |
| WebSocket | あり | あり | - |

## Application Load Balancer (ALB)
- `Layer 7`:                           HTTP/HTTPS
- `ルーティング`:
  - パスベース:                        `/api/*` → API サーバー
  - ホストベース:                      `api.example.com` → API サーバー
  - HTTPヘッダー/メソッド:             条件に応じて振り分け
- `ターゲット`:                        EC2, ECS, Lambda, IP
- `認証`:                              ==Cognito / OIDC 統合==
- `スティッキーセッション`:            Cookie ベース

## Network Load Balancer (NLB)
- `Layer 4`:                           TCP/UDP/TLS
- `パフォーマンス`:                    ==超低レイテンシ== / 数百万リクエスト/秒
- `静的IP`:                            ==AZごとに固定IP== / Elastic IP 割り当て可
- `ターゲット`:                        EC2, IP, ALB
- `ユースケース`:                      ゲーム、IoT、金融取引

## Gateway Load Balancer (GLB)
- `Layer 3`:                           IP パケット
- `用途`:                              ==サードパーティアプライアンス== (ファイアウォール、IDS/IPS)
- `GENEVE`:                            6081番ポート

## 共通機能
- `ヘルスチェック`:                    ターゲットの正常性を監視
- `クロスゾーン負荷分散`:              AZ間で均等に分散 (ALB: デフォルトON, NLB: デフォルトOFF)
- `SSL/TLS終端`:                       ALB/NLB で SSL オフロード
- `Connection Draining`:               登録解除時に既存接続を完了させる

## SAA試験ポイント
- ==HTTP/パスルーティング== → ALB
- ==静的IP / 超低レイテンシ== → NLB
- ==ファイアウォールアプライアンス== → GLB
- ==Cognito認証== → ALB
- ==Lambda ターゲット== → ALB のみ
