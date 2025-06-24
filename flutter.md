# Flutter

## Dart

- NullSafety
    - Nullable 型:
        - `型名?` (etc. String? hoge; や int? fuga; など)
    - Null-aware 演算子:
        - `?.` 演算子 (Swift と一緒)
        - `??` 演算子 (Swift と一緒)
        - `??=` 演算子 (変数が null でないなら値を変えず、null なら右辺値を使う)
    - `!` 強制アンラップ (Swift と一緒)
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

## Folder Tree

## Library

- `dart:`
  - `ui`/
    - `Locale`
  - `io`/
    - `Platform`                                                    [Platform] version や OS の種類を取得できる
- `package:`                                                        Flutter/Dart の Build System (pub) が `pubspec.yaml` の内容をもとに解決
  - shared_preferences/shared_preferences.dart/
    - `SharedPreferences`                                           [Storage] Flutter アプリで簡単なデータ（キー・バリュー形式）を端末に永続的に保存する
  - flutter/
    - foundation.dart                                             Flutter SDK の一部で、フレームワークの基本機能や共通ユーティリティを提供する
    - material.dart
      - `MediaQuery`                                                [Platform] 画面サイズ・文字のスケーリング・向き・デバイス情報などにアクセス
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

## Class

- 定数コンストラクタ
    - `abstract class AppSessionStatus {`
    - `  const AppSessionStatus();`
    - `}`
    - コンパイル時にインスタンスを生成できる コンストラクタ
    - そのクラスのインスタンスが「不変（immutable）」であることを前提にしていて、再利用される
    - メモリ効率が良く、Flutter では UI 表示でよく使われる（const Text(...) など）
