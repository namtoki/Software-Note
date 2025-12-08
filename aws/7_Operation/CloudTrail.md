# CloudTrail

セキュリティ監査、コンプライアンス、トラブルシューティングに利用

```
ユーザー/サービス
      |
      v
   API コール（EC2起動、S3アップロード等）
      |
      v
   CloudTrail が記録
      |
      +---> CloudTrail コンソール（90日間）
      +---> S3（長期保存）
      +---> CloudWatch Logs（リアルタイム監視）
```

## Functions
- 基本設定:
  - 証跡名:                           一意の識別子
  - 適用範囲:                         ==単一リージョン or 全リージョン== (セキュリティのベストプラクティスは全リージョン)
  - S3 バケット:                      ログの保存先 (S3 バケットポリシーで、CloudTrail からの書き込みを許可すること)
  - ログファイル暗号化:               SSE-S3 または SSE-KMS
- 誰が、いつ、何をしたかを記録:
  - 誰が:                             userIdentity（IAMユーザー、ロール、root等）
  - いつ:                             eventTime（UTC）
  - 何をしたか (Event):
    - `Management Events`:              ==Default ON（90日間保持）== / リソースの操作 (EC2起動、IAMユーザー作成など)
      - 料金:                         各リージョンの最初の証跡は無料、2つ目以降は $2.00 / 100,000 イベント
    - `Data Events`:                    データの操作 (S3オブジェクト操作、Lambda実行など)
      - 料金:                         $0.10 / 100,000 イベント
    - `Insights Events`:                異常なアクティビティ検出 (API コール急増など)
      - 料金:                         $0.35 / 100,000 分析イベント
- `ログファイル整合性検証`:             ログの改ざん検知（ダイジェストファイル）/ 無料

## Best Practice
### CloudWatch Logs 連携
```
CloudTrail → CloudWatch Logs → Metric Filter → Alarm
```
- リアルタイムでログを監視
- 特定 API コールを検知してアラート
**例**: root ユーザーログイン検知
```
{ $.userIdentity.type = "Root" && $.eventType = "AwsConsoleSignIn" }
```
### 組織の証跡（Organization Trail）
- AWS Organizations で**全アカウントのログを集約**
- 管理アカウントで設定
