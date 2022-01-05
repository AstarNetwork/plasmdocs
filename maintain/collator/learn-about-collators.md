# Learn about collators

## Introduction

A collator plays an essential role in our network and is responsible for crucial tasks, including block production and transaction confirmation. A collator needs to maintain a high communication response capability to ensure the seamless operation of the Shiden Network.

Based on network affordability and security considerations, collator seats will gradually open after the launch of Shiden.\


## Role of collators in Astar ecosystem

Collators maintain our ecosystem by collecting transactions from users and producing state transition proofs for Relay Chain validators. In other words, collators maintain the network by aggregating parachain transactions into parachain block candidates and producing state transition proofs for validators based on those blocks. \


Unlike validators, collator nodes do not secure the network. If a parachain block is invalid, it will get rejected by validators. Therefore the assumption that having more collators is better or more secure is not correct. On the contrary, too many collators may slow down the network. The only nefarious power collators have transaction censorship. To prevent censorship, a parachain only needs to ensure some neutral collators - but not necessarily a majority. Theoretically, the censorship problem is solved by having just one honest collator. (reference: [https://wiki.polkadot.network/docs/learn-collator](https://wiki.polkadot.network/docs/learn-collator))\


**XCMP**

Collators are a key element of [XCMP (Cross-Chain Message Passing)](https://wiki.polkadot.network/docs/learn-crosschain). By being full-nodes of the Relay Chain, they are all aware of each other as peers. This makes it possible for them to send messages from parachain A to parachain B.\


## Aura PoS

Aura PoS consist out of 2 pallets:

* [Aura pallet](https://crates.parity.io/pallet\_aura/index.html)
* PoS pallet

The first phase in making PoS will be by deploying the Aura pallet. Aura PoA Collator Phase - permissioned block authoring and collator session key setup for Astar ecosystem. After extended testing, we have deployed the PoS pallet and switched to Aura PoS. We have enabled permissionless collator staking, network inflation, and rewards.

**Let’s break down the latest phase:**

* **Collator staking**: collators can now start with staking. This will be with a minimum bond of 32k tokens or be selected to join the first collator set (these are already selected).
* **Network inflation**: 10% inflation will start after this phase 10% per year (7,000,000 native tokens for the first year).
* **Reward**: a fixed amount will be created at each block 2.66 tokens for the first 2,628,000 blocks (block time of 12 seconds) and divided like the following scheme\


![](https://lh3.googleusercontent.com/z-BcHXcOdD9Yy7q5Q93lNsdaGo53uaLX4lVpJdapDiOUcPOjzFC5l2R9wX\_meTHkTYA1RFXHBh8MAnxFfieEbvsB9DWiBkYDsvw7Y65tHk8XzUTnNqczNhrzXftAIdPAe19q6-GT)

A collator (block producer) gets a reward for each block it’s produced. The reward is around 0.266 SDN for each block.

## How to become a collator

### Token balance

To become a collator on one of our networks, you need to know these settings:

**Collator staking parameters/limit:**

{% tabs %}
{% tab title="Astar" %}
**To become a permissionless collator on Astar**

* Bond: 3,200,000 ASTR tokens
* Meet hardware requirements

If your node stops producing blocks for 1 session, your node will be kicked out of the active set.
{% endtab %}

{% tab title="Shiden" %}
**To become a permissionless collator on Shiden**

* Bond: 32,000 SDN tokens
* Meet hardware requirements

If your node stops producing blocks for 1 session, your node will be kicked out of the active set.
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Set your collator with: \
**Extrinsics - CollatorSelection - Register as candidate**

Onboarding takes `n+1` session.
{% endhint %}

### System requirements

A collator usually deploys its nodes on cloud servers. You can choose your preferred VPS service provider and operating system. You need to run Ubuntu 20.04 or higher and we recommend using Azure.

**Hardware requirements:**

Here you can find the basic configuration for reference, which guarantees that all blocks can process in time. If the hardware is inferior to that, there is a chance it will be malfunctioning.

**Recommended configuration:**

{% hint style="info" %}
Make sure you only use your server for running the collator!
{% endhint %}

* System: Linux or macOS, Ubuntu 20.04
* CPU: 8 cores, Intel Core
* Memory: 816 GB
* Hard Disk: 250 GB SSD&#x20;

## How to deploy your node

#### Shibuya network:

{% content-ref url="shibuya-network/shibuya-node.md" %}
[shibuya-node.md](shibuya-network/shibuya-node.md)
{% endcontent-ref %}

#### Shiden network:

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}

## Collator election mechanism

### Election process

When your node fits the parameters and checks all the boxes to become a collator, you will be added to the chain. After registering for a collator and bonded the tokens. **Note: if your collator doesn’t produce blocks during one session (1h) it will be kicked as collator.**

## Collator reward distribution mechanism

At every block you produced as a collator, rewards will automatically be transferred to your account. The reward includes block reward + fees.

## Slash mechanism

At this stage, there is no slash mechanism in place on Shiden Network but if a collator doesn’t produce blocks in one session it will be kicked as a collator in the network.

## FAQ

### What about NPoS?

Our first intention was to activate NPoS to Shiden Network. After internal testing, this would use a lot of Shiden collator resources. NPoS is not designed for collators in the Polkadot ecosystem (see part: role of collators). Astar ecosystem is build to be a dApp hub in the Polkadot ecosystem for smart contracts with a unique incentive reward mechanism for developers, dApp staking. \


### How can users get staking rewards?

Users can nominate smart contracts through dApp staking and earn the same staking rewards as they would on validators. By staking on smart contracts you not only get staking rewards but you support your favorite project that is building in our ecosystem.&#x20;

It’s still possible to stake on collators in our network but this is possible with our partners who build their own nominated system for their collator.
