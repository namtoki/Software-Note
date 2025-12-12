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
- CDN:
  - `Distribution`:                 配信設定単位
    - `Origin`:                     ==!S3 -> Edge 無料, 他 -> Edge Region 間転送料金== / S3, ALB, EC2, カスタムHTTP
    - `Edge Location`:              ==!Edge -> User $0.114/GB== / ==450箇所以上==
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
    - `Invalidation`:               キャッシュ強制削除 / ==!最初1,000パス/月無料、以降$0.005/パス==
  - セキュリティ:
    - `HTTPS`:                      ACM 証明書 (==us-east-1 で作成必須==)
    - `署名付き URL`:               個別ファイルへのアクセス制御
    - `署名付き Cookie`:            複数ファイル / ストリーミング
    - `Geo Restriction`:            国別でホワイトリスト / ブラックリスト
    - `OAC(Origin Access Control)`: ==S3 を CloudFront 経由のみに制限 (旧 OAI)==
    - `AWS WAF 統合`:               SQLi, XSS, DDoS 対策、レート制限
  - エッジコンピューティング:
    - `Lambda@Edge`:                ==us-east-1== で作成 / Node.js, Python / 複雑な処理 (認証等)
    - `CloudFront Functions`:       JavaScript のみ / ==数百万/秒== / ==1/6 コスト== / 軽量処理
  - 高速化:
    - `自動圧縮`:                   Gzip, Brotli (1KB〜10MB)
    - `HTTP/2`:                     デフォルト有効
    - `Origin Shield`:              オリジンへのリクエスト最小化
