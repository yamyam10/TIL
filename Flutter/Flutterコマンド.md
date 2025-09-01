# Flutter コマンド一覧まとめ

## Flutter 環境セットアップ

### $ flutter precache

Flutter の SDK 内部では必要なデータを Google のインフラサーバーから必要なタイミングでダウンロードしていますが、それを意図的に行うためのコマンドです。普通のユーザは基本的に利用する必要がありません。

### $ flutter doctor

インストールバージョンやインストールされてないものが無いかなど、Flutter 環境診断をしてくれます。
Flutter 実行出来なくなったなど、困ったらまずこれをやってみると良いです。

さらに`-v`オプションをつける事で詳細情報を確認できます。

```
$ flutter doctor -v
```

### $ flutter --version

現在の SDK バージョンを確認するときに利用します。`flutter doctor`は時間が少しかかるので、バージョンだけ調べたいときはこれを使います。

```
$ flutter --version
Flutter 1.23.0-4.0.pre • channel dev • https://github.com/flutter/flutter
Framework • revision 83dd176777 (12 days ago) • 2020-09-22 12:04:44 -0700
Engine • revision 2abe69c608
Tools • Dart 2.10.0 (build 2.10.0-136.0.dev)
```

### $ flutter upgrade

現在のチャンネルの新しいバージョンにアップデートする時に利用します。

### $ flutter downgrade

現在のチャンネルの一つ前のバージョンにダウングレードする時に利用します。

```
$ flutter downgrade
Downgrade flutter to version 1.22.0-12.0.pre
? [y|n]: y
```

### $ flutter channel

現在利用している Flutter SDK のチャンネルを確認します。

```shell:
$ flutter channel
Flutter channels:
* master
  dev
  beta
  stable
```

チャンネルには以下があります。

| チャンネル名 | 内容                                                                                                                 |
| ------------ | -------------------------------------------------------------------------------------------------------------------- |
| master       | github のマスターブランチ。不安定な可能性がありますが、最新を使う場合はこれ                                          |
| dev          | master に対して自動テスト等をパスした一定品質が担保されているもの (α 版相当, Windows/macOS/Linux 版はここに含まれる) |
| beta         | ベータ版機能が有効になったもの。例えば Web プラットフォームなど                                                      |
| stable       | 正式リリースのステーブル版。普通の開発者はこれを利用                                                                 |

### $ flutter channel チャンネル名

オプションで指定したチャンネルに変更されます。

```shell:例.betaチャンネルに切り替え
$ flutter channel beta
```

### $ flutter devices

Flutter アプリとして実行可能なデバイス一覧を確認できます。
Android/iOS エミュレータの場合は、事前に立ち上げた状態でなければ表示されません。

```
$ flutter devices
2 connected devices:

Android SDK built for x86 • emulator-5554 • android-x86 • Android 10 (API 29) (emulator)
macOS                     • macOS         • darwin-x64  • Mac OS X 10.15.3 19D76
```

### $ flutter config

`~/.flutter_settings`に設定ファイルがあり、これを更新するコマンドです。ファイルを直接編集も可能です。
一度設定したらその後はほぼ触る事が無いと思いますが。
※Windows/Linux/macOS を有効にしておくと、新規プロジェクト作成時にそれら向けのディレクトリが作成されます。

```shell:Flutter-Webを有効化
$ flutter config --enable-web
```

```shell:Flutter-Desktop-Linuxを有効化
$ flutter config --enable-linux-desktop
```

```shell:Flutter-Desktop-macOSを有効化
$ flutter config --enable-macos-desktop
```

```shell:Flutter-Desktop-Windowsを有効化
$ flutter config --enable-windows-desktop
```

# プロジェクト作成

### $ flutter create

Flutter プロジェクト新規作成時に利用します。大体以下で足りるかと思います。
オプションの最後に出力先のディレクトリ名を指定します。

| オプション             | 内容                                                                                              |
| ---------------------- | ------------------------------------------------------------------------------------------------- |
| -t, --template=<type>  | app, module, package, plugin のいずれかを指定。デフォルトは app                                   |
| --org                  | オーガナイゼーションを指定。デフォルトは com.example                                              |
| --project-name         | Flutter プロジェクト名を指定                                                                      |
| -i, --ios-language     | iOS 向けプラットフォーム側のコードの言語で objc, swift のいずれかを指定。デフォルトは swift       |
| -a, --android-language | Android 向けプラットフォーム側のコードの言語で java, kotlin のいずれかを指定。デフォルトは kotlin |
| --description          | プロジェクト説明文。デフォルトは"A new Flutter project."                                          |

```shell:
$ flutter create -t app --org com.hoge --project-name ¥
                 example -i swift -a kotlin ¥
                 --description "Example Flutter project." ¥
                 ./example_app
```

また、一度プロジェクトを作成後、そのプロジェクトディレクトリで`$flutter create .`を実行する事で、現在有効なプラットフォーム`andoid/, linux/など`、足りていないのテンプレートだけ生成してくれるようです。

### $ flutter clean

ビルド時に生成されるファイル群のクリーン (削除) 時に利用します。
build と.dart_tool ディレクトリを削除してくれます。

# プラグイン

### $ flutter pub get

pubspec.yaml を更新したら実行するやつです。プラグインのライブラリなどを取得したり更新します。

### $ flutter pub deps

ライブラリの依存関係をツリーで表示してくれます。

# ビルド

### $ flutter build xxx

ターゲット環境 (xxx) を指定してビルドだけ行います。成果物は./build/xxx 以下に生成されます。デフォルトはリリースモードでのビルドになります。

| オプション    | 内容                                                                                                      |
| ------------- | --------------------------------------------------------------------------------------------------------- |
| aar           | Android ARchive ファイル                                                                                  |
| ~~aot~~       | Dart コードの AOT ビルド(マシン語)。いつの間にか削除された様子です。                                      |
| apk           | Android APK ファイル                                                                                      |
| appbundle     | Android App Bundle ファイル                                                                               |
| bundle        | Flutter のフォントや画像等のバンドルのビルド(flutter_assets ディレクトリ以下, Dart の JIT 用バイトコード) |
| iso           | iOS 向けビルド                                                                                            |
| ios-framework | .framework 向けビルド                                                                                     |
| web           | Web アプリ向け                                                                                            |
| macos         | macOS デスクトップ向け(デフォルトはリリースモードでのビルド)                                              |
| linux         | Linux デスクトップ向け(デフォルトはリリースモードでのビルド)                                              |
| windows       | Windows デスクトップ向け(デフォルトはリリースモードでのビルド)                                            |

#### --target-platform オプション

以下のように、ターゲットアーキテクチャを指定してビルドすることが可能です。

```shell:
$ flutter build apk --target-platform=android-arm64
```

# アプリ実行

`flutter run`コマンドを利用することでビルドからインストール、実行まですべて行ってくれます。

### $ flutter run

プロジェクトのディレクトリ直下で実行すると devices に見えているターゲット (Android/iOS 優先） 向けに pub get やビルト、インストールまで一連の作業を実行してくれます。

### $ flutter run --release

リリースモードで実行します。

### $ flutter run --debug

デバッグモードで実行します。

### $ flutter run -d xxx

ターゲットデバイスを指定する場合には-d オプションを利用します。flutter devices で表示されているデバイスの ID を指定します。

```shell:macOSで実行する例
$ flutter run -d macOS
```

### $ flutter run --no-build

既にビルド済みであれば、再ビルドなしでアプリを実行します。

### $ flutter run --verbose

flutter run コマンド実行中の詳細ログを表示します。

# インストール

### $ flutter install

ビルド済みのインストールパッケージをデバイスにインストールします。

# テスト

### $ flutter test

プロジェクト直下の test ディレクトリのユニットテストを実行します。

### $ flutter drive

Flutter アプリのインテグレーションテスト実行コマンドです。

```shell:実行例
$ flutter drive --target=test_driver/sample_perf.dart
```

# その他

### $ flutter screenshot

現在接続しているデバイスのスクリーンショットを取得します。
出力先を指定する場合は、--out オプション (ファイル名も指定必要) を利用します。

### $ flutter --help

ヘルプメッセージを表示します。Flutter コマンドの良いところは、以下のように必要なオプションの後に`--help`を付けるとそのオプションに対するヘルプを表示してくれる点です。

```shell:実行例
$ flutter --help
$ flutter run --help
```
