# AWS IoT Core

IoTデバイスをクラウドに安全に接続し、メッセージの送受信・処理を行うフルマネージドサービス。

```
+------------------+       +---------------------------+       +------------------+
|    IoT Devices   |       |       AWS IoT Core        |       |   AWS Services   |
|  - Sensors       |       |  +---------------------+  |       |  - Lambda        |
|  - Cameras       | <---> |  |  Device Gateway     |  | ----> |  - S3            |
|  - Industrial    |  MQTT |  |  (MQTT/HTTPS)       |  |       |  - DynamoDB      |
|  - Vehicles      |       |  +---------------------+  |       |  - Kinesis       |
+------------------+       |  +---------------------+  |       +------------------+
                           |  |  Rules Engine       |  |
                           |  +---------------------+  |
                           |  +---------------------+  |
                           |  |  Device Shadow      |  |
                           |  +---------------------+  |
                           +---------------------------+
```

## Core Components
- `Device Gateway`:                    デバイス接続エンドポイント / ==MQTT== (軽量Pub/Sub) / ==自動スケール==
- `Message Broker`:                    Pub/Sub メッセージング / トピックベース
- `Device Shadow`:                     ==デバイス状態のJSON表現== / ==オフライン時も状態を保持==
- `Rules Engine`:                      ==SQLライク==でフィルタリング・ルーティング → Lambda, S3, DynamoDB, Kinesis等

## Security
- `X.509 証明書`:                      ==デバイス認証の推奨方式== / 相互TLS (mTLS)
- 転送中暗号化:                        ==TLS必須==

## IoT Greengrass
- `IoT Greengrass`:                    ==エッジでLambda実行== / ==オフライン対応== / ローカル処理

## SAA試験ポイント
| トピック | ポイント |
|---------|---------|
| プロトコル | ==MQTT== が IoT 向け軽量プロトコル |
| Device Shadow | ==オフラインデバイス==の状態管理 |
| Rules Engine | ==SQLライク==でAWSサービスへルーティング |
| セキュリティ | ==X.509証明書==でデバイス認証 |
| Greengrass | ==エッジ==でローカル処理・オフライン対応 |
