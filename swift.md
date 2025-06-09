# Swift

## Ecosystem

- ライブラリ
  - 標準ライブラリ
  - コアライブラリ
    - Foundation
    - libdispatch
    - XCTest
    - ..
- 開発ツール
  - Swift Package Manager
  - LLDB

## Project Structure

- `swift package init --type executable`
```
<your-project-name>
 ├── Package.swift                          ... Manifest File
 ├── README.md
 ├── Sources
 │    └── <your-project-name>
 │           └── main.swift
 └── Tests
       ├── LinuxMain.swift
       └── <your-project-name>Tests
              ├── XCTestManifests.swift
              └── demoTests.swift
```
- `swift build`

## Rules

- variables: `var totalValue:Int`
- constants: `let threshould:Int`
- closure: `{ 引数 in 戻り値を返す式 }`
- initializer: `let a:Int = 123          let b:Int64 = Int64(a)`
