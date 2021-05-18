# Ethereum SeedでAddressを作成する

これは、Plasm Networkネットワーク内で使用するために、ECDSAキー（特にEthereumウォレット）をPlasm Networkにインポートするためのガイドです。どのような Ethereum 秘密鍵でも Plasm Network 内で使用することができますが、このガイドは Etherum ロックドロップの参加者が自分のトークンにアクセスする際に最も役立つでしょう。

[Plasm Network](https://www.plasmnet.io/)はSubstrateをベースとしたブロックチェーンです。Ethereumとは基盤が異なっていますが、異なる基盤のSeedから[Plasm Network](https://www.plasmnet.io/)上でのアドレスが作成できることはユーザビリティを大きく改善します。

{% page-ref page="../../ecosystem/substrate.md" %}

{% hint style="danger" %}
**免責事項 :** Ethereumの秘密鍵が流出すると、Ethereumウォレットが危険にさらされる可能性があるので、取り扱いには注意が必要です。
{% endhint %}

## Plasm Network Portal

Ethereumウォレットを[Plasm Network](https://www.plasmnet.io/)にインポートするための最初のステップは、[Plasm Network](https://www.plasmnet.io/)ポータルにアクセスすることです。以下のIPFSリンクを使用します。

* [IPFS Link](https://ipfs.io/ipfs/QmZQBwe4DeW6aruayemGXA5ysexsqJVRzF6YHHeNPzKi7d)

> コンテンツ指向の分散ストレージとしてのIPFSは、機密性の高いコードにとって最も安全な場所です。コードを変更すると URI が変更され、このコードは利用できなくなります。

より良いパフォーマンスを得るためには、ローカルにインストールされたIPFSノードを使用することをお勧めします。また、お使いのブラウザにIPFSコンパニオンエクステンションをインストールすることをお勧めします。

* Chrome: [https://chrome.google.com/webstore/detail/ipfs-companion/nibjojkomfdiaoajekhjakgkdhaomnch](https://chrome.google.com/webstore/detail/ipfs-companion/nibjojkomfdiaoajekhjakgkdhaomnch)
* FireFox: [https://addons.mozilla.org/ru/firefox/addon/ipfs-companion/](https://addons.mozilla.org/ru/firefox/addon/ipfs-companion/)

以下のページをご覧になってみてください。



## Import Ethereum Seed

それでは、[Plasm Network](https://www.plasmnet.io/)にインポートしたいEthereumの秘密鍵を準備しましょう。ロックドロップ参加者の場合は、ロックドロップ取引を行ったウォレットの秘密鍵でなければなりません。16進数文字列でも、ニーモニックでもどちらでも構いません。

{% hint style="info" %}
[Metamask guid](https://metamask.zendesk.com/hc/en-us/articles/360015289632-How-to-Export-an-Account-Private-Key)に沿って鍵を取り出すことができます。
{% endhint %}

Ethereumウォレットからの鍵のエクスポートが完了したら、Plasm Networkにインポートする準備ができました。サイドタブから「アカウント」→「アカウントを追加」に移動します。

![](../../.gitbook/assets/sukurnshotto-2020-05-31-173619png.png)

ここで、16進数の秘密鍵やニーモニックをコピーしてシード入力欄に貼り付けます。 **ECDSA**タイプの鍵ペアと16進数を選択してください（メタマスク鍵をガイドでエクスポートする場合）。

{% hint style="info" %}
0xをhex文字列秘密鍵の先頭につけることを忘れないでください。
{% endhint %}

![](../../.gitbook/assets/sukurnshotto-2020-05-31-173905png%20%282%29%20%282%29.png)

パスワードを含む別のフィールドにアカウントを保存するように記入します。

![](../../.gitbook/assets/sukurnshotto-2020-05-31-173938png.png)

すべてがうまくいった場合は、インポートされているECDSAのタイプの新しいウォレットが表示されるはずです。さらに、ロックドロップ参加者の場合は、インポートされたアドレスにロックドロップから受け取ったPLMが含まれていることを確認する必要があります。

質問があれば、[Tech Chat](https://discord.gg/Cyjnrxv)の日本語チャネルでご質問ください。

