# AWS IoT Core

IoTデバイスをクラウドに安全に接続し、メッセージの送受信・処理を行うフルマネージドサービス。

```
+------------------+       +---------------------------+       +------------------+
|    IoT Devices   |       |       AWS IoT Core        |       |   AWS Services   |
|  - Sensors       |       |  +---------------------+  |       |  - Lambda        |
|  - Cameras       | <---> |  |  Device Gateway     |  | ----> |  - S3            |
|  - Industrial    |  MQTT |  |  (MQTT/HTTPS/WS)    |  |       |  - DynamoDB      |
|  - Vehicles      |       |  +---------------------+  |       |  - Kinesis       |
+------------------+       |  +---------------------+  |       |  - SNS/SQS       |
                           |  |  Message Broker     |  |       |  - CloudWatch    |
                           |  +---------------------+  |       +------------------+
                           |  +---------------------+  |
                           |  |  Rules Engine       |  |
                           |  +---------------------+  |
                           |  +---------------------+  |
                           |  |  Device Shadow      |  |
                           |  +---------------------+  |
                           +---------------------------+
```

## Core Components

### Device Gateway
- `Device Gateway`:                    デバイスとIoT Coreを接続するエンドポイント
  - プロトコル:
    - `MQTT`:                          軽量Pub/Sub / ==ポート8883== / IoT向け標準
    - `MQTT over WebSocket`:           ブラウザ対応 / ポート443
    - `HTTPS`:                         RESTful / ポート443
  - スケーリング:                      ==自動スケール== / 数十億デバイス対応

### Message Broker
- `Message Broker`:                    ==Pub/Sub メッセージング== / トピックベース
  - Topic:                             階層構造 (`sensors/room1/temperature`)
  - QoS (Quality of Service):
    - QoS 0:                           最大1回配信 (At most once)
    - QoS 1:                           最低1回配信 (At least once)

### Device Shadow
- `Device Shadow`:                     ==デバイス状態のJSON表現== / オフライン時も状態を保持
  - 構造:
    - `desired`:                       アプリが要求する状態
    - `reported`:                      デバイスが報告する状態
    - `delta`:                         desired と reported の差分
  - ユースケース:
    - デバイスがオフラインでも状態変更を送信可能
    - 再接続時に最新状態を同期
    - 双方向の状態管理

### Rules Engine
- `Rules Engine`:                      ==メッセージをフィルタリング・変換・ルーティング==
  - SQL文:                             `SELECT * FROM 'topic/subtopic' WHERE temperature > 30`
  - アクション (宛先):
    | アクション | 用途 |
    |-----------|------|
    | Lambda | カスタム処理 |
    | S3 | データ保存 |
    | DynamoDB | NoSQL保存 |
    | Kinesis Data Streams | ストリーム処理 |
    | Kinesis Data Firehose | S3/Redshift配信 |
    | SNS | 通知 |
    | SQS | キューイング |
    | CloudWatch | メトリクス/ログ |
    | IoT Analytics | IoTデータ分析 |
    | Step Functions | ワークフロー |

## Security

### 認証
- `X.509 証明書`:                      ==デバイス認証の推奨方式== / 相互TLS (mTLS)
  - AWS IoT で証明書を発行
  - 証明書 + ポリシーをデバイスにアタッチ
- `IAM`:                               AWSサービス/ユーザー向け
- `Cognito`:                           モバイルアプリユーザー向け
- `Custom Authorizer`:                 Lambda でカスタム認証ロジック

### 認可
- `IoT Policy`:                        ==JSON形式== / デバイスの操作権限を定義
  - アクション例:                      `iot:Connect`, `iot:Publish`, `iot:Subscribe`, `iot:Receive`
  - リソース例:                        `arn:aws:iot:region:account:topic/sensors/*`

### 暗号化
- 転送中:                              ==TLS 1.2 必須==
- 保存時:                              AWS管理キーで暗号化

## Related Services

| サービス | 用途 |
|---------|------|
| `IoT Device Management` | デバイスの登録・整理・監視・リモート管理 |
| `IoT Device Defender` | セキュリティ監査・異常検知 |
| `IoT Analytics` | IoTデータの収集・処理・分析 |
| `IoT Events` | イベント検知・アクション実行 |
| `IoT Greengrass` | ==エッジでLambda実行== / オフライン対応 |
| `IoT SiteWise` | 産業機器データの収集・分析 |

## SAA試験頻出ポイント

| トピック | ポイント |
|---------|---------|
| プロトコル | ==MQTT== が IoT 向け軽量プロトコル |
| Device Shadow | ==オフラインデバイス==の状態管理 |
| Rules Engine | ==SQLライク==でフィルタ・ルーティング |
| セキュリティ | ==X.509証明書==でデバイス認証 |
| Greengrass | ==エッジ==でローカル処理・オフライン対応 |
| スケーリング | 数十億デバイスまで==自動スケール== |

## ユースケース

| ユースケース | 説明 |
|-------------|------|
| スマートホーム | 照明、サーモスタット、セキュリティカメラ |
| 産業IoT (IIoT) | 工場機器監視、予知保全 |
| コネクテッドカー | テレマティクス、車両追跡 |
| ヘルスケア | ウェアラブル、医療機器モニタリング |
| スマートシティ | 交通管理、環境センサー |
