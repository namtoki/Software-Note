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
- optional:
    - 明示的アンラップ
        - `let optionlInt: Int? = 1`
            - 👍デフォルト (??):
                - `let optionalInt: Int? = nil`
                - `let int = optionalInt ?? 3 // 3`
            - 強制アンラップ (!):
                - `let a: Int? = 1`
                - `let b: Int? = 1`
                - `a! + b! // 2`
            - 👍オプショナルバインディング:
                - `let optionalDouble = Optional(1.0) // 1`
                - `let optionalIsInfinite: Bool?`
                - `if let double = optionalDouble {`
                - `    optionalIsInfinite = double.isInfinite`
                - `} else {`
                - `    optionalIsInfinite = nil`
                - `}`
            - 👍オプショナルチェイン (?):
                - `let optionalDouble = Optional(1.0) // Optional(1.0)`
                - `let optionalIsInfinite = optionalDouble?.isInfinite`
                - `print(String(describing: optionalIsInfinite))`
    - 暗黙的アンラップ
        - `let a: Int! = 1`
        - `a + 1 // Int型と同様に演算が可能`
        - `var b: Int! = nil`
        - `b + 1 // 値が入っていないため実行時エラー`
- Cast:
    - アップキャスト:
        - 👍明示的アップキャスト:
            - `let any = "abc" as Any`
        - 暗黙的アップキャスト:
            - `let any: Any = "abc"`
    - ダウンキャスト:
        - 👍通常のダウンキャスト (?):
            - `let any = 1 as Any`
            - `let int = any as? Int // Optional(1)`
            - `let string = any as? String // nil`
        - 強制的ダウンキャスト (!):
            - `let any = 1 as Any`
            - `let int = any as! Int`
            - `let string = any as! String // 実行時エラー`
