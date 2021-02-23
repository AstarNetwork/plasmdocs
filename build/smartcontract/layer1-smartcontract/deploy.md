# デプロイ

[Plasm Network](https://www.plasmnet.io/)のメインネットにデプロイする前に、自身のローカルチェーンとDusty Networkにデプロイすることを推奨します。これは安全な開発を行なうためであり、ローカル環境とDusty Network上でテストを行なうことでデプロイするスマートコントラクトの動作を確認することができます。

### Development Network

ローカルチェーンでスマートコントラクトを試してみましょう。Plasm Network Portal UIを開いてください。

{% embed url="https://apps.plasmnet.io" %}

まず、左上のチェーン選択のセクションで、**Local Node** を選択してください。

![](../../../.gitbook/assets/select_local.png)

**Contracts** タブをクリックして、 **Code** -&gt; **Upload WASM** を選択してください

![](../../../.gitbook/assets/upload.png)

Metadata と WASM コードは、フォームに記入する必要があります。

![](../../../.gitbook/assets/filled_form.png)

コードのアップロードには約220ユニットが必要です。

![](../../../.gitbook/assets/uploaded.png)

Congratulations! 最初のレイヤー1コントラクトをアップロードしました！ "**Deploy"** ボタンから、最初のインスタンスをつくりましょう。

![Don&apos;t foget to set 100 unit endowment.](../../../.gitbook/assets/deploy.png)

取引手数料は1.6ユニット程度です。その結果、スマートコントラクトのインスタンスを見ることができます。

![](../../../.gitbook/assets/instance_000.png)

コントラクトとのやり取りについては次のチャプターで説明します。



