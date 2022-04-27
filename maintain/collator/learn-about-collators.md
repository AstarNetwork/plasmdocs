# Learn about collators

## Introduction

A collator plays an essential role in our network and is responsible for crucial tasks, including block production and transaction confirmation. A collator needs to maintain a high communication response capability to ensure the seamless operation of the Shiden Network.

Based on network affordability and security considerations, collator seats will gradually open after the launch of Shiden.\


## Role of collators in Astar ecosystem

Collators maintain our ecosystem by collecting transactions from users and producing state transition proofs for Relay Chain validators. In other words, collators maintain the network by aggregating parachain transactions into parachain block candidates and producing state transition proofs for validators based on those blocks. \


Unlike validators, collator nodes do not secure the network. If a parachain block is invalid, it will get rejected by validators. Therefore the assumption that having more collators is better or more secure is not correct. On the contrary, too many collators may slow down the network. The only nefarious power collators have transaction censorship. To prevent censorship, a parachain only needs to ensure some neutral collators - but not necessarily a majority. Theoretically, the censorship problem is solved by having just one honest collator. (reference: [https://wiki.polkadot.network/docs/learn-collator](https://wiki.polkadot.network/docs/learn-collator)).

Performance of the network depends directly of collators:

* A block will not be produced when it is affected to a collator who is offline. It will take 12 extra seconds to attribute this block to the next collator.
* The block filling percentage (ie amount of data included in a block) depends directly on the collator hardware performance. A collator with weak hardware will only fill a small % of the block.

To ensure optimal performance of the network, a [slashing mechanism](learn-about-collators.md#slash-mechanism) is implemented.\


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

A collator usually deploys its nodes on cloud servers. You can choose your preferred operating system, we highly recommend Linux.

**Hardware requirements**

Here you can find the basic configuration for reference, which guarantees that all blocks can process in time. If the hardware is inferior to that, there is a chance it will be malfunctioning and you will be automatically kicked out from the active set.

{% hint style="info" %}
Make sure your server is only dedicated to the collator node
{% endhint %}

**Minimum recommended configuration for a mainnet collator**

* System: Linux (macOS possible)
* Bare Metal server dedicated to the collator node
* CPU: 8 physical cores
* Memory: 16 GB
* Hard Disk: 250 GB SSD NVMe (storage space will increase with time)

## How to deploy your node

#### Shibuya network

{% content-ref url="shibuya-network/" %}
[shibuya-network](shibuya-network/)
{% endcontent-ref %}

#### Shiden and Astar network

{% content-ref url="shiden-collator-guide/" %}
[shiden-collator-guide](shiden-collator-guide/)
{% endcontent-ref %}

## Collator election mechanism

### Election process

When your node fits the parameters and checks all the boxes to become a collator, you will be added to the chain. After registering for a collator and bonded the tokens. **Note: if your collator doesn’t produce blocks during one session (1h) it will be kicked as collator.**

## Collator reward distribution mechanism

At every block you produced as a collator, rewards will automatically be transferred to your account. The reward includes block reward + fees.

## Slash mechanism

Starting April 2022, a slashing mechanism is implemented on Astar and Shiden network: a collator who doesn't produce any block during one session (1 hour) will get slashed by 1% of his total stake and kick out from active collator set.

This slashing aims to ensure the best block rate for the network and prevent malicious actors to harm it without financial consequences.

## FAQ

### What about NPoS?

Our first intention was to activate NPoS to Shiden Network. After internal testing, this would use a lot of Shiden collator resources. NPoS is not designed for collators in the Polkadot ecosystem (see part: role of collators). Astar ecosystem is build to be a dApp hub in the Polkadot ecosystem for smart contracts with a unique incentive reward mechanism for developers, dApp staking. \


### How can users get staking rewards?

Users can nominate smart contracts through dApp staking and earn the same staking rewards as they would on validators. By staking on smart contracts you not only get staking rewards but you support your favorite project that is building in our ecosystem.&#x20;

It’s still possible to stake on collators in our network but this is possible with our partners who build their own nominated system for their collator.
