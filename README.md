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

日本語化

```bash
flutter pub add flutter_localizations --sdk=flutter
```
