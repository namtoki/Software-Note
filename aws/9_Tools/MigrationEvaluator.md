# AWS Migration Evaluator

オンプレミス環境の==移行コスト試算==・ビジネスケース作成サービス。

## 特徴
- `インベントリ収集`:                  エージェントレス or エージェントでサーバー情報を収集
- `使用率分析`:                        CPU、メモリ、ストレージの==実際の使用率==を分析
- `コスト試算`:                        AWS移行後の==TCO (総所有コスト)==を算出
- `レポート`:                          経営層向けビジネスケースを自動生成

## 移行関連サービス比較 (SAA頻出)

| サービス | 用途 |
|---------|------|
| `Migration Evaluator` | ==コスト試算== / ビジネスケース作成 |
| `Migration Hub` | ==移行進捗の一元管理== |
| `Application Discovery Service` | ==サーバー情報の検出== |
| `DMS` | ==データベース移行== |
| `SMS` | ==サーバー移行== (非推奨 → MGN) |
| `MGN (Application Migration Service)` | ==サーバー移行== (推奨) |

## SAA試験ポイント
- ==移行コスト試算== → Migration Evaluator
- ==移行進捗管理== → Migration Hub
