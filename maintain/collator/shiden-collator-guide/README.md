# Mainnet collator guide

The **Astar Network** ecosystem has 2 mainnet parachains: ****&#x20;

* [**Astar**](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Frpc.astar.network#/accounts) **** connected to **Polkadot**&#x20;
* [**Shiden**](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fshiden.api.onfinality.io%2Fpublic-ws#/accounts) **** connected to **Kusama**

We have permissionless onboarding for collators if you meet our [requirements](../learn-about-collators.md), you can spin up a collator by bonding:

* **3 200 000 ASTR** on Astar
* **32 000 SDN** on Shiden

We also have a program to become a **whitelisted collator** for most supportive community members who have a **proven record** running collator nodes inside our ecosystem:

* Operators who have maintained a Dusty and [Shibuya collator node](../shibuya-network/) for a long time can get whitelisted on Shiden.
* Operators who have maintained a Shiden collator node for a long time can get whitelisted on Astar.

If you never operated a collator node, we strongly encourage you to spin up a **Shibuya collator** node to start before thinking about mainnet. You can join the _#collator-lounge_ our[ Discord](https://discord.gg/Z3nC9U4) to find out the latest news and support.&#x20;

{% hint style="danger" %}
From April 2022, a [slashing mechanism](../learn-about-collators.md) of 1% is implemented. Make sure you know very well how to run and monitor your collator to avoid financial loss!
{% endhint %}

{% content-ref url="../learn-about-collators.md" %}
[learn-about-collators.md](../learn-about-collators.md)
{% endcontent-ref %}

{% content-ref url="../shibuya-network/" %}
[shibuya-network](../shibuya-network/)
{% endcontent-ref %}

### Chain Specifications

{% content-ref url="../../../integration/network-details.md" %}
[network-details.md](../../../integration/network-details.md)
{% endcontent-ref %}

### Connect to Astar

{% embed url="https://polkadot.js.org/apps?rpc=wss%3A%2F%2Frpc.astar.network#/accounts" %}
Astar Polkadot.js portal
{% endembed %}

### Connect to Shiden

{% embed url="https://polkadot.js.org/apps?rpc=wss%3A%2F%2Frpc.shiden.astar.network#/accounts" %}
Shiden Polkadot.js portal
{% endembed %}

### Build a collator

{% content-ref url="spin-up-mainnet-collator.md" %}
[spin-up-mainnet-collator.md](spin-up-mainnet-collator.md)
{% endcontent-ref %}
