# 環境

macOSにGitをインストールします。

# 方法1 Xcode Command Line Toolsを使用する方法

## Xcode Command Line Tools

ターミナルで以下のコマンドを実行。

```sh
xcode-select --install
```

これでXcode Command Line Toolsの一部としてGitが使えるようになります。ただし、バージョン管理の観点から、下記の方法2も一緒に行うことをおすすめします。

# 方法2 Homebrewを用いる

## Xcode Command Line Tools

ターミナルで以下のコマンドを実行。

```sh
xcode-select --install
```

## Homebrewのインストール

ターミナルで以下のコマンドを実行します。なお、コマンドは本稿執筆時点で有効なものです。最新のものは、[このサイト](https://brew.sh/ja/:title)から確認して下さい。

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## Gitのインストール

ターミナルで以下のコマンドを実行します。

```sh
brew install git
```

# 確認

以下のコマンドを実行してGitが使用できるか確認してください。

```sh
git --version
```