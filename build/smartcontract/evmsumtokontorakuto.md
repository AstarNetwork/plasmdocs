# EVMスマートコントラクト

![](https://gblobscdn.gitbook.com/assets%2F-M8GVK5H7hOsGnYqg-7q%2F-MJzUHzpmiTdY_nPC0eJ%2F-MJzUOjDYur09w-atEHV%2Fwhat-is-ethereum-logo-big.o.png?alt=media&token=5aea9d5a-029c-4fab-96e2-750f0ffd56e0)

EVM（Ethereum Virtual Machine）は、スマートコントラクト用のVMとして最もポピュラーなものです。EVMには、開発者、テスター、ユーザーのための豊富なエコシステムがあります。Plasm Networkは、EVMベースのスマートコントラクトを**レイヤー**1コントラクトとして完全にサポートしています。

## EVMスマートコントラクトをデプロイする <a id="deploy-your-evm-smart-contract"></a>

この記事では、Plasmのローカル開発環境にスマートコントラクトを展開します。

### ノードをインストールする <a id="install-a-plasm-node"></a>

The next step is to launch a node in the development environment.

ローカル開発環境を利用するには、Plasmノードが必要です。ここから最新のPlasmノードをインストールしてください。[https://github.com/staketechnologies/Plasm/tree/dusty（ビルド手順）](https://github.com/staketechnologies/Plasm/tree/dusty（ビルド手順）。)

次に開発環境でノードを起動します。

```text
plasm-node --dev -l evm=debugOct 14 15:07:56.998  WARN Running in --dev mode, RPC CORS has been disabled.    Oct 14 15:07:56.998  INFO Plasm Node                                                                                           Oct 14 15:07:56.998  INFO ✌️  version 1.6.0-1dc78cce-x86_64-linux-gnu    Oct 14 15:07:56.998  INFO ❤️  by Stake Technologies <devops@stake.co.jp>, 2019-2020    Oct 14 15:07:56.998  INFO 📋 Chain specification: Development     Oct 14 15:07:56.998  INFO 🏷  Node name: skillful-war-1171    Oct 14 15:07:56.998  INFO 👤 Role: AUTHORITY
```

これで、メタマスクでノードが使えるようになりました。いい感じですね。

### Metamaskの接続設定

![](https://gblobscdn.gitbook.com/assets%2F-M8GVK5H7hOsGnYqg-7q%2F-MJflFO1jfrrqPijjtm4%2F-MJflbt7EI3w0dAiaS0r%2Fnetwork_connection.png?alt=media&token=4c44d98e-0383-4ca3-9dd9-a11e7dd83905)

次は開発者アカウントのシードをインポートします。

> `0x60ed0dd24087f00faea4e2b556c74ebfa2f0e705f8169733b01530ce4c619883`

開発者アカウントのシードをインポートする。

![](https://gblobscdn.gitbook.com/assets%2F-M8GVK5H7hOsGnYqg-7q%2F-MJflFO1jfrrqPijjtm4%2F-MJfmWd4NwY7QATrJEE7%2Fimport_dev_account.png?alt=media&token=44b9fff9-0e9f-4678-b3c5-e528f9e5792e)

残高を確認できます。

![](https://gblobscdn.gitbook.com/assets%2F-M8GVK5H7hOsGnYqg-7q%2F-MJflFO1jfrrqPijjtm4%2F-MJfmbC1kFpY_0YUFSqE%2Faccount_imported.png?alt=media&token=59d27dc6-bd46-46da-9cac-38f724c78429)

PLMはERC20ではありませんので、お気をつけください。

### Remixからコントラクトをデプロイする <a id="deploy-contracts-by-using-remix"></a>

アカウントの準備が整ったら、Remixからいくつかのサンプルコントラクトをデプロイしてみましょう。

Remixのデモコントラクトを使いましょう。

![](https://gblobscdn.gitbook.com/assets%2F-M8GVK5H7hOsGnYqg-7q%2F-MJflFO1jfrrqPijjtm4%2F-MJfms8YtbaFMDpjGn5M%2Fremix_demo.png?alt=media&token=9008a929-f060-4020-bf54-9f5343f1ae64)

デプロイ環境をMetamask injected web3に変更してください。

![](https://gblobscdn.gitbook.com/assets%2F-M8GVK5H7hOsGnYqg-7q%2F-MJflFO1jfrrqPijjtm4%2F-MJfmyvrcI1W9tHe5L0o%2Fchange_env.png?alt=media&token=2d1464e4-1111-43e0-a639-c5ae7c66090c)

デプロイを押して、Metamaskのトランザクションを承認してください。

![](https://gblobscdn.gitbook.com/assets%2F-M8GVK5H7hOsGnYqg-7q%2F-MJflFO1jfrrqPijjtm4%2F-MJfn5sUQgGeD_AWTUKj%2Fdeploy.png?alt=media&token=f0cc065e-760f-4868-9cc6-e804dc8f3468)

Plasmノードですべてがうまくいくと、以下のような行が表示されます。

```text
Oct 15 13:09:30.009 DEBUG apply_extrinsic: Execution Succeed(Returned) [source: 0x7ef99b0e5beb8ae42dbf126b40b87410a440a32a, value: 0, gas_limit: 320315, used_gas: 320315, actual_fee: 3523465000000000]    {ext}                                             Oct 15 13:09:30.009 DEBUG apply_extrinsic: Inserting code (938 bytes) at 0x66bb595bc60c8af0a306aa86edf96a88d3a59e9a    {ext}   Oct 15 13:09:30.009 DEBUG apply_extrinsic: Updating storage for 0x66bb595bc60c8af0a306aa86edf96a88d3a59e9a [index: 0x0000000000000000000000000000000000000000000000000000000000000000, value: 0x0000000000000000000000007ef99b0e5beb8ae42dbf126b40b87410a440a32a]    {ext}                                                                                                                   Oct 15 13:09:30.009 DEBUG apply_extrinsic: Updating storage for 0x66bb595bc60c8af0a306aa86edf96a88d3a59e9a [index: 0x0000000000000000000000000000000000000000000000000000000000000002, value: 0x000000000000000000000000000000000000000000000000000000000000000a]    {ext}Oct 15 13:09:30.009 DEBUG apply_extrinsic: Updating storage for 0x66bb595bc60c8af0a306aa86edf96a88d3a59e9a [index: 0xc8f9a9dfd79ec8caa983b729134bf933685749347f774048aeeda9f0685a095f, value: 0x0000000000000000000000000000000000000000000000000000000000000001]    {ext}
```

 `0x66bb595bc60c8af0a306aa86edf96a88d3a59e9a` がコントラクトのアドレスです。

今後デモを作成し、もっとわかりやすく説明する予定です。

### Truffleからデプロイする

### truffleからコントラクトをデプロイする <a id="deploy-contracts-by-using-truffle"></a>

準備中

