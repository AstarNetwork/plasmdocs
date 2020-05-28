---
description: This page explains the overview of Plasma
---

# Plasma Overview

Plasma is a framework for layer 2 blockchain scaling solution first proposed by Joseph Poon and Vitalik Buterin.

Plasma [White paper](https://plasma.io/plasma.pdf)

In the Plasma framework, any heavy lifting such as processing transaction will be handled by a separate off-chain node that is essentially a small copy of the main blockchain \(i.e. Ethereum\), called the child chain. The child chain will periodically communicate with the main blockchain for finalizing any set of state transitions that happened within the child chain.

## Why Plasma?

Blockchains are slow and expensive by design. The traditional design of blockchains are not yet capable of replacing the existing payment infrastructures without having an optimal scalability solution. We, Plasma implementers, strive to create a fast and cheap transaction system without sacrificing safety and decentralization that blockchains provide.

## In the Plasm Network

Plasma is one of the L2 scaling solution that Plasm Network provides. The basic idea of ​​Plasma is to manage and process transactions in a Merkle tree outside the chain at high speed and engrave only the Merkle root on to the main blockchain. In Plasma, the node responsible for performing the off-chain processing and submitting the hash to the blockchain is called an Aggregator.

![plasma\_1](https://user-images.githubusercontent.com/6259384/75877313-c4338600-5e5a-11ea-845a-edef3640c469.png)

Plasm Network supports a variant of Plasma that is based on Plasma-Cash. It has a single NFT state at the leaves of the Merkle tree. Rules for performing state transition can be defined by OVM which is described in a later section. The figure below shows an example of an NFT state transition that contains the ownership as its state and the necessary transaction.

![plasma\_2](https://user-images.githubusercontent.com/6259384/75877349-d7465600-5e5a-11ea-8ac8-5774636f2448.png)

In this construct, we have several requirements for making a state transition, 

1. It must be signed by "Owner"   
2. A new state must be specified for output   
3. A state must not have already been transitioned in another way, this is described using OVM. 

This set of verification is called a "Predicate". It is described in first-order logic. When OVM receives the accepted transaction, it changes the state and updates the Merkle root.

In Plasma, a single Aggregator handles these transactions and submits the resulting Merkle root. If the Aggregator cheats or attempt to submit an invalid transaction, the transaction submitted by the user can be falsified and reverted, as Plasma can dispute the correctness of transactions and states on the main chain using the OVM and Predicate described above. This allows Plasma to combine both the fast transaction processing power by a single Aggregator and the strong security that the blockchain provides.

