# Polkadot 波卡 🔴

![](../.gitbook/assets/sukurnshotto-2020-06-07-221155png.png)

[Polkado](https://polkadot.network/)是一个具有异构分片机制的公链，使各独立区块链可以互相交换信息和价值。同时它也是由Gavin Wood作为创始人&CTO的[Web3 Foundation](https://web3.foundation/)主导开发的一个开源项目。

### Polkadot 基础

![](../.gitbook/assets/sukurnshotto-2020-06-07-230056png.png)

Polkadot主要包含两个部分: 中继链和平行链。

* **中继链:** Polkadot的核心, 负责网络安全，共识机制和跨链互操作性。
* **平行链:** 可拥有自定义代币，并针对特定用例优化功能的主权区块链。需要付费使用或租用一个插槽连接到中继链。

[**Plasm Network**](https://www.plasmnet.io/) **计划成为Polkadot的第一个可拓展智能合约平行链. \(**Plasm可以成为平行链因为它是使用Parity Substrate开发\)

{% page-ref page="substrate.md" %}

Through this architecture, Polkadot makes the following things possible. 

1. **By connecting Parachain to the Relaychain, the data and token can be transferable among Parachains seamlessly.**
2. **Parachain can import Relaychain's security.**

If you are interested in Polkadot, you can learn more from the following web pages.

* **Polkadot Lightpaper:** [https://polkadot.network/Polkadot-lightpaper.pdf](https://polkadot.network/Polkadot-lightpaper.pdf)
* **Polkadot web page:** [https://polkadot.network/](https://polkadot.network/)
* **Polkadot wiki:** [https://wiki.polkadot.network/](https://wiki.polkadot.network/)

##  Plasm Network and Polkadot

In this section, we will describe the roles of [Plasm Network ](https://www.plasmnet.io/)in the Polkadot ecosystem. [Plasm Network](https://www.plasmnet.io/) aims to be the first scalable smart contract Polkadot Parachain. 

### Smart Contract

The [Polkadot](https://polkadot.network/) Relaychain, by design, does not support smart contracts. This allows Plasm the opportunity to fill in this gap. Scalability is obviously one of the most crucial demands DApp developers have. Ideally, the developers can build whatever applications on Plasm Network without having to consider its scalability.

### Scalability

[Plasm Network](https://www.plasmnet.io/) is scalable because we are implementing layer2 solutions especially Optimistic Virtual Machine.

{% page-ref page="../learn/optimistic-virtual-machine.md" %}

Scalability is one of the most crucial issues blockchain has. In order to make blockchain a social infrastructure, it needs high processing performance. Solving this scalability problem in the blockchain ecosystem is an urgent task for us.

When we say scalability, there are 2 types: 

* **Layer1 \(horizontal\) scalability:** The concept of layer1 scalability is to do more on layer1 blockchain. \(e.g. sharding and Segwit\)
* **Layer2 \(vertical\) scalability:** The concept of layer2 scalability is to do less on layer1 and to do more on layer2 or off-chain.  \(e.g. Plasma and State Channel\)

Polkadot has the layer1 scalability because it is a sharding ish architecture. [Plasm](https://www.plasmnet.io/) is also scalable because it has layer2 vertical scalabilities. 

![](../.gitbook/assets/sukurnshotto-2020-06-07-234905png.png)

Layer1 solution and layer2 solution are completely different and they complement each other. 

In addition to that, scalability is NOT just a benefit we can get through layer2 solutions. We can get the followings as well

* **First Finality**
* **Flexible DApps development**
* **Cheaper transaction\(gas\) cost**

Through layer1 smart contract and layer2 solutions, we are looking forward to seeing various use cases on [Plasm Network](https://www.plasmnet.io/). \(e.g. Gaming, IoT, Payment, DEX, and Bridge\) 

![](../.gitbook/assets/sukurnshotto-2020-06-08-00739png.png)

Any questions? Feel free  to ask us on [Discord Tech Channel](https://discord.gg/Z3nC9U4).

