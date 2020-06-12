# Plasma Overview 🔮

Plasma is a blockchain scaling solution invented by Joseph Poon and Vitalik Buterin.

[White paper](https://plasma.io/plasma.pdf)

Plasma is a framework to make a side chain and connect it to a main chain \(e.g. Ethereum\). The side chain and the main chain communicate each other.

## Why Plasma?

Blockchains are slow and expensive by design. Blockchains can't be an infrastructure of the world without an high scalability. Plasma intends on making blockchains fast and cheap without sacrificing safety and decentralization.

## In the Plasm Network

Plasma is a popular blockchain scaling solution. ​​Plasma manages and processes transactions in a Merkle tree outside the chain at high speed, and engraves only the Merkle root on the blockchain. The actor responsible for performing the off-chain processing and submitting the hash to the blockchain is called an Aggregator in Plasma.

![](../.gitbook/assets/sukurnshotto-2020-05-31-183650png.png)

Plasm Network supports "Plasma" which is based on Plasma-Cash. It has one NFT state, not a transaction, at the leaves of the Merkle tree. Rules for performing state transition can be defined by Optimistic Virtual Machine \(OVM\) are described later.

{% page-ref page="optimistic-virtual-machine.md" %}

Below shows an example of an NFT state transition that has ownership as a state and the necessary transaction.

![](../.gitbook/assets/sukurnshotto-2020-05-31-183843png.png)

State transition work flow:

1. Owner signes the transaction 
2. A new state must be specified for output   
3. A state must not have already been transitioned in another way, this is described using OVM. The logic described here is called "Predicate". It is described in first-order logic. When OVM receives the accepted transaction, it changes the state and updates the Merkle route.

In Plasma, a single Aggregator handles transactions and submits the Merkle route. If the Aggregator cheats, the transaction submitted by the user may be falsified. Plasma can dispute the correctness of transactions and states on the main chain using OVM and Predicate described above. This allows Plasma to combine both the fast transaction processing power by a single Aggregator and the strong security of the blockchain.

