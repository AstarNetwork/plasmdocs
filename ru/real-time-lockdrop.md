# Real Time Lockdrop

{% hint style="warning" %}
このモジュールは実験的なもので、いくつかの機能が動作しなかったり、問題があっても動作しなかったりします。問題を発見した際には[こちら](https://github.com/staketechnologies/Plasm/issues/new/choose)よりレポートをお願いします。
{% endhint %}

### Quick Install <a id="quick-install"></a>

1. [README](https://github.com/staketechnologies/Plasm/tree/plasm-real-time-lockdrop#building-from-source)に従って依存関係をインストールします。 
2. plasm-nodeのカスタムロックドロップブランチを取得します。

```text
git clone https://github.com/staketechnologies/Plasm -b plasm-real-time-lockdrop && cd Plasm
```

1. Plasm binaryをビルドります。

```text
cargo build --release
```

1. ビルドが完了するのを待ちます。

### Preparing for tests <a id="preparing-for-tests"></a>

1. development modeでノードを立てます。

```text
./target/release/plasm-node --dev
```

> Previous versions of db should be removed before launch: `./target/release/plasm-node purge-chain --dev`

1. Plasm Portalの[Settings page](https://apps.plasmnet.io/#/settings)を開きます。
   1. `Local Node`.にremote endpointを設定します。
   2. `Developer` タブで以下のcustom typesを入力します。

```text
{
  "ClaimId": "H256",
  "Lockdrop": {
    "type": "u8",
    "transaction_hash": "H256",
    "public_key": "[u8; 33]",
    "duration": "u64",
    "value": "u128"
  },
  "TickerRate": {
    "authority": "u16",
    "btc": "DollarRate",
    "eth": "DollarRate"
  },
  "DollarRate": "u128",
  "AuthorityId": "AccountId",
  "AuthorityVote": "u32",
  "ClaimVote": {
    "claim_id": "ClaimId",
    "approve": "bool",
    "authority": "u16"
  },
  "Claim": {
    "params": "Lockdrop",
    "approve": "AuthorityVote",
    "decline": "AuthorityVote",
    "amount": "u128",
    "complete": "bool"
  }
}
```

### Price oracle <a id="price-oracle"></a>

起動後、権限ノードは定期的にフェッチを開始し、ブロックチェーンに送信します BTCとETHの現在の価格を米ドルで取得します。[エクスプローラ](https://apps.plasmnet.io/#/explorer)を開くと、各インポートされたモジュールに設定されたドルレートのExtrinsicを見ることができます。このドルレートは、発行量の推定のためのロックドロップパレットで使用されます。

![Set Dollar Rate](https://docs.plasmnet.io/img/set_dollar_rate_xt.png)

### Lockdrop request <a id="lockdrop-request"></a>

特にテスト目的のために我々はEthereum RopstenネットワークにLockdropスマートコントラクトをデプロイしました。

* [https://ropsten.etherscan.io/address/0xeed84a89675342fb04fafe06f7bb176fe35cb168](https://ropsten.etherscan.io/address/0xeed84a89675342fb04fafe06f7bb176fe35cb168)

Etherscanとmetamaskを使ってトランザクションをlockdropスマートコントラクトに送り込んでみましょう。

![Lock tx](https://docs.plasmnet.io/img/lock_tx_etherscan.png)

ロックした後、Plasm開発チェーンでリクエストを作成してみましょう。

![Request](https://docs.plasmnet.io/img/eth_lockdrop_req.png)

使用したテストデータは以下です。

```text
0x6c4364b2f5a847ffc69f787a0894191b75aa278a95020f02e4753c76119324e0
0x039360c9cbbede9ee771a55581d4a53cbcc4640953169549993a3b0e6ec7984061
2592000
100000000000000000
```

![Response](https://docs.plasmnet.io/img/eth_lockdrop_res.png)

また、結果は以下で確認することができます。

![Chain state](https://docs.plasmnet.io/img/eth_lockdrop_state.png)

質問があれば、[Tech Chat](https://discord.gg/Cyjnrxv)の日本語チャネルでご質問ください。

