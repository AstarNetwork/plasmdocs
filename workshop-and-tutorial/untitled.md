# Validator Guide

**TO BE REVIEWED**

> This short guide explain step by step how to become a Plasm Testnet validator.

* Install node **v1.0.0-dusty** using [binaries](https://github.com/staketechnologies/Plasm/releases/tag/v1.0.0-dusty) or [build from source code](https://github.com/staketechnologies/Plasm#building-from-source).
* Launch node plasm-node --validator --name node-name --rpc-cors all
* Wait for syncing up.

![](../.gitbook/assets/testnet_sync.png)

* Open [Setting](https://apps.plasmnet.io/#/settings) and select local node.

![](../.gitbook/assets/testnet_settings.png)

* Open [Accounts](https://apps.plasmnet.io/#/accounts) and create new account.

![](../.gitbook/assets/testnet_accounts.png)

* Share your validator account address and with **Stake Technologies** team in [Google Form](https://docs.google.com/forms/d/e/1FAIpQLSday0ckkK43TzJgKtQmJdzkudQNFDXspZAuUGi5Y5vfjkis3Q/viewform).
* [Claim tokens](https://medium.com/stake-technologies/dusty-lockdrop-how-to-claim-def048fa353) for transactions or request it in [Discord](https://discord.gg/Z3nC9U4) **\#faucet** channel.
* Open Toolbox window and call `rotateKeys()` RPC call or use curl command:

```bash
curl -H "Content-Type: application/json" -d '{"id":1, "jsonrpc":"2.0", "method": "author_rotateKeys", "params":[]}' http://localhost:9933
```

![](../.gitbook/assets/testnet_rotate.png)

* Save result for next step usage.
* Click "Session Key" button and paste result for validator account.

## Conclusion

When you finish this tutorial please wait a bit while **Stake Technologies** team approve your account as validator. Thank you for Plasm Network contribution and let's make Plasm better together!

## Testnet v3 migration

When you already participate in Testnet V3 validation you could be initerested in migration. Please copy your session keys from testnet v3 keystore into dusty keystore by following commands before launch node:

```text
mkdir .local/share/plasm-node/chains/dusty
cp -r .local/share/plasm-node/chains/plasm_testnet_v3/keystore .local/share/plasm-node/chains/dusty
```

