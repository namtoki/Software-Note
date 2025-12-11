# AWS Compute Optimizer

- ==!AWS Compute Optimizer==                   直近 14 日間のコンピュータリソースの最適化提案 / EC2, Auto Scaling Groups, EBSボリューム, Lambda / ==!14日以上設定だと課金==

## Overview
- リソース最適化:                           ==機械学習==で使用状況を分析し、最適なリソース構成を推奨

---

## 対象リソース

| リソース | 推奨内容 |
|---------|---------|
| **EC2** | インスタンスタイプ |
| **EBS** | ボリュームタイプ・サイズ |
| **Lambda** | メモリサイズ |
| **Auto Scaling** | グループ設定 |

---

## Trusted Advisor vs Compute Optimizer

| 項目 | ==Trusted Advisor== | ==Compute Optimizer== |
|------|---------------------|----------------------|
| **対象** | 幅広い AWS サービス | ==コンピュート==に特化 |
| **分析** | しきい値ベース | ==機械学習==ベース |
| **詳細度** | 基本的な推奨 | より詳細な推奨 |

---

## SAA 出題パターン

| シナリオ | 回答 |
|---------|------|
| 「==EC2 インスタンスタイプ==を最適化したい」 | ==Compute Optimizer== |
| 「==機械学習==でリソース使用状況を分析」 | ==Compute Optimizer== |
| 「Lambda の==メモリサイズ==を最適化」 | ==Compute Optimizer== |
