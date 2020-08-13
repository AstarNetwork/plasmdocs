---
description: Substrateは活発な開発が行われている最中です。もし問題やエラーがありましたらDiscordグループでご連絡ください。
---

# ローカルでノードを動かす

Plasm Networkにスマートコントラクトをデプロイする前に、ローカルの環境でノードを動かしてみましょう。

まず最初にPlasm Nodeをインストールしローカル環境でテストします。

### Plasm Node <a id="plasm-node"></a>

現在、Plasm Nodeをインストールするには2つの方法があります。

**①最新のリリースからインストールする**

{% embed url="https://github.com/staketechnologies/Plasm/releases" %}

**②ソースからビルドする**

Rustがインストールされていることを確認してください。

```text
> curl https://sh.rustup.rs -sSf | sh# on Windows download and run rustup-init.exe# from https://rustup.rs instead​> rustup update nightly> rustup target add wasm32-unknown-unknown --toolchain nightly
```

また以下のディペンデンシーをインストールする必要があります。お使いの環境に合わせてインストールしてください。

* **Linux**: `sudo apt install cmake git clang libclang-dev build-essential`
* **Mac**: `brew install cmake git llvm`
* **Windows**: Download and install the Pre Build Windows binaries of LLVM from [http://releases.llvm.org/download.html](http://releases.llvm.org/download.html)​

追加のビルドツールをインストールします。

```text
cargo install --git https://github.com/alexcrichton/wasm-gc
```

Plasm NodeをGitのソースからインストールします。

```text
cargo install --force —locked  --git https://github.com/staketechnologies/Plasm --tag v1.0.0 plasm-cli
```

Plasm NetworkのR&Dチェーン（準テストネット）であるDusty Network上でノードを動かすには以下のコマンドを実行します。

```text
plasm-node
```

開発環境でノードを動かすには以下のコマンドを実行します。

```text
plasm-node --dev
```

最後にPlasm上のスマートコントラクト言語であるink!を書くためにink!をインストールします。

```text
cargo install cargo-contract --vers 0.6.1 --force
```

他のコマンドを理解するためには、"cargo contract --help" で確認できます。

もしご質問ありましたら、[Discord](https://discord.gg/kH3Njpr)にてご連絡してください。

