# Flutter

## Folder Tree

## Library

- `dart:ui`/
  - `Locale`
- `package:`                                                        Flutter/Dart の Build System (pub) が `pubspec.yaml` の内容をもとに解決
  - `flutter`/
    - `foundation.dart`                                             Flutter SDK の一部で、フレームワークの基本機能や共通ユーティリティを提供する
  - package_info/package_info.dart/`PackageInfo`                    `await PackageInfo.fromPlatform();` で `pubspec.yaml` の情報を取得できる
  - device_info_plus/device_info_plus.dart/`AndroidDeviceInfo`      端末のモデル、OSバージョン、メーカー名、ハードウェア構成など
  - device_info_plus/device_info_plus.dart/`IosDeviceInfo`          端末のモデル、OSバージョン、メーカー名、ハードウェア構成など
  - device_info_plus/device_info_plus.dart/`DeviceInfoPlugin`       OS・端末情報の取得（デバッグ・クラッシュ対応などに有用）
  - flutter_device_locale/flutter_device_locale.dart/`DeviceLocale`
  - shared_preferences/shared_preferences.dart/`SharedPreferences`  Flutter アプリで簡単なデータ（キー・バリュー形式）を端末に永続的に保存する





