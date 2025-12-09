# Amazon Transcribe

==音声をテキストに変換== (Speech-to-Text) するサービス。

## 特徴
- `リアルタイム`:                      ストリーミング音声を即時変換
- `バッチ`:                            S3 上の音声ファイルを変換
- `話者識別`:                          複数話者を区別
- `カスタムボキャブラリー`:            専門用語・固有名詞の認識精度向上

## バリエーション
- `Transcribe`:                        汎用
- `Transcribe Medical`:                ==医療用語==に特化

## SAA試験ポイント
- ==音声 → テキスト== → Transcribe
- ==テキスト翻訳== → Translate (Transcribeではない)
- ==テキスト → 音声== → Polly (Transcribeではない)
