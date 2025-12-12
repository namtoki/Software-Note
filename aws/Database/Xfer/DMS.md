# AWS DMS (Database Migration Service)

## Overview
- DB 移行サービス:    オンプレ/クラウドから AWS への DB 移行 / ==ソース稼働中でも移行可能==
  - 移行タイプ:
    - 同種移行:       MySQL → MySQL, Oracle → Oracle
    - 異種移行:       Oracle → ==SCT (スキーマ変換)== → DMS (データ移行) → PostgreSQL (RDS)
  - `CDC`:              継続的レプリケーション /==変更データを継続的に同期== / ==ダウンタイム最小==で移行
