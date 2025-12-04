# Amazon Kinesis Video Streams

動画・音声ストリーミングデータをAWSにリアルタイムで取り込み、保存、処理するためのフルマネージドサービス。

```
+------------------+       +---------------------------+       +------------------+
|  Video Sources   |       | Kinesis Video Streams     |       |  Consumers       |
|  - IP Camera     | ----> |  - Ingest                 | ----> |  - Rekognition   |
|  - Drone         |       |  - Store (encrypted)      |       |  - SageMaker     |
|  - Smartphone    |       |  - Index                  |       |  - Custom App    |
|  - IoT Device    |       |  - Playback               |       |  - HLS Player    |
+------------------+       +---------------------------+       +------------------+
```

## Functions
- `Producer`:                       動画を送信するデバイス・アプリ / SDK提供 (C++, Java, Android, iOS)
- `Video Stream`:                   動画データを格納するリソース / 自動スケーリング
- `Consumer`:                       動画を取得・処理するアプリ / HLS, DASH, GetMedia API
- `Playback`:                       HLS/DASH でブラウザ・モバイルで再生可能
- `保存期間`:                       数時間〜数年 (設定可能) / ==保存しない設定も可能==

## 料金
- `取り込み (Ingest)`:              ==$0.0085/GB==
- `データ保存`:                     ==$0.023/GB/月==
- `データ消費 (Egress)`:            ==$0.0085/GB==
- `HLS/DASH ストリーミング`:        ==$0.0119/GB==

---

## Kinesis ファミリー比較

| サービス | 対象データ | 用途 |
|---------|-----------|------|
| **Kinesis Video Streams** | 動画・音声 | カメラ映像の収集・ML分析 |
| Kinesis Data Streams | ログ、クリックストリーム | リアルタイムデータ処理 |
| Kinesis Data Firehose | 同上 | S3/Redshift/OpenSearch へ配信 |
| Kinesis Data Analytics | ストリームデータ | SQLでリアルタイム分析 |

---

## ユースケース

| ユースケース | 説明 |
|-------------|------|
| スマートホーム | ドアベルカメラ、ベビーモニター |
| 監視・セキュリティ | 防犯カメラ映像の収集・分析 |
| 機械学習連携 | Rekognition Video で顔認識・物体検出 |
| 産業用途 | 工場ラインの監視、品質検査 |
| メディア | ライブ配信、VODコンテンツ管理 |

---

## 連携サービス

| サービス | 連携内容 |
|---------|---------|
| Amazon Rekognition Video | 顔認識、物体検出、人物追跡 |
| Amazon SageMaker | カスタムMLモデルで動画分析 |
| AWS IoT Core | IoTデバイスからの動画取り込み |
| Amazon S3 | 動画のアーカイブ保存 |

