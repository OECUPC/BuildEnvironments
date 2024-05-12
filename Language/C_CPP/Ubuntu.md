# はじめに

LinuxディストリビューションにC/C++の開発環境を構築します.

# 依存関係のインストール
- Ubuntu (dpkg/apt)
    ```bash
    sudo apt install -y build-essential clang gdb lldb cmake ccache
    ```
- Fedora (rpm/dnf)
    ```bash
    sudo dnf install kernel-devel clang gdb lldb cmake ccache
    ```
- ArchLinux (pacman)
    ```bash
    sudo pacman -S base-devel clang gdb lldb  cmake ccache
    ```

## 各パッケージの紹介

### __build-essential, kernel-devel, base-devel__
- Linuxカーネルをコンパイルするのに必要なメタパッケージ
- LinuxカーネルはC言語で書かれているので、これを入れとけばgccやmakeなどのc言語をコンパイルする環境が整う

### __clang__
- コンパイラ基盤にLLVMを採用しているC/C++用コンパイラ
- macOSやFreeBSDの標準コンパイラとして採用されている
- gccとは幾つか仕様が異なるが、使用感はだいたい一緒

### __gdb__
- GNU製のデバッガ
- ブレークポイントを設定してメモリの中身を覗くときによく使う

### __lldb__
- gdbに似たデバッガ
- 使い方もgdbに似てる

### __cmake__
- プログラムのビルドを自動化するためのソフトウェア

### __ccache__
- 一度生成したオブジェクトファイルをキャッシュ（ストレージのどこかに保存すること）して次回のビルドを高速にするアプリケーション

# 設定と確認
- 各ツールのバージョン確認
    ```sh
    gcc --version
    g++ --version
    gdb --version
    clang --version
    clang++ --version
    lldb --version
    cmake --version
    ```

- CやC++のコードを書く
    ```C++
    #include<iostream>

    int main(){
        int a,b
        std::cin>>a>>b;
        int ans = a * 2 + (1 - b) / 2;
        std::cout<<ans<<std::endl;
        return 0;
    }
    ```

- コンパイルする
    ```sh
    # gcc(g++)でコンパイルする場合
    g++ main.cpp -o a.out
    # clangでコンパイルする場合
    clang++ main.cpp -o a.out
    ```

- そのまま実行してみる

    ```sh
    ./a.out
    ```

- デバッガを通して実行する
    ```sh
    # gdb
    gdb a.out
    # lldb
    lldb a.out
    ```

# 便利なツール

## Visual Studio Code
- __特にこだわり無ければこれ使っててOK.__
- UbuntuやFedoraは公式サイトにパッケージで配布されている
- ArchLinuxはAURにバイナリがある（pacmanリポジトリにある`code`はcode-ossなので別物）
    - `code-oss`: vscodeからmicrosoftのトラッカーや同期機能, 拡張機能のリポジトリが異なるオープンソース版
    ```sh
    yay -S visual-studio-code-bin
    ```
- C/C++のプロジェクト内で`.vscode/launch.json`と`.vscode/tasks.json`を設定すればF5キーでビルド＆デバッグが行える

### launch.jsonの一例
```json
{
    // IntelliSense を使用して利用可能な属性を学べます。
    // 既存の属性の説明をホバーして表示します。
    // 詳細情報は次を確認してください: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "type": "lldb",
            "request": "launch",
            "name": "lldb Debug",
            "program": "${workspaceFolder}/a.out",
            "args": [],
            "cwd": "${workspaceFolder}",
            "preLaunchTask": "gcc compile"
        }
    ]
}
```


### tasks.jsonの一例
```json
{
    "tasks": [
        {
            "type": "cppbuild",
            "label": "gpp compile",
            "command": "/usr/bin/g++",
            "args": [
                "-std=gnu++17",
                "-fdiagnostics-color=always",
                "-g",
                "${file}",
                "-o",
                "${workspaceFolder}/a.out"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "detail": "デバッガーによって生成されたタスク。"
        },
        {
            "type": "cppbuild",
            "label": "clang++ compile",
            "command": "/usr/bin/clang++",
            "args": [
                "-std=gnu++17",
                "-fdiagnostics-color=always",
                "-g",
                "${file}",
                "-o",
                "${workspaceFolder}/a.out"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "detail": "デバッガーによって生成されたタスク。"
        },
        {
            "type": "cppbuild",
            "label": "gcc compile",
            "command": "/usr/bin/gcc",
            "args": [
                "-std=gnu17",
                "-fdiagnostics-color=always",
                "-g",
                "${file}",
                "-o",
                "${workspaceFolder}/a.out"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "detail": "デバッガーによって生成されたタスク。"
        }
    ],
    "version": "2.0.0"
}
```



## JetBrains CLion
- プロ仕様の本格派IDE
- 機能が豊富で使いこなすことができれば超優秀なIDE
- 学生は無料で使えるので是非使ってみてはどうだろうか



# 小ネタ

- パッケージマネージャーでツールをインストールした時点で勝手にPATHは通る. 自分の環境のPATHを確認したいときは
`echo $PATH`で見れる

- ログインシェルの設定ファイル（bashなら`.bashrc`. zshなら`.zshrc`）にPATHを書けば永続的に設定できる

# 参考資料

- WSLの環境構築はこちらを参照するといい
[Visual Studio Codeで競プロ環境構築(導入編) / Qiita](https://qiita.com/AokabiC/items/e9312856f588dd9303ed)

