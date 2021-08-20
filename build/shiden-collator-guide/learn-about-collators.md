# Learn about Shiden collators

## Introduction

A collator plays an essential role in the Shiden network and is responsible for crucial tasks, including block production and transaction confirmation. A collator needs to maintain a high communication response capability to ensure the seamless operation of the Shiden Network.

Based on network affordability and security considerations, collator seats will gradually open after the launch of Shiden.  


## Role of collators in Shiden Network

Collators maintain Shiden Network by collecting transactions from users and producing state transition proofs for Relay Chain validators. In other words, collators maintain Shiden Network by aggregating parachain transactions into parachain block candidates and producing state transition proofs for validators based on those blocks.   


Unlike validators, collator nodes do not secure the network. If a parachain block is invalid, it will get rejected by validators. Therefore the assumption that having more collators is better or more secure is not correct. On the contrary, too many collators may slow down the network. The only nefarious power collators have transaction censorship. To prevent censorship, a parachain only needs to ensure some neutral collators - but not necessarily a majority. Theoretically, the censorship problem is solved by having just one honest collator. \(reference: [https://wiki.polkadot.network/docs/learn-collator](https://wiki.polkadot.network/docs/learn-collator)\)  


**XCMP**

Collators are a key element of [XCMP \(Cross-Chain Message Passing\)](https://wiki.polkadot.network/docs/learn-crosschain). By being full-nodes of the Relay Chain, they are all aware of each other as peers. This makes it possible for them to send messages from parachain A to parachain B.  


## Aura PoS

Aura PoS consist out of 2 pallets:

* [Aura pallet](https://crates.parity.io/pallet_aura/index.html)
* PoS pallet

The first phase in making Shiden PoS will be by deploying the Aura pallet. Aura PoA Collator Phase - permissioned block authoring and collator session key setup for Shiden. After extended testing, we will deploy the PoS pallet and switch to Aura PoS. We will enable permissionless collator staking, network inflation, and rewards.

**Let’s break down the latest phase:**

* **Collator staking**: collators can now start with staking. This will be with a minimum bond of 32k SDN tokens or be selected to join the first collator set \(these are already selected\).
* **Network inflation**: 10% inflation will start after this phase 10% per year \(7,000,000 SDN for the first year\).
* **Reward**: a fixed amount will be created at each block 2.66 SDN for the first 2,628,000 blocks \(block time of 12 seconds\) and divided like the following scheme 

![](https://lh3.googleusercontent.com/z-BcHXcOdD9Yy7q5Q93lNsdaGo53uaLX4lVpJdapDiOUcPOjzFC5l2R9wX_meTHkTYA1RFXHBh8MAnxFfieEbvsB9DWiBkYDsvw7Y65tHk8XzUTnNqczNhrzXftAIdPAe19q6-GT)

A collator \(block producer\) gets a reward for each block it’s produced. The reward is around 0.266 SDN for each block.

## How to become a collator

### SDN balance

To become a collator for Shiden, you need to know these settings:

**Collator staking parameters/limit:**

* Bond: 32,000 SDN
* Bond duration: 7 days
* Slots: 200 active collators
* Estimated annual percentage yield: 11%

### System requirements

A collator usually deploys its nodes on cloud servers. You can choose your preferred VPS service provider and operating system. We recommend Ubuntu 18.04 and Azure.

**Hardware requirements:**

Shiden will provide a basic configuration for reference, which guarantees that all blocks can process in time. If the hardware is inferior to that, there is a chance it will be malfunctioning.

**Basic configuration:**

* System: Linux or macOS, Ubuntu 20 is recommended
* CPU: at least two cores, Intel Core
* Memory: at least 8 GB
* Hard disk: at least 120 GB, regularly evaluated

**Recommended configuration:**

* System: Linux or macOS, Ubuntu 20
* CPU: 4 cores, Intel Core
* Memory: 8-16 GB
* Hard Disk: 250 GB

## How to deploy your node 

{% page-ref page="become-a-collator.md" %}

## Collator election mechanism

### Election process

In an era \(24 hours\), the Shiden Network will lock the data in the last 15 minutes of the fifth epoch. When your node fits the parameters and checks all the boxes to become a collator, you will be added to the chain. Note: if your collator doesn’t produce blocks during one session \(1h\) it will be kicked as collator.

## Collator reward distribution mechanism

In the Shiden network, the system records each collator’s rewards in an epoch cycle and issues rewards in an era cycle. A collator does not need to claim the rewards but will be added automatically to their stash account.  


## Slash mechanism

At this stage, there is no slash mechanism in place on Shiden Network but if a collator doesn’t produce blocks in one session it will be kicked as a collator in the network.

## FAQ

### What about NPoS?

Our first intention was to activate NPoS to Shiden Network. After internal testing, this would use a lot of Shiden collator resources. NPoS is not designed for collators in the Polkadot ecosystem \(see part: role of collators\). Astar ecosystem is build to be a dApp hub in the Polkadot ecosystem for smart contracts with a unique incentive reward mechanism for developers, dApp staking.   


### How can users get staking rewards?

Users can nominate smart contracts through dApp staking and earn the same staking rewards as they would on validators. By staking on smart contracts you not only get staking rewards but you support your favorite project that is building in our ecosystem. 

It’s still possible to stake on collators in our network but this is possible with our partners who build their own nominated system for their collator.

