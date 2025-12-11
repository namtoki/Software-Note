# IAM Role

## Terraform

### aws_iam_role
```HCL
resource "aws_iam_role" "test_role" {
  name = "test_role"                                        # (Optional, Forces new resource)
  name_prefix = "my-app-role-"                              # (Optional, Forces new resource) 末尾ランダム文字列 (my-app-role-20231215abc123)
  path = "/prod/lambda/"                                    # (Optional) ロールをフォルダのように階層整理し、管理・権限制御をしやすくする
  description = "brabrabra"                                 # (Optional)

  force_detach_policies = var.environment != "production"   # (Optional) ロール削除時に「ポリシーが付いてるから消せません」エラーを回避する

  max_session_duration = 3600                               # (Optional) 1時間（デフォルト）「最長何時間まで有効にできるか」の上限設定

  permissions_boundary = aws_iam_policy.boundary.arn        # (Option) ポリシーをアタッチしても、この範囲を超えた権限は絶対に使えない

  assume_role_policy = jsonencode({                         # (Required)
    Version = "2012-10-17"
    Statement = [
      {
        Action = "sts:AssumeRole"
        Effect = "Allow"
        Sid    = ""
        Principal = {
          Service = "ec2.amazonaws.com"
        }
      },
    ]
  })

  tags = {                                                  # (Optional)
    tag-key = "tag-value"
  }
}
```
