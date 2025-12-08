# Amazon Rekognition

==画像・動画分析==サービス。機械学習による視覚的コンテンツ分析。

## 機能
- `顔検出・認識`:                      顔の検出、比較、検索
- `オブジェクト検出`:                  物体、シーン、アクティビティの識別
- `テキスト検出`:                      画像内の文字を抽出 (OCR)
- `コンテンツモデレーション`:          ==不適切コンテンツ==の検出
- `有名人認識`:                        著名人の識別
- `PPE検出`:                           保護具 (ヘルメット等) の着用確認

## 対応メディア
- `Image`:                             S3 または Base64 エンコード
- `Video`:                             S3 / Kinesis Video Streams

## SAA試験ポイント
- ==画像・動画分析== → Rekognition
- ==顔認識・検出== → Rekognition
- ==不適切コンテンツ検出== → Rekognition (Content Moderation)
- ==画像内テキスト抽出== → Rekognition (vs Textract: ドキュメント向け)
