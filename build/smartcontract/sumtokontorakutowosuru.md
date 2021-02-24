# スマートコントラクトを確認する

最初のステップは、デプロイされたコントラクトの正しいPlasmアドレスを抽出することです。正しいコントラクトアドレスは以下のようになります。

![Contract address deployed on Dusty network.](../../.gitbook/assets/hackathon01.png)

アドレスはアルファベット順になっており、 [Address Book](https://apps.plasmnet.io/#/addresses)に正しくインポートされている必要があります。

{% hint style="info" %}
DustyかPlasmのポータルに接続してください
{% endhint %}

![Click &quot;Save&quot;](../../.gitbook/assets/hackathon02.png)

![The contract address has positive balance.](../../.gitbook/assets/hackathon03.png)

プラスの残高が確認できれば、コントラクトが正常にデプロイされたことを意味します。

2つ目のステップは、デプロイされたコントラクトが本当にスマートコントラクトなのかどうかを確認することです。   
この目的のために、以下のようなスマートコントラクトパレットを使用してみましょう。

![Information about alive smart contracts on chain.](../../.gitbook/assets/hackathon04.png)

`contractInfoOf` を呼び出すと、デプロイされたスマートコントラクトに関する多くの情報（codeHashやデプロイされたブロックなど）が表示されます。この情報が空でなければ、与えられたアドレスは Plasm や Dusty にデプロイされたスマートコントラクトです。

