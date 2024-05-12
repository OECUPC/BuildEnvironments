# はじめに

LinuxにGo言語の開発環境を用意します

# Goって何?

- 2009年11月10日にGoogleが発表したプログラミング言語です
- Robert Griesemer、ロブ・パイク、ケン・トンプソンによって開発されました
    - ケン・トンプソンはオリジナルのUNIXを開発した一人です. ~~この年でもプログラマーなのやばすぎる~~
- Pythonのような書きやすさ, Javaのような巨大なシステムでも動作する堅牢さ, C言語ライクの馴染みやすさが魅力です
    - 特に __並行処理__ のプログラムが書きやすいです。*並列じゃないよ！！！*

## C言語との違い
- ネットワークを使ったプログラムが書きやすい
- ポインタ演算がなくてメモリ安全
    - ポインタ自体はバリバリ使う
    - 低レイヤーはｷﾋﾞｼｲ
- クロスコンパイル簡単
- ガベージコレクションがある(不必要なメモリを自動的に解放してくれる)
- 標準ツールが超優秀（Rustとの共通点）

# インストール
## 公式ダウンロードページから

1. `https://go.dev/dl/`にアクセス
2. 次のどちらかをインストール
    - M1チップ搭載のMac: `go<任意のバージョン>.darwin-arm64.pkg`をクリック
    - intel CPU搭載のMac: `go1.22.3.darwin-amd64.pkg`をクリック

> [!WARNING]
> arm64とamd64は別物です. めちゃくちゃ間違いやすいので注意

3. インストーラーの指示に従ってインストール





# VSCodeの設定

## 1. 拡張機能のインストール

1. `Ctrl + Shift + x`で拡張機能のメニューを開き, 検索窓に`Go`と入力
2. __*Go/Go Team at Google*__ をインストール
3. `Ctrl + Shift + p`でコマンドパレットを開き, `Go:Install/Update Tools`と入力する
4. 幾つかのツールが表示されるが全て選択してインストール

## 2. デバッガを使用中でも標準入力を受け取る
Goのデバッガ`delve`は通常だと標準入力のあるプログラムをうまく実行できない（~~まじで何でなんだよ~~）

`launch.json`に`"console": "integratedTerminal"`を追加することで対処可能

### .vscode/launch.jsonの一例
```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Launch",
            "type": "go",
            "request": "launch",
            "mode": "debug",
            "program": "${fileDirname}",
            "console": "integratedTerminal",
            "env": {},
            "args": []
        }
    ]
}
```


# 参考文献

- [とりあえずWikipedia見ればなんとなくわかるので、ほれ](https://ja.wikipedia.org/wiki/Go_(%E3%83%97%E3%83%AD%E3%82%B0%E3%83%A9%E3%83%9F%E3%83%B3%E3%82%B0%E8%A8%80%E8%AA%9E))
- [Goの公式インストールサイト](https://go.dev/doc/install)