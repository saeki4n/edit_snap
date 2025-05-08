# edit_snap

flutter練習

## 初期セットアップ

プロジェクト用のフォルダを作成する。
次の条件のフォルダを作成する。

```txt
Dart パッケージ名のルール（要約）
すべて小文字 (lowercase)

単語はアンダースコア _ で区切る

英数字とアンダースコアのみ使用可能 ([a-z0-9_])

数字で始めてはいけない

予約語（if、forなど）を使ってはいけない
```

パターン1

Android Studioの New Flutter Project で作成する。

パターン2

次のコマンドで作成する

```bash
flutter create test_flutter
```

参考：
<https://codelabs.developers.google.com/codelabs/flutter-codelab-first?hl=ja#2>

実行コマンドをテスト実行を行なう。
次のコマンドは chrome(Web)にテスト実行を行なう。

```bash
flutter run -d chrome
```

### アプリを日本語化する

パッケージを導入する。

```bash
flutter pub add flutter_localizations --sdk=flutter
flutter pub add intl:any
```

コードジェネレーターを設定する

pubspec.yaml にgenerateを有効にする。

```yml
flutter:
  generate: true
```

生成されたコードプロジェクトから参照するように以下のコマンドを実行する

```bash
flutter pub get
```

ローカライズ構成ファイルを作成する

./l10n.yaml ファイルを作成して、次のように記入する。

```yml
template-arb-file: app_ja.arb
output-class: L10n
nullable-getter: false
```

arbファイルを作成する

/lib/l10n/app_ja.arb

```json
{
    "startScreenTitle": "Edit Snap",
    "helloWorldOn": "こんにちは！\n今日は{date}です",
    "@helloWorldOn": {
        "placeholders":{
            "date":{
                "type":"DateTime",
                "format":"MEd"
            }
        }
    },
    "start":"開始する"
}
```

作成できたら次のコマンドでコードジェネレーターを実行すると、.dart_tool/flutter_gen/gen_l10n にファイルが出力される。

```bash
flutter gen-l10n
```

ローカライズされたメッセージを適用する

main.dart は次のように追加する。

```dart
import 'package:edit_snap/start_screen.dart';
import 'package:flutter/material.dart';
import 'package:flutter_gen/gen_l10n/app_localizations.dart';  // 追加

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      localizationsDelegates: L10n.localizationsDelegates,　    // 追加
      supportedLocales: L10n.supportedLocales,　　              // 追加
      // Android のタスクマネージャーに表示されるアプリ名
      // iOSでは使用されない
      title: 'Edit Snap',
      theme: ThemeData(
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.teal),
        useMaterial3: true,
      ),
      home: StartScreen(),
    );
  }
}
```

iOSの場合、App Storeでの表示言語を設定します。

ios/Runner/Info.plit に次を書き加える。

```xml
 <key>CFBundleLocalizations</key>
 <array>
  <string>ja</string>
 </array>
```

Androidの場合の表示言語表示設定は次のサイトを参照

[Flutter] アプリアイコン下のアプリ名のローカライゼーション
<https://zenn.dev/chimay_white/articles/a2fafa63fed9a6>
