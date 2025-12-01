# CloudFormation

## Terminology
- `Template`:                 JSON/YAML形式、Infrastructure as Code (IaC)
- `Stack`:                    ==Account, Region 固定== / テンプレートからプロビジョニングされるリソースの集合
- `Change Sets`:              スタック更新前の変更内容プレビュー
- `Stack Sets`:               ==複数のAWSアカウント・リージョン==に対して、1つのテンプレートからスタックを一括デプロイ
- `Drift Detection`:          CloudFormationで作成したリソースが、テンプレートの定義と異なる状態になっていないかを検出
- `Deletion Policy`:          スタック削除時に、リソースをどう扱うかを指定する属性
  - ```yaml
    Resources:
      MyDB:
        Type: AWS::RDS::DBInstance
        DeletionPolicy: Retain    # Retain / Snapshot / Delete
    ```
- `Infrastructure Composer`:  Template をビジュアルで設計できるツール / ドラッグ＆ドロップでAWSリソースを配置
- `IaC generator`:            既存リソースからテンプレート生成（リバースエンジニアリング）
- `Hooks`:                    スタック操作の前後にカスタムロジックを実行し、リソースの作成・更新を検証・制御する機能
⏺ `CloudFormation Registry`:  CloudFormationで使用できる拡張機能（Extensions）を管理する場所

## Template
```yaml
AWSTemplateFormatVersion: "2010-09-09"
Description: テンプレートの説明
Parameters:     # 入力パラメータ
Mappings:       # キー値マッピング
Conditions:     # 条件分岐
Resources:      # AWSリソース定義（必須）
Outputs:                    # `Outputs` + `Export` でクロススタック参照
  VPCId:
    Description: VPC ID
    Value: !Ref MyVPC
    Export:
      Name: MyApp-VPC-ID    # エクスポート名（リージョン内で一意）
```

### 2. 組み込み関数
- `!Ref` - パラメータ/リソース参照
- `!GetAtt` - リソース属性取得
- `!Sub` - 文字列置換
- `!ImportValue` - 他スタックの出力値インポート

## ロールバック動作
- 作成失敗時：自動ロールバック（デフォルト）
- 更新失敗時：前の状態に戻る
- `--disable-rollback` オプションでデバッグ可能
