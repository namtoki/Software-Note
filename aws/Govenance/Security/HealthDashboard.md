# AWS Health Dashboard

⏺ `AWS Health Dashboard`                    ==Service Health Dashboard== と ==Your Account Health== を可視化し、影響を通知 / Event Bridge で自動通知させると便利

## Overview
- サービス稼働状況の確認:                   AWS サービスの障害・メンテナンス情報を提供
  - `Service Health Dashboard`:            ==全 AWS==のサービス稼働状況 (公開)
  - `Personal Health Dashboard`:           ==自アカウント==に影響するイベント通知

---

## Service Health vs Personal Health (SAA 頻出)

| 項目 | ==Service Health== | ==Personal Health== |
|------|--------------------|--------------------|
| **対象** | ==全 AWS ユーザー== | ==自アカウントのみ== |
| **内容** | 全リージョンの障害情報 | 自分のリソースへの影響 |
| **通知** | なし | ==EventBridge 連携==可能 |

---

## SAA 出題パターン

| シナリオ | 回答 |
|---------|------|
| 「==自アカウント==に影響する AWS 障害を通知」 | ==Personal Health Dashboard== |
| 「AWS 障害時に ==EventBridge で自動対応==」 | ==Personal Health Dashboard== |
| 「AWS 全体のサービス稼働状況を確認」 | ==Service Health Dashboard== |
