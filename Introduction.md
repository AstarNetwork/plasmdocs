Reminder: This is the first draft. We will polish this draft to make it more understandable and more professional.

# Introduction
We realize Web3.0 by utilizing blockchain technologies. In the existing society, data and wealth are controlled by central authorities and history shows us that they made a monopoly structure and created the rules that justify themselves. Even if the centralized authority builds a fair mechanism, this has not been verifiable because the system has no transparency. Traditionally, the protocol and application have been based on the trust of the party.  On the other hand, public blockchain, a decentralized peer to peer network has decentralized governance to realize a trust-less system with high transparency and fairness without a single point of failure. In this sense, public blockchain has fault tolerance and a high tamper resistance on the system that anyone can view, verify, and operate.

An application is necessary when protocol developers deliver the benefits of blockchain because an application is an interface between a protocol and a user. Blockchain applications are generally called Decentralized Application (DApps). A lot of DApps have been developed and provided to users on various blockchains in the form of smart contracts and chain codes. However, the processing performance of Dapps is not high due to the distributed and redundant structure of blockchains. The transaction throughput of Ethereum, the largest smart contract platform, is 14 per second. On the other hand, VISA and Alipay, which have many users around the world, process 3,000 transactions and 256,000 transactions per second. It turns out that the current performance is too inadequate for many users to get benefits from Dapps. Therefore, various scaling solutions were invented.

There are several blockchain scaling solutions. For example, 

1. **SegWit** : Fixing transaction malleability by removing the signature information and storing it outside the base transaction block. 
2. **State channel** : Combining off-chain transactions among particular users and only the final state is committed to the main blockchain.
3. **Sharding :** Allowing many more transactions to be processed in parallel at the same time by making shards. 
4. **Plasma** :  Storing transactions in separate child chains and only the root hash is stored in the main chain.

And so on. 
**To Do: Clarify the sentences above.**

Among all scaling solutions, we focus on layer2 solutions because public blockchain like Bitcoin and Ethereum are almost full[15]. We believe that blockchain will be used in a different way from the way we use today. The 1st layer will be a trust layer and a 2nd layer will be a transaction layer. 

Among all layer2 solutions, the reason we focus on Plasma is that Plasma is a scaling solution that is the least dependent on the processing performance of the main chain. In Plasma, an operator manages his side-chain without sacrificing decentralization. This means that many transactions can be handled in a centralized way that does not require a consensus process, but all participants on the side chain can safely exit by submitting fraud proofs. The scaling solutions used in the existing centralized system can be used as they are. Hence, it is possible to achieve high processing performance that is not feasible with a native distributed ledger. Plasma should be recognized as an indispensable technology in the future because it can dramatically improve processing performance for all distributed ledgers.

However, Plasma has several difficulties. First, there is a limitation on what can be done with Plasma Applications (Plapps).  All the things that Plasma can is described with Predicate[11]. But, the Predicate is under development. 
**To Do: Add an explanation of Predicate.**

Second, it is difficult to make a Plapps compared to making a traditional DApp because writing and deploying smart contracts are not enough to make a Plapps. Plasma is the complicated technical stack that consists of several components. Precisely, Plasma application consists of 4 components, a smart contract on a parent chain, a child chain, an operator, and a user. We solve these two problems through **"Plasm Project"**. 

**"Plasm Project"** has

- **Plasm** is a set of standard libraries that enable to write Predicates quickly.
- **PlaaS** is cloud service to deploy and manage the Plasma components.
- **Plasm chain** is a blockchain that is expected to be a parachain on Polkadot.

With these tools, Plasm developers can build their applications easily. 

We are planning to build these systems around Polkadot.  Polkadot is a heterogeneous multi chain framework which empowers blockchain networks to work together under the protection of shared security. In addition, there is a framework to create blockchains called Substrate. Currently, Polkadot itself and parachains are created with Substrate. In the future, we think blockchains will be paralleled simply because there is no perfect blockchain which supports all governance models and customer's needs by itself. Hence, there are more than 900 public blockchains have been built and more and more blockchains are being created. Polkadot and Substrate empower this movement of creating the perfect custom blockchain based on the need. Plasma is one of the most promising domains on Polkadot as Dr.Gavin mentioned at Subzero Summit. We decided to make Plasma solutions for Polkadot and Substrate.

Presented by [StakeTechnologies](https://stake.co.jp).