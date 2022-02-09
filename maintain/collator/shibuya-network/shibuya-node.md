# Spin up testnet Collator

### Build a collator node

Start by building the collator node with the guide from [Secure Collator Setup](../secure-validator/) below:

{% content-ref url="../secure-validator/plasm-shiden-node.md" %}
[plasm-shiden-node.md](../secure-validator/plasm-shiden-node.md)
{% endcontent-ref %}

### Verify synchronization

Before jumping to the next steps, you have to wait until your node is **fully synchronized**. This can take a long time depending on the chain height.

Check the current synchronization status:

```
journalctl -f -u shibuya-node -n100
```

### Session Keys

#### Author session keys

Run the following command to author session keys:

```
curl -H "Content-Type: application/json" -d '{"id":1, "jsonrpc":"2.0", "method": "author_rotateKeys", "params":[]}' http://localhost:9933
```

Result will look like this, copy the key:

```
{"jsonrpc":"2.0","result":"0x600e6cea49bdeaab301e9e03215c0bcebab3cafa608fe3b8fb6b07a820386048","id":1}
```

#### Set session keys

Go to the Shibuya Polkadot.js portal: _**Developper > Extrinsic**_

Select your **collator account** and extrinsic type: _**session / setKeys**_

Enter the **session keys** and set proof to `0x00`

![](<../../../.gitbook/assets/Capture d’écran de 2022-02-08 20-35-09.png>)

Submit the transaction.

### Identity

#### Set identity

Go to the Shibuya Polkadot.js portal: **Accounts**

Open the 3 dots next to your collators address: **Set on-chain Identity**

![](<../../../.gitbook/assets/Capture d’écran de 2022-02-08 20-48-00.png>)

Enter all fields you want to set.

![](<../../../.gitbook/assets/Capture d’écran de 2022-02-08 20-54-16.png>)

Send the transaction.

#### Request judgment

Go to the Shibuya Polkadot.js portal: _**Developper > Extrinsic**_

Select your **collator account** and extrinsic type: _**identity / requestJudgment**_

![](<../../../.gitbook/assets/Capture d’écran de 2022-02-08 20-58-04.png>)

Send the transaction.

### Bond funds

To start collating, you need to have 32 000 SBY tokens.

Go to the Shibuya Polkadot.js portal: _**Developper > Extrinsic**_

Select your **collator account** and extrinsic type: _**CollatorSelection / registerAsCandidate**_

![](<../../../.gitbook/assets/Capture d’écran de 2022-02-08 20-38-46.png>)

Submit the transaction.

### Production blocks

{% hint style="info" %}
Onboarding takes place at `n+1` session.
{% endhint %}

Once your collator is active, you will see your name inside **Network** tab every time you produce a block:

![](<../../../.gitbook/assets/Capture d’écran de 2022-02-08 21-04-11.png>)

### External documentation

For an all-in-one tutorial, you can find below he document made by _Mercury_, one of our community members during the Shibuya onboarding challenge.

{% embed url="https://app.subsocial.network/4907/shibuya-collators-guide-19840" %}
