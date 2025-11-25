# DynamoDB

```HCL
resource "aws_dynamodb_table" "hoge" {      # (Required) ローカルの識別子
  attribute {
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

  name           = "GameScores"             # (Required) AWS Region 内での識別子
  hash_key       = "UserId"                 # (Required) Attribute to use as the hash (partition) key.

  range_key      = "GameTitle"              # Sort Key
  region         = ~~                       # Optional

  # -----------
  # Table class
  # -----------
  table_class = "STANDARD"                  # Standard or Standard-IA (STANDARD_INFREQUENT_ACCESS)

  # -------------------
  # Capacity calculator
  # -------------------
  read_capacity  = 20
  write_capacity = 20

  ttl {
    attribute_name = "TimeToExist"
    enabled        = true
  }

  import_table                = ~~

  # ----------------------------
  # Read/write capacity settings
  # ----------------------------
  billing_mode   = "PROVISIONED"            # Capacity Mode / "PAY_PER_REQUEST" or "PROVISIONED"

  # ---------------
  # Warm throughput
  # ---------------
  warm_throughput {                         # 即座に処理できるスループット容量を事前に確保する機能
    read_units_per_second  = 1000
    write_units_per_second = 500
  }

  # -----------------
  # Secondary indexes
  # -----------------
  global_secondary_index {                  # GSI
    name               = "GameTitleIndex"
    hash_key           = "GameTitle"
    range_key          = "TopScore"
    write_capacity     = 10
    read_capacity      = 10
    projection_type    = "INCLUDE"
    non_key_attributes = ["UserId"]
  }

  # ------------------
  # Encryption at rest
  # ------------------
  server_side_encryption {
    enabled = true                          # if false, AWS-own key
    kms_key_arn =                           # if enabled = true and this is specified, AWS KMS-managed key
  }                                         # else, Customer managed key

  # -------------------
  # Deletion protection
  # -------------------
  deletion_protection_enabled = false       # 削除する前に削除保護を無効化する手順を踏ませるようにできる

  # ----
  # Tags
  # ----
  tags = {
    Name = local.table_name                 # Key = Value
  }
}
```

    local_secondary_index
    on_demand_throughput
    point_in_time_recovery
    replica
    global_table_witness
    restore_date_time
    restore_source_name
    restore_source_table_arn
    restore_to_latest_time
    stream_enabled
    stream_view_type
    ttl
