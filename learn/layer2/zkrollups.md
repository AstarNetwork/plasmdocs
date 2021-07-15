# ZKRollups

Astar Network received a [Web3 Foundation grant](https://medium.com/plasm-network/plasm-network-team-receives-a-web3-foundation-open-grant-to-implement-zk-rollups-2faceeeeaf1e) to implement ZK Rollups. Astar's vision is to become a smart contract platform that supports rollups for both Ethereum Virtual Machine \(EVM\), WebAssembly \(Wasm\), and hoping to expand this in the future.

## What is a Rollup?

A Rollup is an off-chain aggregation of transactions inside an Ethereum smart contract, which reduces fees and congestion by increasing the throughput of the blockchain from its current 15 tps to more than 1,000 tps. Within the smart contract, users can transact with security guarantees. Their transactions will not be misused and they will settle to the main chain at some point in the future. It publishes just enough data on-chain so that any observer can reconstruct the state \(ex.: account balances\) and detect invalidity.

#### What is zkSync?

zkSync is a scaling and privacy engine for Ethereum. Its current functionality scope includes low gas transfers of ETH and ERC20 tokens in the Ethereum network.

![](https://cdn-images-1.medium.com/max/800/1*nhUeqOVM1ij6dwSM_nLyaw.png)

zkSync is built on ZK-Rollup architecture. In short, ZK-Rollup is an L2 scaling solution in which all funds are held by a smart contract on the main chain, while it performs computation and storage off-chain where the validity of the side chains is ensured by zero-knowledge proofs. For every Rollup block, a state transition zero-knowledge proof \(SNARK\) is generated and verified by the mainchain contract. This SNARK includes proof of the validity of every single transaction in the Rollup block. Additionally, the public data update for every block is published over the mainchain network in the cheap CALLDATA.

In other words, ZK-Rollup strictly inherits the security guarantees of the underlying L1.

## Roadmap

We are on track with the milestones we set upfront as you can see in the table below. There is still a lot ahead of us, and we will inform everyone of all the developments on our path.

![](../../.gitbook/assets/image%20%289%29.png)

