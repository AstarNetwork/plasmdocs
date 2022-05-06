# Network Details



Astar fully supports standard Substrate RPC methods that are Remote Calls available by default and allow you to interact with the actual node, query, and submit👇\
[https://polkadot.js.org/docs/substrate/rpc/](https://polkadot.js.org/docs/substrate/rpc/)

Link of deposit processing logic document - the doc describing how to get transaction information in the RPC return structure 👇\
[https://polkadot.js.org/docs/api/examples/promise/listen-to-balance-change/](https://polkadot.js.org/docs/api/examples/promise/listen-to-balance-change/)

API and free RPC WebSocket endpoints for the Astar community.👇

{% content-ref url="../build/api.md" %}
[api.md](../build/api.md)
{% endcontent-ref %}

{% hint style="info" %}
Building a dApp on Astar? **We recommend building your own endpoints or using our infra partners to make sure you have full control over them.**

Astar is not responsible for your project downtime in case of public endpoint issues. Currently, endpoints provided by Astar team have rate limits 10 reqs/sec. There is a possibility that this value will be lowered.



Use one of our infra partners:

* [BwareLabs](https://app.bwarelabs.com)
* [OnFinality](https://www.onfinality.io)
{% endhint %}

{% content-ref url="../maintain/archive-node/" %}
[archive-node](../maintain/archive-node/)
{% endcontent-ref %}

{% tabs %}
{% tab title="Astar Network" %}
The documentation corresponding contains details for the RPC - HTTP, WSS endpoints.&#x20;

| **Network name**     | Astar Network                                                                                                                                                                                                                                                                                                                                                                       |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Parent chain**     | Polkadot                                                                                                                                                                                                                                                                                                                                                                            |
| **Parachain ID**     | 2006                                                                                                                                                                                                                                                                                                                                                                                |
| **Chain ID**         | 592                                                                                                                                                                                                                                                                                                                                                                                 |
| **Symbol**           | ASTR                                                                                                                                                                                                                                                                                                                                                                                |
| **EVM RPC**          | <p>OnFinality: https://astar.api.onfinality.io/public</p><p></p><p>Astar team: https://evm.astar.network</p><p></p><p>Public RPCs may have traffic or rate-limits depending on usage. You can sign up for a dedicated free RPC URL at the following:</p><ul><li><a href="https://app.bwarelabs.com">Bware Labs</a></li><li><a href="https://onfinality.io">OnFinality</a></li></ul> |
| **Native RPC**       | <p>OnFinality: https://astar.api.onfinality.io/public</p><p></p><p>Astar team: https://rpc.astar.network</p><p></p><p>Public RPCs may have traffic or rate-limits depending on usage. You can sign up for a dedicated free RPC URL at the following:</p><ul><li><a href="https://app.bwarelabs.com">Bware Labs</a></li><li><a href="https://onfinality.io">OnFinality</a></li></ul> |
| **Native WebSocket** | <p>OnFinality: wss://astar.api.onfinality.io/public-ws</p><p></p><p>Astar team: wss://rpc.astar.network</p><p></p><p>Public RPCs may have traffic or rate-limits depending on usage. You can sign up for a dedicated free RPC URL at the following:</p><ul><li><a href="https://app.bwarelabs.com">Bware Labs</a></li><li><a href="https://onfinality.io">OnFinality</a></li></ul>  |
| **Block explorer**   | <p>Substrate: <a href="https://astar.subscan.io">https://astar.subscan.io</a></p><p>EVM: <a href="https://blockscout.com/astar/">https://blockscout.com/astar/</a></p>                                                                                                                                                                                                              |
{% endtab %}

{% tab title="Shiden Network" %}
The documentation corresponding contains details for the RPC - HTTP, WSS endpoints.&#x20;

| **Network name**     | Shiden Network                                                                                                                                                                                                                                                                                                                                                                              |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Parent chain**     | Kusama                                                                                                                                                                                                                                                                                                                                                                                      |
| **Parachain ID**     | 2007                                                                                                                                                                                                                                                                                                                                                                                        |
| **Chain ID**         | 336                                                                                                                                                                                                                                                                                                                                                                                         |
| **Symbol**           | SDN                                                                                                                                                                                                                                                                                                                                                                                         |
| **EVM RPC**          | <p>OnFinality: https://shiden.api.onfinality.io/public<br><br>Astar team: https://evm.shiden.astar.network</p><p></p><p>Public RPCs may have traffic or rate-limits depending on usage. You can sign up for a dedicated free RPC URL at the following:</p><ul><li><a href="https://app.bwarelabs.com">Bware Labs</a></li><li><a href="https://onfinality.io">OnFinality</a></li></ul>       |
| **Native RPC**       | <p>OnFinality: https://shiden.api.onfinality.io/public</p><p></p><p>Astar team: https://rpc.shiden.astar.network</p><p></p><p>Public RPCs may have traffic or rate-limits depending on usage. You can sign up for a dedicated free RPC URL at the following:</p><ul><li><a href="https://app.bwarelabs.com">Bware Labs</a></li><li><a href="https://onfinality.io">OnFinality</a></li></ul> |
| **Native WebSocket** | <p>OnFinality: wss://shiden.api.onfinality.io/public-ws<br><br>Astar team: wss://rpc.shiden.astar.network</p><p></p><p>Public RPCs may have traffic or rate-limits depending on usage. You can sign up for a dedicated free RPC URL at the following:</p><ul><li><a href="https://app.bwarelabs.com">Bware Labs</a></li><li><a href="https://onfinality.io">OnFinality</a></li></ul>        |
| **Block explorer**   | <p>Substrate: <a href="https://shiden.subscan.io">https://shiden.subscan.io</a></p><p>EVM: <a href="https://blockscout.com/shiden/">https://blockscout.com/shiden/</a></p>                                                                                                                                                                                                                  |
{% endtab %}

{% tab title="Shibuya" %}
The documentation corresponding contains details for the RPC - HTTP, WSS endpoints.&#x20;

| **Network name**     | Shibuya Network (parachain testnet)                                                                                                                                        |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Parent chain**     | Tokyo (own relay chain)                                                                                                                                                    |
| **Parachain ID**     | 1000                                                                                                                                                                       |
| **Chain ID**         | 81                                                                                                                                                                         |
| **Symbol**           | SBY                                                                                                                                                                        |
| **EVM RPC**          | https://evm.shibuya.astar.network                                                                                                                                          |
| **Native RPC**       | https://rpc.shibuya.astar.network                                                                                                                                          |
| **Native WebSocket** | wss://rpc.shibuya.astar.network                                                                                                                                            |
| **Block explorer**   | <p>Substrate: <a href="https://shibuya.subscan.io">https://shibuya.subscan.io/</a><br>EVM: <a href="https://blockscout.com/shibuya">https://blockscout.com/shibuya</a></p> |
{% endtab %}
{% endtabs %}





