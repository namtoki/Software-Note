# DynamoDB

```HCL
resource "aws_dynamodb_table" "basic-dynamodb-table" {  # ローカルの識別子
  name           = "GameScores"                         # (Required) AWS Region 内での識別子
  billing_mode   = "PROVISIONED"                        # Capacity Mode / "PAY_PER_REQUEST" or "PROVISIONED"
  read_capacity  = 20                                   # (PROVISIONED)
  write_capacity = 20                                   # (PROVISIONED)
  hash_key       = "UserId"                             # (Required) Attribute to use as the hash (partition) key.
  range_key      = "GameTitle"

  attribute {                                           # (Required) Only required for hash_key and range_key attributes.
    name = "UserId"
    type = "S"
  }

  attribute {
    name = "GameTitle"
    type = "S"
  }

  attribute {
    name = "TopScore"
    type = "N"
  }

  ttl {
    attribute_name = "TimeToExist"
    enabled        = true
  }

  global_secondary_index {                              # GSI
    name               = "GameTitleIndex"
    hash_key           = "GameTitle"
    range_key          = "TopScore"
    write_capacity     = 10
    read_capacity      = 10
    projection_type    = "INCLUDE"
    non_key_attributes = ["UserId"]
  }

  tags = {
    Name        = "dynamodb-table-1"
    Environment = "production"
  }

  # region                      = ~~
  # deletion_protection_enabled = ~~
  # import_table                = ~~
  # server_side_encryption {
  #   enabled = true
  # }
}
```
