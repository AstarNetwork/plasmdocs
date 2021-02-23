# 書くold

![](../.gitbook/assets/undraw_dev_focus_b9xo-1-.png)

[Plasm Network](https://www.plasmnet.io/)はレイヤー2ソリューションをサポートしているレイヤー1ブロックチェーンです。このセクションではレイヤー1上にどのようにスマートコントラクトを書くのかを説明します。

### イントロダクション

Plasm NetworkはWebAssemblyをサポートしているので、WebAssemblyに対応している全ての言語（Go、Rust、C など）に対応することができます。現在サポートされているのはRustベースのeDSLである ink! とEthereumの開発で使用されるSolidity です。このセクションではink!を使ったスマートコントラクトの書き方について説明します。

### Substrateの環境構築

まずはじめに、Substrateの環境構築を行う必要があります。MacOSかLinuxディストリビューションのいずれかを使用している方は以下のコマンドでセットアップを行ってください。

```text
curl https://getsubstrate.io -sSf | bash -s -- --fast

rustup target add wasm32-unknown-unknown --toolchain stable
rustup component add rust-src --toolchain nightly
```

Windowsを利用している方は以下のページよりセットアップ方法を確認してください。

{% embed url="https://substrate.dev/docs/en/knowledgebase/getting-started/windows-users" %}

### ink! の環境構築

ink!でコントラクトを開発を行うためのセットアップを行います。

以下のコマンドでink!のコマンドラインツールをインストールすることができます。

```text
cargo install cargo-contract --vers 0.6.1 --force
```

`cargo contract --help` でコマンドの詳細を確認することができます。

### プロジェクトディレクトリを作成する

新しく開発用のディレクトリを作成します。以下のコマンドで作成可能です。

```text
cargo contract new <name>
```

 ここで、`<name>`には作成するプロジェクト名\(ディレクトリ名\)を指定します。このコマンドにより、カレントディレクトリに新たなディレクトリ `<name>` が作成されます。`<name>`内にはコントラクトの雛形が格納されています。

公式チュートリアルにならって、ここではflipperというコントラクトを作成してみましょう。

```text
cargo contract new flipper
```

これにより`flipper`というディレクトリが作成されていることが確認できるかと思います。

### コントラクトをコンパイルする

以下のコマンドにより、ink!で記述されたコントラクトをwasmバイナリに変換することができます。

```text
cargo +nightly contract build
```

試しに、flipperをコンパイルしてみましょう。`target`ディレクトリに`fliipper.wasm`が生成されたことが確認できます。

### メタデータを作成する

以下のコマンドでコントラクトのメタデータを作成することができます。

```text
cargo +nightly contract generate-metadata
```

wasmバイナリと同様に`target`ディレクトリ内に`metadata.json`が作成されます。

