# IAM Policy

## Terraform

### aws_iam_role_policy_attachment

既存のマネージドポリシー（AWS管理またはカスタム）をIAMロールにアタッチする

```HCL
resource "aws_iam_role_policy_attachment" "lambda_basic" {
  role       = aws_iam_role.lambda_execution.name
  policy_arn = "arn:aws:iam::aws:policy/service-role/AWSLambdaBasicExecutionRole"
}
```

### aws_iam_role_policy

インラインポリシーをIAMロールに直接作成・埋め込む

```HCL
resource "aws_iam_role_policy" "test_policy" {
  name = "test_policy"                                  # (Optional)
  name_prefix = "my-app-role-"                          # (Optional) 末尾ランダム文字列 (my-app-role-20231215abc123)
  role = aws_iam_role.test_role.id                      # (Required) IAM Role

  policy = jsonencode({                                 # (Required)
    Version = "2012-10-17"
    Statement = [
      {
        Action = [
          "ec2:Describe*",
        ]
        Effect   = "Allow"
        Resource = "*"
      },
    ]
  })
}
```
