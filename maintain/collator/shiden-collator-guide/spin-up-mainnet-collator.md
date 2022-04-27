# Spin up mainnet Collator

### Build a collator node <a href="#build-a-collator-node" id="build-a-collator-node"></a>

​Start by building the collator node with the guide from [Secure Collator Setup](../secure-validator/) below:

{% content-ref url="../secure-validator/plasm-shiden-node.md" %}
[plasm-shiden-node.md](../secure-validator/plasm-shiden-node.md)
{% endcontent-ref %}

{% hint style="warning" %}
Collators are responsible for the network stability, it is very important to be able to react at any time of the day or night in case of trouble. We strongly encourage collators to set up a monitoring and alerting system as described in the [Secure Collator Setup](../secure-validator/).
{% endhint %}

### Verify synchronization <a href="#verify-synchronization" id="verify-synchronization"></a>

Before jumping to the next steps, you have to wait until your node is **fully synchronized**. This can take a long time depending on the chain height.

Check the current synchronization:

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

#### Set session keys <a href="#set-session-keys" id="set-session-keys"></a>

Go to the Polkadot.js portal: _**Developper > Extrinsic**_

Select your **collator account** and extrinsic type: _**session / setKeys**_

Enter the **session keys** and set proof to `0x00`

![](<../../../.gitbook/assets/image (111) (1).png>)

Submit the transaction.

### Identity <a href="#identity" id="identity"></a>

#### Set identity <a href="#set-identity" id="set-identity"></a>

Go to the Polkadot.js portal: **Accounts**

Open the 3 dots next to your collators address: **Set on-chain Identity**

![](<../../../.gitbook/assets/image (119) (1) (1) (1) (1).png>)

Enter all fields you want to set.

![](<../../../.gitbook/assets/image (117) (1) (1).png>)

Send the transaction.

#### Request judgment <a href="#request-judgment" id="request-judgment"></a>

Go to the Polkadot.js portal: _**Developper > Extrinsic**_

Select your **collator account** and extrinsic type: _**identity / requestJudgment**_

Send the transaction.

### Bond funds <a href="#bond-funds" id="bond-funds"></a>

To start collating, you need to have **32 000 SDN** tokens for Shiden or **3 200 000 ASTR** tokens for Astar.

Go to the Shibuya Polkadot.js portal: _**Developper > Extrinsic**_

Select your **collator account** and extrinsic type: _**CollatorSelection / registerAsCandidate**_

![](<../../../.gitbook/assets/image (116) (1) (1).png>)

Submit the transaction.

### Production blocks <a href="#production-blocks" id="production-blocks"></a>

{% hint style="info" %}
Onboarding takes place at `n+1` session
{% endhint %}

Once your collator is active, you will see your name inside **Network** tab every time you produce a block:

![](<../../../.gitbook/assets/image (113) (1) (1).png>)

### Maintenance

Maintaining a collator means it has to stay up and up-to-date all the time, have a look at [Maintenance operations](../../node-maintenance.md) page to get familiar with those.

{% content-ref url="../../node-maintenance.md" %}
[node-maintenance.md](../../node-maintenance.md)
{% endcontent-ref %}
