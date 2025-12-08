# Amazon EKS (Elastic Kubernetes Service)

```
+------------------------------------------------------------------+
|                        Amazon EKS                                |
|  +------------------------------------------------------------+  |
|  |              Control Plane (AWS マネージド)                |  |
|  |      API Server, etcd, Controller Manager                  |  |
|  +------------------------------------------------------------+  |
|                              |                                   |
|  +------------------------------------------------------------+  |
|  |              Data Plane (顧客管理)                         |  |
|  |  +------------------+  +------------------+  +-----------+ |  |
|  |  |   EC2 Node       |  |   EC2 Node       |  | Fargate   | |  |
|  |  |   (Pod群)        |  |   (Pod群)        |  | (Pod単位) | |  |
|  |  +------------------+  +------------------+  +-----------+ |  |
|  +------------------------------------------------------------+  |
+------------------------------------------------------------------+
```

## Overview
- Kubernetes サービス:                     ==フルマネージド== Kubernetes
- Control Plane:                           ==AWS マネージド== (複数AZ冗長, etcd暗号化)
- Data Plane:                              顧客管理 (EC2 or Fargate)
- 料金:                                    ==$0.10/時間/クラスター== + ノード料金

## Node Types
| 項目 | マネージドノード | セルフマネージド | Fargate |
|------|----------------|-----------------|---------|
| 管理負荷 | ==低== | 高 | ==最低== |
| カスタマイズ | 中 | 高 | 低 |
| GPU サポート | ○ | ○ | ==✗== |
| DaemonSet | ○ | ○ | ==✗== |
| コスト | EC2 料金 | EC2 料金 | Pod 単位 |

## IAM Roles for Service Accounts (IRSA)
Pod に ==AWS サービスへのアクセス権限== を付与

```
Pod (ServiceAccount)
      ↓ OIDC Token
  IAM Role
      ↓
  S3, DynamoDB 等へアクセス
```

## Storage
| ストレージ | アクセスモード | ユースケース |
|-----------|---------------|-------------|
| ==EBS== | ReadWriteOnce | 単一 Pod のデータ永続化 |
| ==EFS== | ReadWriteMany | 複数 Pod での共有ストレージ |

## Load Balancing
| K8s リソース | AWS Load Balancer |
|-------------|-------------------|
| Ingress | ==ALB== |
| Service (type: LoadBalancer) | ==NLB== |

---

## EKS ファミリー
| 項目 | Amazon EKS | EKS Distro | EKS Anywhere |
|------|------------|------------|--------------|
| 実行場所 | ==AWS Cloud== | どこでも | ==オンプレミス== |
| Control Plane | AWS マネージド | 顧客管理 | 顧客管理 |
| 料金 | $0.10/時間 | 無料 | 無料 (サポート有料) |
| ユースケース | クラウドネイティブ | カスタム構築 | ハイブリッド |

## EKS Anywhere
- オンプレミスで EKS と同じ K8s を実行
- プロバイダー: ==VMware vSphere==, ==Bare Metal==, Nutanix, ==AWS Snow==
- `EKS Connector`: AWS コンソールで可視化 (読み取り専用)

---

## ECS vs EKS
| 項目 | ECS | EKS |
|------|-----|-----|
| オーケストレーター | ==AWS 独自== | ==Kubernetes== |
| 学習コスト | 低い | 高い |
| ポータビリティ | AWS 依存 | ==マルチクラウド可能== |
| 料金 | 無料 | $0.10/時間 |
| 既存 K8s 資産 | 移行必要 | ==そのまま利用== |

---

## SAA試験ポイント
| シナリオ | 解答 |
|---------|------|
| フルマネージド K8s | ==Amazon EKS== |
| サーバーレスで K8s | ==EKS on Fargate== |
| オンプレミスで AWS と同じ K8s | ==EKS Anywhere== |
| データを国外に出せない | ==EKS Anywhere== |
| 切断環境で K8s | ==EKS Anywhere on Snow== |
| Pod から S3 にアクセス | ==IRSA== |
| GPU ワークロード | ==EKS on EC2== (Fargate非対応) |
| 複数 Pod でファイル共有 | ==EFS== |
| K8s 経験があるチーム | ==EKS== |
| AWS に特化、シンプルに | ==ECS== |
