# Amazon Kinesis

==リアルタイムストリーミングデータ==の収集・処理・分析サービス群。

## サービス比較 (SAA頻出)

| サービス | 用途 | 特徴 |
|---------|------|------|
| `Data Streams` | ==リアルタイム取り込み== | シャード単位、カスタム処理、24時間〜365日保持 |
| `Data Firehose` | ==配信 (ETL)== | S3/Redshift/OpenSearch へ、ほぼリアルタイム |
| `Data Analytics` | ==リアルタイム分析== | SQLでストリーム分析 |
| `Video Streams` | ==動画ストリーミング== | カメラ映像の収集・ML分析 |

## Kinesis Data Streams
- `シャード`:                          スループット単位 / ==1シャード = 1MB/秒 (入力), 2MB/秒 (出力)==
- `保持期間`:                          ==24時間 (デフォルト)== 〜 365日
- `コンシューマー`:                    Lambda, EC2, Kinesis Data Analytics 等
- `容量モード`:
  - Provisioned:                       シャード数を手動指定
  - On-demand:                         ==自動スケール== (管理不要)

## Kinesis Data Firehose
- `配信先`:                            ==S3==, Redshift, OpenSearch, Splunk, HTTP エンドポイント
- `変換`:                              Lambda で==データ変換可能==
- `バッファ`:                          サイズ or 時間でバッファリング (==ほぼリアルタイム==, 最短60秒)
- `フルマネージド`:                    シャード管理==不要==

## Data Streams vs Firehose (SAA頻出)

| 項目 | Data Streams | Firehose |
|-----|--------------|----------|
| 管理 | シャード管理必要 | ==フルマネージド== |
| レイテンシ | ==リアルタイム (70-200ms)== | ほぼリアルタイム (60秒〜) |
| カスタム処理 | 可能 | Lambda変換のみ |
| 配信先 | カスタム | S3, Redshift等に限定 |
| データ保持 | 24時間〜365日 | ==保持しない== (配信のみ) |

## 典型的な構成パターン

```
【リアルタイム処理 + S3 格納】
センサー/IoT → Firehose → Data Analytics (SQL分析) → リアルタイム配信
                   ↓
                  S3 (データレイク)
```

- Firehose: 高頻度データを効率的に S3 へ格納
- Data Analytics: SQL でリアルタイム統計処理
- 両方を組み合わせて「リアルタイム配信 + 分析用蓄積」を実現

## SAA試験ポイント
- ==リアルタイム + カスタム処理== → Data Streams
- ==S3/Redshift に配信== → Firehose
- ==シャード管理不要== → Firehose
- ==SQLでストリーム分析== → Data Analytics
- ==リアルタイム処理 + S3格納 を同時に== → ==Firehose + Data Analytics==
