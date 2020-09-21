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

Polkadot平行链和中继链使以下事情成为可能：

1. **数据和代币可以在平行链之间无缝传输。**
2. **平行链可以导入中继链的安全性。**

如果你对Polkadot感兴趣，可以从以下网页中了解更多：

* **Polkadot 白皮书:** [https://polkadot.network/Polkadot-lightpaper.pdf](https://polkadot.network/Polkadot-lightpaper.pdf)
* **Polkadot 网页:** [https://polkadot.network/](https://polkadot.network/)
* **Polkadot 百科:** [https://wiki.polkadot.network/](https://wiki.polkadot.network/)

## Plasm Network 和 Polkadot

在本节中，我们将概述Plasm Network在Polkadot生态系统中的作用。Plasm Network的目标是成为Polkadot的第一个可扩展智能合约平行链。

### 智能合约

设计上[Polkadot](https://polkadot.network/)中继链并不支持智能合约，使得Plasm Network有机会去填补这个空缺。可拓展性无疑是dApps开发者最关键的需求。理想中，开发者们将可以在Plasm Network上开发任意应用程序而不用担心拓展性。

### 可拓展性

[Plasm Network](https://www.plasmnet.io/) 具有可拓展性因为我们采用了二层扩容方案和OVM\(Optimistic Virtual Machine\)。

{% page-ref page="../learn/optimistic-virtual-machine.md" %}

可拓展性是区块链所面临的最重要的问题之一。为了广泛采用区块链技术，区块链需要更更高的处理性能。可拓展性是区块链生态系统亟待解决的问题。 

可拓展性有两种类型: 

* **第1层 \(水平\) 可拓展性:** 对第一层区块链进行更多处理 \(例如，分片机制和SegWit隔离见证\)
* **Layer2 \(vertical\) scalability:** 对第二层区块链和链外进行更多处理  \(例如，Plasma和状态通道\)

Polkadot第一层可拓展性是通过分片机制实现的。 另一方面，[Plasm Network](https://www.plasmnet.io/)具有第二层 \(垂直\) 可拓展性。

![](../.gitbook/assets/sukurnshotto-2020-06-07-234905png.png)

第一层扩容方案和第二层扩容方案完全不同，同时相互补充以实现更灵活的开发。

此外，可拓展性并非第二层扩容方案的唯一优势，同时也可以带来：

* 第一最终性
* 更灵活的dApps开发
* 更低的交易成本

通过智能合约和二层扩容方案，我们期待在[Plasm Network](https://www.plasmnet.io/)实现多种 \(例如 游戏, IoT, 支付, DEX, 和 Bridge\) 

![](../.gitbook/assets/sukurnshotto-2020-06-08-00739png.png)

有疑问吗? 欢迎提问 [Discord Tech Channel](https://discord.gg/Z3nC9U4).

