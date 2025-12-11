# Amazon VPC (Virtual Private Cloud)

```
+----------------------------------------------------------+
|                         VPC                              |
|  CIDR: 10.0.0.0/16                                       |
|                                                          |
|  +------------------------+  +------------------------+  |
|  |  Public Subnet (AZ-a)  |  |  Private Subnet (AZ-a) |  |
|  |  10.0.1.0/24           |  |  10.0.2.0/24           |  |
|  |  +------------------+  |  |  +------------------+  |  |
|  |  |   EC2 (Web)      |  |  |  |   EC2 (App/DB)   |  |  |
|  |  +------------------+  |  |  +------------------+  |  |
|  +------------------------+  +------------------------+  |
|           |                           |                  |
|           v                           v                  |
|     Internet GW                  NAT Gateway             |
+----------------------------------------------------------+
```

## Overview
- Virtual Private Cloud:
  - `CIDR`:                     VPC作成時に IPv4 CIDRブロック を指定 (必須) / /16 ~ /28 / ==変更不可==
    - Secondary CIDR:         後から追加可能 (最大5個、拡張で最大200個)
  - Subnet:                   VPC内のIPアドレス範囲を分割した単位 / ==AZをまたげない==
    - `Public Subnet`:          IGW と直接接続 (Route Table `0.0.0.0/0 -> IGW`, Instance に Public IP/Elastic IP 付与)
    - `Private Subnet`:         Public Subnet と NAT 経由でインターネット接続
    - 予約IP:                 .0 (ネットワーク) .1 (VPCルーター) .2 (DNS サーバー) .3 (将来利用) .255 (ブロードキャスト)
  - Route Table:              各サブネットは 1つのテーブル に関連付け / 最長プレフィックスマッチ (最も具体的なルートが優先)
    - `Main Route Table`:       VPC作成時に自動作成、明示的に関連付けのないサブネットが使用
    - `Custom Route Table`:     必要に応じて作成
  - ファイアウォール:
    - `Network ACL`:            ==サブネット単位==   / ==ステートレス== / 特定 IP のブロック / エフェメラルポート許可設定
    - `Security Group`:         ==インスタンス単位== / ==ステートフル== (戻りトラフィックの自動許可)
  - `Internet Gateway (IGW)`:   VPCとインターネット間の通信 / ==高可用性 (Managed)== / 1VPCに1IGW / 
  - `NAT Gateway`:              ==$0.062/時間+$0.062/GB== / ==高可用性 (Managed, 単一AZ内)== / Elastic IPが必要 / 複数AZ可能
  - `VPC ピアリング`:           2つのVPC間でプライベート接続 / 異なるリージョン,アカウント 間でも可能
  - `VPC Flow Logs`:            VPC内のIPトラフィックをキャプチャ / 出力先: CloudWatch Logs, S3, Kinesis Data Firehose
  - `Elastic IP アドレス`:      静的 Public IPv4 Addr / 1Regionあたり5個上限 / Instance 間で付け替え可能
- `VPC Endpoint`:               インターネットを経由せずにAWSサービスにプライベート接続
  - `Gateway Endpoint`:         ==無料== / VPC ⇔ S3, DynamoDB / VPC内からのみアクセス可能
  - `Interface Endpoint`:       ==$0.014/時間+$0.01/GB== / VPC ⇔ 他 AWS サービス / ENI を作成
  - `AWS PrivateLink`:          VPC間でプライベートサービス公開
    - 構成:                     サービス提供側に ==NLB 必須== + VPCエンドポイントサービス
    - 利用側:                   Interface Endpoint で接続 / ==DNS名でアクセス可==
    - 特徴:                     インターネット非経由 / VPCピアリング不要
- VPN:
  - Virtual Private Gateway:
    - `Site-to-Site VPN`:       ==!$0.05/h + 転送料金== / VPC ⇔ オンプレ (==ネット経由==)
    - `Direct Connect`:         ==!高い== / VPC ⇔ オンプレ (==専用物理回線==)
  - Clients VPN endpoints:
    - `Client VPN`:             VPC ⇔ リモートユーザー(個人デバイス) / OpenVPNベース
- Hub:
  - `AWS Transit Gateway`:      ==!$0.05/h+$0.02/GB== / 複数のVPC,VPN,Direct Connectを相互接続 / ネットワークトポロジーを簡素化
  - `Direct Connect Gateway`:   複数リージョンのVPCに1つのDirect Connectで接続
