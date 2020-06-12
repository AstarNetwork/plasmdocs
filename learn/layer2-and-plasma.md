# Layer 2 and Plasma ⚡

### About Scalability

At the time of writing, the second-biggest blockchain that acts as a dApps platform is [Ethereum](https://www.ethereum.org/), which can process around 15 transactions per second \(ref:[Ethereum Transaction Throughput](https://www.coindesk.com/information/will-ethereum-scale)\). VISA or Alipay can process around 1,700 transactions per second \(ref:[Visa Transaction Throughput](https://hackernoon.com/the-blockchain-scalability-problem-the-race-for-visa-like-transaction-speed-5cce48f9d44)\) and 256,000 transactions per second respectively \(ref:[ALIPAY Transaction Throughput](https://www.barrons.com/articles/alibaba-records-25-3-billion-in-singles-day-sales-1510538618)\). Transaction speed for dApps is slow and prohibitive for bringing new users to this technology. To solve this issue, there have been several blockchain scalability solutions proposed:

### Blockchain Scaling Solutions

These are some of the well-known blockchain scalability solutions:

1. [**SegWit**](https://github.com/bitcoin/bips/blob/master/bip-0141.mediawiki): Fixing transaction malleability by removing the signature information and storing it outside of the base transaction block.
2. [**State Channel**](https://l4.ventures/papers/statechannels.pdf): Combining off-chain transactions among particular users and only the final state is committed to the main blockchain.
3. [**Sharding**](https://www.bubifans.com/ueditor/php/upload/file/20181015/1539597837236127.pdf): Allowing many more transactions to be processed in parallel at the same time by making shards.
4. [**Plasma**](https://plasma.io/plasma.pdf): Storing transactions in separate child chains and only the root hash is stored in the main chain.

Scaling solutions can be categorized as layer 1 or layer 2.

Layer 1 solutions exist only on layer 1 of the Ethereum mainnet.  Layer 2 solutions may combine layer 1, layer 2, and off-chain solutions for greater performance and scalability.  

Transaction processing needs to be done outside of the mainnet layer 1 chain as it is reaching critical performance limits\(ref:["The Ethereum-blockchain size has exceeded 1TB, and yes, it’s an issue"](https://hackernoon.com/the-ethereum-blockchain-size-has-exceeded-1tb-and-yes-its-an-issue-2b650b5f4f62)\). 

Ultimately, **the blockchain model may evolve, where layer 1 is used as the trust layer, and layer 2 is the transaction layer.**

Plasma is a layer 2 scaling solution that is the **least** dependent on the processing performance of the main chain.  Plasma is a decentralized operator managed side-chain. **Transactions can be handled in a centralized way that does not require a consensus, but participants on the side chain can only safely exit by submitting fraud proofs.** The scaling solutions used in the existing centralized system can be used as they are.

Plasma could become an indispensable technology in the future, dramatically improving processing performance for all distributed ledgers.

