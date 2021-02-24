# コントラクトをcallする

## スマートコントラクトメッセージ

スマートコントラクトとのコミュニケーションには "messages"を使用しています。

![](../../../.gitbook/assets/messages.png)

2種類のmessagesを渡すことができます：

* スマートコントラクトの状態を変更するメッセージはトランザクションとして送信されます。
* スマートコントラクトの状態を変更しないメッセージはRPCコールを使って呼び出すことができます。

スマートコントラクトの値を`get()` メッセージコールで読み取ってみましょう。

![This smart contract was deployed with enabled state flag.](../../../.gitbook/assets/get_interaction.png)

次に、スマートコントラクトの真偽値を反転させる `flip()` メッセージを送信して、スマートコントラクトの状態を変更してみましょう。

![Flip call is a transaction.](../../../.gitbook/assets/flip.png)

![New contract flag value reached.](../../../.gitbook/assets/get_new.png)

この2種類のメッセージを使用して、DAppは簡単にスマートコントラクトデータを書き込んだり、読み込んだりすることができます。楽しんでください。

