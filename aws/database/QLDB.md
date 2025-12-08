# Amazon QLDB (Quantum Ledger Database)

## Overview
- 台帳データベース:                        ==イミュータブル== / ==暗号的に検証可能== な変更履歴
- フルマネージド:                          ==サーバーレス== / 自動スケーリング
- クエリ:                                  ==PartiQL== (SQL互換)

## Features
- `Journal`:                               全ての変更を追記専用で記録 / 削除・改ざん不可
- `Cryptographic Verification`:            SHA-256ハッシュで履歴の整合性を検証可能
- `History Function`:                      任意時点のデータ状態を照会可能

## Use Cases
- 監査証跡:                                金融取引、規制対応
- サプライチェーン:                        商品の追跡・来歴管理
- 人事記録:                                変更履歴の完全な保持

## QLDB vs Managed Blockchain
| 項目 | QLDB | Managed Blockchain |
|-----|------|-------------------|
| 信頼モデル | ==中央集権型== | ==分散型== |
| 管理者 | 単一の信頼できる機関 | 複数パーティで合意 |
| 用途 | 単一組織内の監査証跡 | 複数組織間での信頼構築 |

## SAA試験ポイント
- 「変更履歴を完全に追跡」「監査証跡」「改ざん不可」→ ==QLDB==
- 「信頼できる中央機関がある」→ ==QLDB==
- 「複数組織間で信頼が必要」→ ==Managed Blockchain==
