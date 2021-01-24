# Validator Guide

Thanks to our community we have several tutorials you can use to become a validator on Plasm Testnet.

* Install Dusty on your local device
* Install Dusty on a VPS server \([Microsoft Azure](https://fiex.medium.com/plasm-node-on-azure-32ec5a204b45), [Digital Ocean](https://fiex.medium.com/become-a-plasm-network-validator-c212085cc72e), ...\)
* Install Dusty on a [Raspberry Pi4](https://github.com/bLd75/Plasm-RPi)

To become a validator, follow these steps:

1. Run a node on Dusty network.
2. Claim tokens for transactions by requesting them on [the Discord](https://discord.gg/Z3nC9U4) **\#faucet** channel.
3. Get your `rotateKey()` and connect this to your validator account.
4. Share your validator account address with **Stake Technologies** team via [Google Form](https://docs.google.com/forms/d/e/1FAIpQLSday0ckkK43TzJgKtQmJdzkudQNFDXspZAuUGi5Y5vfjkis3Q/viewform).
5. Follow your submission in the [Dusty validator sheet](https://docs.google.com/spreadsheets/d/1AYsS6V_Ypwde5lYulhZBMAx1X2vZ1u1zDXni_ddz-6c/edit#gid=2013382367).

{% hint style="info" %}
Tutorial video for running a node on Microsoft Azure  👇
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=wZgIqAufyCE&ab\_channel=KenzoKobayashi" caption="Kenzo Kobayashi, Plasm Network Ambassador" %}

{% hint style="info" %}
This short guide explains how to become a Dusty validator step by step on your local device.
{% endhint %}

* Install node **v1.7.0-dusty** using [binaries](https://github.com/PlasmNetwork/Plasm/releases/tag/v1.7.0-dusty) or [building from source code](https://github.com/staketechnologies/Plasm#building-from-source).
* Launch node `plasm-node --validator --name node-name --rpc-cors all`
* Wait for syncing up.

![](../.gitbook/assets/testnet_sync.png)

* Open "[Setting](https://apps.plasmnet.io/#/settings)" and select "local node".

![](../.gitbook/assets/testnet_settings.png)

* Open "[Accounts](https://apps.plasmnet.io/#/accounts)" and create a new account.

![](../.gitbook/assets/testnet_accounts.png)

* Share your validator account address with **Stake Technologies** team via [Google Form](https://docs.google.com/forms/d/e/1FAIpQLSday0ckkK43TzJgKtQmJdzkudQNFDXspZAuUGi5Y5vfjkis3Q/viewform).
* Claim tokens for transactions by requesting them on [the Discord](https://discord.gg/Z3nC9U4) **\#faucet** channel.
* Open Toolbox window and call `rotateKeys()` RPC call or use curl command:

```bash
curl -H "Content-Type: application/json" -d '{"id":1, "jsonrpc":"2.0", "method": "author_rotateKeys", "params":[]}' http://localhost:9933
```

![](../.gitbook/assets/testnet_rotate.png)

* Save the result for the next steps.
* Click the "Session Key" button and paste the result for the validator account.

## Conclusion

When you finish this tutorial, please wait a bit while **Stake Technologies** team approves your account as a validator. Thank you for Plasm Network contribution and let's make Plasm better together!

If you have already participated in testnet V3 as a validator, you could be interested in migration. Please copy your session keys from **testnet v3 keystore** into **dusty keystore** by following commands before launch node:exit: Ctrl+↩

```text
mkdir .local/share/plasm-node/chains/dustycp -r .local/share/plasm-node/chains/plasm_testnet_v3/keystore .local/share/plasm-node/chains/dusty
```

Any questions? Feel free to ask us on [Discord Tech Channel](https://discord.gg/Z3nC9U4).

