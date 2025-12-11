# Amazon DocumentDB

## Associate Level
- ドキュメント DB:                        ==MongoDB 互換== / フルマネージド / JSON ドキュメント保存

---

## 特徴

| 項目 | 説明 |
|------|------|
| **互換性** | ==MongoDB== API・ドライバー互換 |
| **ストレージ** | 自動スケーリング (最大 128TB) |
| **可用性** | 3 AZ に 6 コピー (Aurora と同様) |
| **レプリカ** | 最大 15 台 |

---

## データベースの使い分け (SAA 頻出)

| 要件 | サービス |
|------|---------|
| リレーショナル (SQL) | ==RDS / Aurora== |
| キーバリュー | ==DynamoDB== |
| ==ドキュメント (JSON)==, ==MongoDB== | ==DocumentDB== |
| グラフ (関係性) | ==Neptune== |
| データウェアハウス | ==Redshift== |

---

## SAA 出題パターン

1. 「==MongoDB== ワークロードを AWS に移行したい」
   → ==DocumentDB==

2. 「==JSON ドキュメント==を保存・クエリしたい」
   → ==DocumentDB== または ==DynamoDB==

3. 「MongoDB 互換でフルマネージド」
   → ==DocumentDB==
