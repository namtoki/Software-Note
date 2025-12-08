# AWS Transfer Family

```
既存のファイル転送クライアント
      ↓ SFTP / FTPS / FTP / AS2
AWS Transfer Family
      ↓
   S3 / EFS
```

## Overview
- ファイル転送サービス:              ==SFTP / FTPS / FTP / AS2== で S3 / EFS に転送
- フルマネージド:                    サーバー管理不要
- 用途:                              ==既存のファイル転送ワークフローを維持==

## Protocols
| プロトコル | 説明 |
|-----------|------|
| ==SFTP== | SSH File Transfer Protocol (セキュア) |
| ==FTPS== | FTP over TLS |
| ==FTP== | 非暗号化 (VPC内のみ) |
| ==AS2== | B2B データ交換 (EDI) |

## Storage
| 転送先 | 用途 |
|-------|------|
| ==S3== | オブジェクトストレージ |
| ==EFS== | 共有ファイルシステム |

## Transfer Family vs DataSync
| | Transfer Family | DataSync |
|--|----------------|----------|
| 用途 | ==既存SFTPワークフロー維持== | 大量データ移行・同期 |
| プロトコル | SFTP/FTPS/FTP | 独自エージェント |
| ユースケース | パートナー連携、B2B | DC移行、定期同期 |

## SAA試験ポイント
| シナリオ | 解答 |
|---------|------|
| 既存のSFTPワークフローをAWSに移行 | ==Transfer Family== |
| パートナーがSFTPでファイル送信 | ==Transfer Family== |
| 大量データをオンプレからS3に移行 | ==DataSync== |
