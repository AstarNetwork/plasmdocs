# Layer2 and Plasma ⚡

### The Necessity of Scalability

At the time of this writing, the second-biggest blockchain that acts as a Dapp platform is [Ethereum](https://www.ethereum.org/), which can process around 15 transactions per second \(ref:[Ethereum Transaction Throughput](https://www.coindesk.com/information/will-ethereum-scale)\). In contrast to this, VISA or Alipay can process around 1,700 transactions \(ref:[Visa Transaction Throughput](https://hackernoon.com/the-blockchain-scalability-problem-the-race-for-visa-like-transaction-speed-5cce48f9d44)\) and 256,000 transactions respectively \(ref:[ALIPAY Transaction Throughput](https://www.barrons.com/articles/alibaba-records-25-3-billion-in-singles-day-sales-1510538618)\). It is true that the transaction speed for Dapps is very slow for users to utilize this technology to its full potential. To solve this issue, there have been several blockchain scalability solutions being proposed.

### Some Blockchain Scaling Solutions

These are some of the well-known blockchain scalability solutions.

1. [**SegWit**](https://github.com/bitcoin/bips/blob/master/bip-0141.mediawiki): Fixing transaction malleability by removing the signature information and storing it outside of the base transaction block.
2. [**State Channel**](https://l4.ventures/papers/statechannels.pdf): Combining off-chain transactions among particular users and only the final state is committed to the main blockchain.
3. [**Sharding**](https://www.bubifans.com/ueditor/php/upload/file/20181015/1539597837236127.pdf): Allowing many more transactions to be processed in parallel at the same time by making shards.
4. [**Plasma**](https://plasma.io/plasma.pdf): Storing transactions in separate child chains and only the root hash is stored in the main chain.

Broadly speaking, we have two types of scaling solutions: Layer1 solutions and Layer2 solutions. 

Layer1 solutions try to do more of what developers can do on layer1. On the contrast, layer2 solutions try to do less on layer1 and try to do more on layer2 or off-chain.  

We want to focus on processing transactions outside of the main chain, called the Layer 2 solution. Layer 1 refers to public blockchains like Ethereum or Bitcoin. In recent years, this layer is suffering from increased transaction capacity, making the blockchain "full" \(ref:["The Ethereum-blockchain size has exceeded 1TB, and yes, it’s an issue"](https://hackernoon.com/the-ethereum-blockchain-size-has-exceeded-1tb-and-yes-its-an-issue-2b650b5f4f62)\). 

From this, we can predict that in about a decade, **blockchain will have a different usage, where Layer 1 is used as the trust layer, while Layer 2 is the transaction layer.**

Among all layer2 solutions, the reason we focus on Plasma is that it is a scaling solution that is the **least** dependent on the processing performance of the main chain. In Plasma, an operator manages its side-chain without sacrificing decentralization. **This means that many transactions can be handled in a centralized way that does not require a consensus process, but all participants on the side chain can safely exit by submitting fraud proofs.** The scaling solutions used in the existing centralized system can be used as they are. Hence, it is possible to achieve high processing performance that is not feasible with a native distributed ledger. 

Plasma should be recognized as an indispensable technology in the future because it can dramatically improve processing performance for all distributed ledgers.

