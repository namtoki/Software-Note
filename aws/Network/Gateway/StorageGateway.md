# AWS Storage Gateway

```
オンプレミス                        AWS Cloud
┌─────────────┐                  ┌─────────────┐
│  Server /   │                  │  S3 / EBS   │
│  App        │ ←── Gateway ──→  │  / Glacier  │
│             │                  │             │
└─────────────┘                  └─────────────┘
```

## Overview
- ハイブリッドストレージ:         ==オンプレミス== と ==AWS ストレージ== をシームレスに接続
  - 用途:                         バックアップ、DR、データ移行、クラウド拡張
  - デプロイ:                     ==VM (VMware/Hyper-V)== または ==ハードウェアアプライアンス==
  - `Gateway Types`:
    - `S3 File Gateway`:            ==NFS/SMB== → S3
    - `FSx File Gateway`:           ==SMB== → FSx for Windows
    - `Volume Gateway`:             ==iSCSI== ブロックストレージ (S3 + EBS)
      - `Cached`:                   データは ==S3==、頻繁にアクセスするデータをローカルキャッシュ
      - `Stored`:                   データは ==ローカル==、S3 に非同期バックアップ
    - `Tape Gateway`:               ==仮想テープ== (VTL) (S3 + Glacier) / 用途: ==物理テープ== から ==仮想テープ (VTL)== への移行
