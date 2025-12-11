# AWS Elastic Disaster Recovery (DRS)

- `Elastic Disaster Recovery (AWS DRS)`     災害復旧サービス / 物理、仮想、クラウドサーバーをAWSに継続的に複製し、迅速な復旧を可能に

## Overview
- 災害復旧 (DR):                            オンプレミス / AWS からの==継続的レプリケーション== / 数分で復旧

---

## 主な特徴

| 項目 | 説明 |
|------|------|
| **RPO** | ==数秒== (継続的レプリケーション) |
| **RTO** | ==数分== (迅速なフェイルオーバー) |
| **ステージング** | 低コストインスタンスで待機 |
| **対象** | オンプレミス / 他クラウド / AWS |

---

## SAA 出題パターン

| シナリオ | 回答 |
|---------|------|
| 「オンプレミスの ==DR サイト==を AWS に構築」 | ==Elastic Disaster Recovery== |
| 「==RPO 数秒 / RTO 数分==の災害復旧」 | ==Elastic Disaster Recovery== |
| 「==継続的レプリケーション==で DR を実現」 | ==Elastic Disaster Recovery== |
