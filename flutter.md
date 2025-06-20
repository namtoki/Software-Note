# Flutter

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





