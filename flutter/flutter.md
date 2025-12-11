# Dart

-  変数宣言
    - 型注釈: `int age = 0;`
    - 型推論: `var age = 0;`
    - 遅延初期化: `late String variable = highCostFunction();`
-  組み込み型
    - 数値型: int, double
    - 文字列型: String
    - 論理型: bool
    - 配列: List `final intList = [0, 1, 2, 3];`
    - 集合: Set `final map1 = {'Apple', 'Orange', 'Grapge'}`
    - 連想配列: Map `final map1 = {200: 'OK', 403: 'access forbidden', 404: 'not found'}`
    - タプル: Record `final record = (300, 'cake');`
-  ジェネリクス
-  演算子
    - カスケード記法:
        - ```dart
          final sb = StringBuffer()
            ..write('Hello')
            ..write(',')
            ..write('Dart!!');
          pring(sb.toString()); // Hello, Dart!!
          ```
-  制御構文
    - if-case 文と when
        - ```dart
          final (String?, int?) response = ('OK', 200);
          if (response case (String message, int statusCode) when statusCode == 200) {
            hogehoge
          }
          ```
    - swtich を式として扱うことができる
        - ```dart
          final int statusCode = 省略;
          final message = switch (statusCode) {
            >= 100 && < 200 => 'informational',
            >= 200 && < 300 => 'successful',
            _ => 'error',
          };
          ```
- NullSafety
    - Nullable 型:
        - `型名?` (etc. String? hoge; や int? fuga; など)
    - Null-aware 演算子:
        - `?.` 演算子 (Swift と一緒)
        - `??` 演算子 (Swift と一緒)
        - `??=` 演算子 (変数が null でないなら値を変えず、null なら右辺値を使う)
    - `!` 強制アンラップ (Swift と一緒)
- Class
    - 初期化
        - ```dart
          class Point {
            // 以下いずれか
            Point(int xPosition, int yPosition) : x = xPosition, y = yPosition;
            Point(this.x, this,y);

            int x;
            int y;
          }
          ```
        - ```dart
            Point(this.x, this,y) : assert(x >= 0), assert(y >= 0); // アサーションも可能
          ```
    - 定数コンストラクタ
        - ```dart
          abstract class AppSessionStatus {
            const AppSessionStatus();
          }
          ```
        - コンパイル時にインスタンスを生成できる コンストラクタ
        - そのクラスのインスタンスが「不変（immutable）」であることを前提にしていて、再利用される
        - メモリ効率が良く、Flutter では UI 表示でよく使われる（const Text(...) など）
    - 名前付きコンストラクタ
        - ```dart
            const Point.zero() : x = 0, y = 0;
          ```
    - 拡張メソッド
        - ```dart
          extention <拡張名> on <拡張先> {
          }
          ```
    - クラス修飾子
        - abstract      処理本体を書かない
        - base          extends:o, implements:x
        - interface     extends:x, implements:o
        - final         extends:x, implements:x
        - mixin
            - ```dart
              mixin Horse on Animal {
                  void run() { print('run'); }
              }
              mixin Bird {
                  void fly() { print('fly'); }
              }
              class Pegasus extends Animal with Bird, Horse { }
              ```
        - sealed
            - ```dart
              sealed class Shape { abstrac int corner; }
              class Rectangle extends Shape {
                @override
                int corner = 4;
              }
              class Triangle extends Shape {
                @override
                int corner = 3;
              }
              ...
              final Shape shpae = getShape();

              switch (shape) {
                case Rectangle(): print("Rectangle");
                case Triangle(): print("Triangle");
                ...
              }
              ```
- 非同期処理 (Future, async)
    - then
        - ```dart
          import 'dart:async';
          void main() async {
            print("main begin");
            Future<String> result1 = asyncFunc("data1", 5);
            result1.then((result) {
                print(result);
            });
            print("main end");
          }
          Future<String> asyncFunc(String name, int time) async {
            return Future.delayed(Duration(seconds: time), () {
              return "${name}:${DateTime.now().toString()}";
            });
          }
          ```
    - await
        - ```dart
          import 'dart:async';

          void main() async {
              print("main begin");
              print("data1 start");
              print(await asyncFunc("data1", 3));
              print("main end");
          }
          ```
    - Future.wait(List)
        - ```dart
          void main() async {
              print("main begin");
              print("data1 start");
              Future<String> data1 = asyncFunc("data1", 5);
              print("data2 start");
              Future<String> data2 = asyncFunc("data2", 3);
              print("data3 start");
              Future<String> data3 = asyncFunc("data3", 1);
              print("main end");
              List<String> datalist = await Future.wait([data1,data2,data3]);
              for(String data in datalist){
                  print(data);
              }
          }
          ```
- 非同期処理 (Stream)
    - listen()
    - pause()
    - resume()
    - onDone()
    - StreamController

---

# Flutter

## Tree

- Widget Tree
    - Immutable なオブジェクトで構成される
    - 頻繁に作り替えられるので、生成と破棄のコストが小さくなるように設計される
- Element Tree
    - Mutable なオブジェクトで構成される
    - 他の Tree の仲介
        - Widget の状態を管理
        - RenderObject のライフサイクルの管理
- RenderObject Tree
    - Mutable なオブジェクトで構成される
    - 画面のレンダリングに関する情報

## App のライフサイクル

- with WidgetsBindingObserver
    - didChangeAppLifecycleState()
        - AppLifecycleState
            - inactive
            - paused
            - resumed
            - detached

## StatefulWidget のライフサイクル

1. createState()            -> created                      `[構築] state オブジェクトの作成`
2. initState()              -> initialized                  `[構築] Widget ツリーの初期化`
3. didChangeDependencies()  -> ready (dirty)                `[構築] state オブジェクトの依存関係が変更された時に呼ばれる`
4. /                        -> ready (clean)
    1. didUpdateWidget()                                    `[描画] Widget の構築が変更された時に呼ばれる`
    2. build()                                              `[描画] Widget で作られる画面を構築`
    3. setState()                                           `[描画] 状態が変わったことを通知する`
5. deactivate()
6. dispose()                -> defunct

## Localization

- AppLocalizations

## BuildContext

- context:
    - Widget が自分の置かれている状況を認識できるように、親の Element への参照を持っている
    - 参照先から子要素まで辿れる
- of メソッド:
    - 親要素に向かって辿る
    - 自分 (子要素) に親要素でどのような設定が行われているか知りたい場合

## Design Pattern

- Stream
    - ```
      var intStream = StreamController<Int>();
      var stringStream = StreamController<String>.broadcast();
      ```
- Provider

---

# Package
- 管理
  - `flutter pub add ____`
  - `flutter pub add --dev ____`
  - `flutter pub get`
  - `flutter pub outdated`
  - `flutter pub upgrade ____`

- `dart:`
  - ui/
    - `Locale`
  - io/
    - `Platform`                                                    [Platform] version や OS の種類を取得できる
  - `async`
  - `isolate`                                                       [Thread] 別スレッドの起動、連携、停止
- `package:`                                                        Flutter/Dart の Build System (pub) が `pubspec.yaml` の内容をもとに解決
  - flutter/
    - foundation.dart                                             Flutter SDK の一部で、フレームワークの基本機能や共通ユーティリティを提供する
      - `compute`                                                   [Thread] スレッドを非同期関数のように扱える
    - material.dart
      - `MediaQuery`                                                [Platform] 画面サイズ・文字のスケーリング・向き・デバイス情報などにアクセス
  - flutter_localizations/
    - `flutter_localizations.dart`                                  [L10N]
  - intl/
    - `intl.dart`                                                   [Date] Date
  - shared_preferences/shared_preferences.dart/
    - `SharedPreferences`                                           [Storage] Flutter アプリで簡単なデータ（キー・バリュー形式）を端末に永続的に保存する
  - package_info/package_info.dart/
    - `PackageInfo`                                                 [pubspec] `await PackageInfo.fromPlatform();` で `pubspec.yaml` の情報を取得できる
  - device_info_plus/device_info_plus.dart/
    - `AndroidDeviceInfo`                                           [Platform] 端末のモデル、OSバージョン、メーカー名、ハードウェア構成など
    - `IosDeviceInfo`                                               [Platform] 端末のモデル、OSバージョン、メーカー名、ハードウェア構成など
    - `DeviceInfoPlugin`                                            [Platform] OS・端末情報の取得（デバッグ・クラッシュ対応などに有用）
  - flutter_device_locale/flutter_device_locale.dart/
    - `DeviceLocale`
  - permission_handler/permission_handler.dart/
    - `PermissionStatus`                                            [Platform] 状態表す Enum
    - `Permission`                                                  [Platform] request など
  - `flutter`/
    - `foundation.dart`                                             Flutter SDK の一部で、フレームワークの基本機能や共通ユーティリティを提供する
  - package_info/package_info.dart/`PackageInfo`                    `await PackageInfo.fromPlatform();` で `pubspec.yaml` の情報を取得できる
  - device_info_plus/device_info_plus.dart/`AndroidDeviceInfo`      端末のモデル、OSバージョン、メーカー名、ハードウェア構成など
  - device_info_plus/device_info_plus.dart/`IosDeviceInfo`          端末のモデル、OSバージョン、メーカー名、ハードウェア構成など
  - device_info_plus/device_info_plus.dart/`DeviceInfoPlugin`       OS・端末情報の取得（デバッグ・クラッシュ対応などに有用）
  - flutter_device_locale/flutter_device_locale.dart/`DeviceLocale`
  - shared_preferences/shared_preferences.dart/`SharedPreferences`  Flutter アプリで簡単なデータ（キー・バリュー形式）を端末に永続的に保存する
  - `rxdart`/
  - rxdart/`BehaviorSubject`                                        ValueStream を実装
    - `final subject = BehaviorSubject<int>.seeded(0); // 初期値 0`
    - `subject.listen((value) {`
    - `  print("Listener1: $value");`
    - `});`
    - `subject.add(1);`
    - `subject.add(2);`
    - `// 新しい購読者は最新値 (2) をすぐ受け取る`
    - `subject.listen((value) {`
    - `  print("Listener2: $value");`
    - `});`
        - `Listener1: 0`
        - `Listener1: 1`
        - `Listener1: 2`
        - `Listener2: 2`  // 直近の値がすぐ送られる
    - listen() で返ってくるオブジェクトは `StreamSubscription`
