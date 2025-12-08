# Amazon CloudFront

```
                          +------------------+
                          |     Origin       |
                          | (S3, ALB, EC2等) |
                          +------------------+
                                   |
                    +--------------+--------------+
                    |              |              |
              +-----v----+  +-----v----+  +-----v----+
              | Edge     |  | Edge     |  | Edge     |
              | Location |  | Location |  | Location |
              | (Tokyo)  |  | (Seoul)  |  | (Oregon) |
              +----------+  +----------+  +----------+
                    |              |              |
                 User A        User B        User C
```

## Overview
- Cache:
  - `Distribution`:                 配信設定単位
    - Components:
      - `Origin`:                   ==S3 -> Edge 無料, 他 -> Edge Region 間転送料金== / S3, ALB, EC2, カスタムHTTP
      - `Edge Location`:            ==Edge -> User $0.114/GB== / ==450箇所以上==
    - `Behavior`:                   パスパターンごとのキャッシュ・転送設定
      - Path Pattern:             /api/*, /images/*.jpg など
        - ```txt
          リクエスト: https://cdn.example.com/api/users
                                                |
                                    パスパターンマッチング
                                                |
                        /api/* にマッチ → Behavior 1 の設定を適用
          ```
      - Origin:                   どのオリジンに転送するか
      - Viewer Protocol Policy:   HTTP許可 / HTTPSリダイレクト / HTTPSのみ / ==HTTP $0.0075/10,000, HTTPS $0.0100/10,000==
      - Allowed HTTP Methods:     GET,HEAD / +OPTIONS / +POST,PUT,DELETE等
      - Cache Policy:             キャッシュキーとTTL設定
        - `Cache Key`:              URL (パス + クエリ文字列), ヘッダー, Cookie
        - `TTL (Time To Live)`:     キャッシュ保持時間 / デフォルト24時間 / 最大 1 年
      - Origin Request Policy:    オリジンに転送するヘッダー・Cookie
      - Response Headers Policy:  レスポンスに追加するヘッダー (CORS等)
      - Lambda@Edge / Functions:  エッジで実行する関数
    - `Regional Edge Cache`:        Edge と Origin の中間キャッシュ / キャッシュヒット率向上

- `追加機能`:                       Lambda@Edge, CloudFront Functions 等は別料金
### キャッシュ無効化 (Invalidation)
- 料金: 最初1,000パス/月無料、以降 ==$0.005/パス==
- 反映時間: 数分

---

## セキュリティ

### HTTPS

| 設定 | 説明 |
|------|------|
| Viewer Protocol Policy | HTTP/HTTPS, Redirect HTTP to HTTPS, HTTPS Only |
| SSL証明書 | ACM (==us-east-1で作成必須==), カスタム証明書 |

### 署名付きURL / 署名付きCookie

| 方式 | 用途 |
|------|------|
| 署名付きURL | 個別ファイルへのアクセス制御 |
| 署名付きCookie | 複数ファイル/ストリーミング |

### 地理的制限 (Geo Restriction)

| 設定 | 説明 |
|------|------|
| ホワイトリスト | 指定した国のみ許可 |
| ブラックリスト | 指定した国をブロック |

### AWS WAF 統合

- SQLインジェクション、XSS、DDoS対策
- レート制限

---

## エッジコンピューティング

### Lambda@Edge

```
Client --> [Viewer Req] --> CloudFront --> [Origin Req] --> Origin
       <-- [Viewer Res] <--            <-- [Origin Res] <--
```

| トリガー | タイミング | 用途 |
|---------|----------|------|
| Viewer Request | クライアント→CloudFront | 認証、URLリライト |
| Origin Request | CloudFront→オリジン | オリジン選択 |
| Origin Response | オリジン→CloudFront | ヘッダー追加 |
| Viewer Response | CloudFront→クライアント | セキュリティヘッダー |

| 制限 | Viewer | Origin |
|------|--------|--------|
| メモリ | 128 MB | 10 GB |
| タイムアウト | 5秒 | 30秒 |
| 作成リージョン | ==us-east-1== | ==us-east-1== |

### CloudFront Functions

| 項目 | Lambda@Edge | CloudFront Functions |
|------|-------------|---------------------|
| 言語 | Node.js, Python | JavaScript のみ |
| 実行場所 | リージョナルエッジ | エッジロケーション |
| スケール | 数千/秒 | ==数百万/秒== |
| 料金 | 高い | ==1/6 のコスト== |
| 用途 | 複雑な処理 | 軽量な処理 |

---

## 高速化機能

| 機能 | 説明 |
|------|------|
| 自動圧縮 | Gzip, Brotli (1KB〜10MB) |
| HTTP/2 | デフォルト有効 |
| HTTP/3 (QUIC) | オプトイン |
| Origin Shield | オリジンへのリクエスト最小化 |

---

## CloudFront vs Global Accelerator

| 項目 | CloudFront | Global Accelerator |
|------|-----------|-------------------|
| 用途 | コンテンツ配信 (CDN) | TCP/UDPアプリの高速化 |
| キャッシュ | あり | なし |
| プロトコル | HTTP/HTTPS | TCP/UDP |
| ユースケース | 静的/動的Web | ゲーム、IoT、VoIP |
| IPアドレス | 動的 | ==静的 (Anycast)== |

---

## SAA試験 頻出ポイント

### 選択シナリオ

| シナリオ | 解答 |
|---------|------|
| S3を直接公開せずCloudFront経由のみ | OAC (Origin Access Control) |
| プライベートコンテンツ配信 | 署名付きURL / 署名付きCookie |
| 特定国からのアクセスブロック | Geo Restriction |
| DDoS対策 | CloudFront + WAF + Shield |
| SSL証明書の設定 | ACM (==us-east-1==で作成) |
| キャッシュの即座の無効化 | Invalidation |
| オリジン障害時のフェイルオーバー | オリジングループ |
| 軽量なエッジ処理 | CloudFront Functions |
| 複雑なエッジ処理 (認証等) | Lambda@Edge |

### 重要ポイント

- ACM証明書: ==us-east-1== で作成必須
- Lambda@Edge: ==us-east-1== で作成
- OAC vs OAI: OAC推奨 (新方式)
- デフォルトTTL: 24時間
