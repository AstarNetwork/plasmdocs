# スマートコントラクトを書く

### コントラクトをコンパイルする

```text
cargo +nightly contract build
```

すると、以下のようなログが表示されます：

![](https://gblobscdn.gitbook.com/assets%2F-M8GVK5H7hOsGnYqg-7q%2F-MAJMytj7yrGxuY0iIFv%2F-MAJVi-aGz2v6IeHrvAm%2F%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88%202020-06-21%2010.33.23.png?alt=media&token=c20d1758-ffcb-446c-b48d-fe91b9d2a219)

After compiling, you can find the `target` folder which contains this `wasm` file on your directory.

コンパイル後、あなたのディレクトリに、この `wasm` ファイルを含んだ`target`  フォルダが見つかります

![](https://gblobscdn.gitbook.com/assets%2F-M8GVK5H7hOsGnYqg-7q%2F-MAJMytj7yrGxuY0iIFv%2F-MAJW-rbcxk2Dl6YNTiN%2F%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88%202020-06-21%2010.34.43.png?alt=media&token=8d881161-06f0-408f-b8f6-f5a89dbc8405)

### メタデータを作成する

以下のコマンドでコントラクトのメタデータを作成することができます。

```text
cargo +nightly contract generate-metadata
```

wasmバイナリと同様に`target`ディレクトリ内に`metadata.json`が作成されます。

