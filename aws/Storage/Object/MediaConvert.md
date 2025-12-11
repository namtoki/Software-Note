# AWS Elemental MediaConvert / Amazon Elastic Transcoder

```
S3 (入力)                                    S3 (出力)
┌─────────┐                                ┌─────────┐
│ video.  │ → MediaConvert / Transcoder → │ video.  │
│ mov     │                                │ mp4/hls │
└─────────┘                                └─────────┘
```

## Overview
- メディア変換サービス:              S3 のメディアファイルを ==様々なフォーマットに変換==
- 用途:                              デバイス対応、ストリーミング配信 (HLS/DASH)、解像度変換

## MediaConvert vs Elastic Transcoder
| | MediaConvert | Elastic Transcoder |
|--|-------------|-------------------|
| 位置づけ | ==推奨 (新規)== | レガシー |
| 機能 | 高度 (HDR, DRM, 4K等) | 基本的 |
| 料金 | より安い | 分単位 |

## SAA試験ポイント
| シナリオ | 解答 |
|---------|------|
| 動画を様々なフォーマットに変換 | ==MediaConvert== |
| ストリーミング配信用に変換 | ==MediaConvert== + CloudFront |
| 既存ワークフロー (レガシー) | Elastic Transcoder |
