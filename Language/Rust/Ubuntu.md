# 環境

Ubuntu及びArchLinuxにRustの環境を構築します.

たぶん他のディストロでも同じような方法でインストールできます.



# 方法

Rustのインストール方法は主に2つ存在します

## その1. 公式インストールスクリプトによるインストール (オススメ)

1. 依存関係のパッケージをインストール

- Ubuntu
    ```sh
    sudo apt install -y build-essential curl make gcc
    ```

- ArchLinux
    ```sh
    sudo pacman -S base-devel curl make gcc
    ```


2. ターミナルアプリで以下のコマンドを実行
    ```sh
    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
    ```

3. システムの再起動

> [!WARNING]
> 再起動しないとパスが通らない可能性があります


## その2. パッケージマネージャーによるインストール (ArchLinux Only)

pacmanのリポジトリにRustupが存在するのでパッケージマネージャー経由でのインストールも可能です.

パスは勝手に通ります.

1. Rustupのインストール
    ```sh
    sudo pacman -S rustup
    ```

2. ツールチェインのインストール
    ```sh
    rustup default stable
    ```


# インストール後の作業

## パスの確認
```sh
rustc --version
cargo --version
```

バージョンが表示されたらパスは通ってます

## (オプション) ネイティブCPUに最適化

`~/.cargo/config`ファイルにフラグを追加しましょう. これで自分のパソコンに最適化されたソフトウェアをビルドできます

```config
[target.x86_64-unknown-linux-gnu]
rustflags = ["-C", "target-cpu=native"]
```

> [!WARNING]
> クロスコンパイル時にはこの設定は無視されます. もしも他のコンピューターへバイナリを渡す際には注意してください.

## ツールをインストール

### rust-analyzer
> [!TIP]
> このツールはIDEやエディタによっては別途でインストールされる場合があるので、飛ばしても多分大丈夫です.

Rust用の[言語サーバー](https://en.wikipedia.org/wiki/Language_Server_Protocol)です. VimやEmacsのような~~互いに争っていたらVSCodeにシェアを漁夫られた~~古いエディタを使っている場合はインストール必須です.


### Rustfmt
ソースコードを整形してくれるフォーマッタです.
```sh
rustup component add rustfmt
```

# Rustを書くのに便利なツール


## __Visual Studio Code__
言わずとしれた超有名最強最高なエディタです. もうこいつ一人で良くないですか...?


Rust用の拡張機能があります. 拡張機能に含まれるものは以下の通り
- rust-analyzer
- rust-sytax
- crates


### インストール
1. 拡張機能画面から`Rust`で検索

2. `1YiB`というユーザーが作成した`rust`拡張機能バンドルをインストール


## __JetBrains RustRover__
最近出てきたRust用の統合開発環境です. 機能豊富で学生のうちなら無料で使用可能です.
Windows, macOS, Linuxで使用可能です.

### インストール

- Ubuntu
    1. 公式サイトから`.deb`ファイルをダウンロード or flatpakでインストール

        [JetBrains toolbox / Download the App](https://www.jetbrains.com/ja-jp/lp/toolbox/)

    2. `JetBrains Tool Box`にログインしてインストール

- ArchLinux
    1. AURから`JetBrains Tool Box`をインストール
        ```sh
        yay -S jetbrains-toolbox
        ```

    2. `JetBrains Tool Box`にログインしてインストール

### 設定
後々記述...

## __JetBrains Fleet Editor__
同じくJetBrainsから出ているテキストエディタ. まだbeta版ですが, 色々と新鮮なので使ってみるのもありかも.

### インストール
`Rust Rover`のインストールとほぼ一緒

### 設定
後々記述...

## __mold__

マルチコアCPUに特化した爆速リンゲージエディタ（リンカ）です. 短時間でビルドできるようになります.

### インストール
- Ubuntu
    ```sh
    sudo apt install -y mold
    ```
- ArchLinux
    ```sh
    sudo pacman -S mold
    ```

### 設定
グローバル設定（どのプロジェクトでも利用する）

- `~/.cargo/config`ファイルに以下の項目を追加

```sh
[target.ARCHITECTURE]
linker = "clang"
rustflags = ["-C", "link-arg=-fuse-ld=mold"]
```


## __sccache__
コンパイル生成物をキャッシュして次回のビルド時にコンパイル時間を短縮できます.

### インストール
- Ubuntu
    ```sh
    sudo apt install -y sccache
    ```

- ArchLinux
    ```sh
    sudo pacman -S sccache
    ```

### 設定

- 一時的に利用したい場合
    - `RUST_WRAPPER`環境変数を設定する
    ```sh
    RUSTC_WRAPPER=sccache cargo build
    ```

- 永続的に利用したい場合
    - `~/.cargo/config`ファイルに以下の項目を追加
    ```sh
    [build]
    rustc-wrapper="sccache"
    ```


# 参考資料
[Rust（プログラミング言語） - Wikipedia](https://ja.wikipedia.org/wiki/Rust_(%E3%83%97%E3%83%AD%E3%82%B0%E3%83%A9%E3%83%9F%E3%83%B3%E3%82%B0%E8%A8%80%E8%AA%9E))

[rust-lang.org / JP（公式サイト）](https://www.rust-lang.org/ja)

[Rust - ArchLinux Wiki](https://wiki.archlinux.jp/index.php/Rust)