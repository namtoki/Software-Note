# Amazon Keyspaces (for Apache Cassandra)

## Overview
- Apache Cassandra 互換:                   ==CQL (Cassandra Query Language)== 対応
- フルマネージド:                          ==サーバーレス== / 自動スケーリング / パッチ適用不要
- 移行:                                    既存Cassandraアプリをそのまま移行可能

## Capacity Mode
- `On-demand`:                             トラフィックに応じて自動スケール / 予測困難なワークロード向け
- `Provisioned`:                           読み書きキャパシティを事前指定 / 予測可能なワークロード向け

## High Availability
- データレプリケーション:                  ==3つのAZ== に自動複製
- 耐久性:                                  99.999999999% (11 nines)

## Security
- 保存時の暗号化:                          ==KMS== (AWS管理キー or CMK)
- 転送中の暗号化:                          ==TLS==
- アクセス制御:                            IAM ポリシー

## SAA試験ポイント
- 「既存Cassandraワークロードの移行」→ ==Keyspaces==
- 「Cassandra運用負担を減らしたい」→ ==Keyspaces== (vs EC2上で自己管理)
- DynamoDB との違い: Cassandra互換が必要な場合に選択
