# Amazon Lightsail

```
+------------------------------------------+
|            Amazon Lightsail              |
|  +------------------------------------+  |
|  | Instance (VPS)                     |  |
|  |  +----------+  +----------------+  |  |
|  |  | Compute  |  | Storage (SSD)  |  |  |
|  |  +----------+  +----------------+  |  |
|  |  +----------+  +----------------+  |  |
|  |  | Memory   |  | Data Transfer  |  |  |
|  |  +----------+  +----------------+  |  |
|  +------------------------------------+  |
|                                          |
|  月額固定料金で全てパッケージ化          |
+------------------------------------------+
```

## Overview
- `Instances`:        仮想サーバー (Linux/Windows) / ==$3.50〜/月 固定==
- `Containers`:       コンテナサービス
- `Databases`:        マネージドDB (MySQL/PostgreSQL)
- `Storage`:          オブジェクトストレージ
- `Load Balancer`:    ロードバランサー
- `CDN`:              コンテンツ配信

## Blueprints (事前構成イメージ)
- `CMS`:              WordPress, Joomla, Drupal
- `アプリ`:           Node.js, LAMP, Django, MEAN
- `OS`:               Amazon Linux, Ubuntu, Windows Server

## EC2 への移行
- Lightsail スナップショット -> EC2 AMI としてエクスポート可能
- 成長に伴いEC2へスケールアップ
