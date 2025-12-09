# AWS Global Accelerator

==AWSグローバルネットワーク==を使用してアプリケーションの可用性とパフォーマンスを向上。

## 特徴
- `静的Anycast IP`:                    ==2つの固定IP==を提供 / DNS変更不要
- `AWSバックボーン`:                   インターネットではなく==AWSグローバルネットワーク==経由
- `エンドポイント`:                    ALB, NLB, EC2, Elastic IP
- `ヘルスチェック`:                    エンドポイント障害時に==自動フェイルオーバー==

## Global Accelerator vs CloudFront (SAA頻出)

| 項目 | Global Accelerator | CloudFront |
|-----|-------------------|------------|
| 用途 | ==TCP/UDP== (動的コンテンツ) | ==HTTP/HTTPS== (静的/動的) |
| IP | ==静的IP== (Anycast) | 動的 (DNS) |
| キャッシュ | ==なし== | ==エッジキャッシュ== |
| ユースケース | ゲーム、IoT、VoIP | Webサイト、API、動画配信 |

## ユースケース
- 静的IPが必要なアプリケーション
- 複数リージョンへの高速フェイルオーバー
- ゲーム、IoT、VoIP等のTCP/UDPトラフィック

## SAA試験ポイント
- ==静的IP + グローバル高速化== → Global Accelerator
- ==キャッシュ + HTTP== → CloudFront
- ==TCP/UDP + 低レイテンシ== → Global Accelerator
- ==マルチリージョンフェイルオーバー== → Global Accelerator
