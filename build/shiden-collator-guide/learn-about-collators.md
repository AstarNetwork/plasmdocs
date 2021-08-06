# Learn about collators

## Introduction

A collator plays an essential role in Shiden network and is responsible for crucial tasks, including block production and transaction confirmation. A collator needs to maintain a high communication response capability to ensure the seamless operation of Shiden Network. It is also necessary for them to establish a good reputation in the community to attract more nominators who nominate their $SDN to improve the network’s stability.

Based on network affordability and security considerations, collator seats will gradually open after the launch of Shiden, starting from 32 collators in the first phase. In the future, we aim to have 100 validator seats on Shiden.

Onboarding collators to Shiden Network

* **Phase 0**: collators run by the team. We need to have control to make sure Shiden is running stable before adding other collators.
* **Phase 1**: increase up to 32 collators. These collators will not be added instantly but will increase gradually. During this phase, we will onboard collators from our service partners, early validators on our testnet Dusty and Ambassadors with node experience.
* **Phase 2**: we will increase the collators up to 100.

## Role of collators in Shiden Network

Collators maintain Shiden Network by collecting transactions from users and producing state transition proofs for Relay Chain validators. In other words, collators maintain Shiden Network by aggregating parachain transactions into parachain block candidates and producing state transition proofs for validators based on those blocks. 

**NOTE**:  In our documentation, we will talk about collators and validators. When you have an overall view in the Polkadot ecosystem, your node will run as a collator. In the first part of this documentation we will use the term collators. When we guide you in building your collator, we will use the term validator because in the Astar ecosystem, your node will act as a validator for our staking mechanism set in place. 

Unlike validators, collator nodes do not secure the network. If a parachain block is invalid, it will get rejected by validators. Therefore the assumption that having more collators is better or more secure is not correct. On the contrary, too many collators may slow down the network. The only nefarious power collators have is transaction censorship. To prevent censorship, a parachain only needs to ensure that there exist some neutral collators - but not necessarily a majority. Theoretically the censorship problem is solved with having just one honest collator.

### XCMP

Collators are a key element of [XCMP \(Cross-Chain Message Passing\)](https://wiki.polkadot.network/docs/learn-crosschain). By being full-nodes of the Relay Chain, they are all aware of each other as peers. This makes it possible for them to send messages from parachain A to parachain B.

### Staking

Another role for collators in Shiden is staking. We have two staking mechanisms in place:

* Staking on collators: users can bond their SDN tokens to a collator to earn block rewards.
* dApp Staking: users can nominate a smart contract to earn block rewards. Collators are needed to support this mechanism.

## How to become a collator

### SDN balance

As long as you have SDN, you can become a collator of the Shiden network. However, the elected collator needs to obtain a certain number of $SDN nominations, and the system will select collators according to the ranking of SDN balances \(this is after we switch to NPoS\). 

### System requirements

A collator usually deploys its nodes on cloud servers. You can choose your preferred VPS service provider and operating system. We recommend Ubuntu 18.04 and Azure.

**Hardware requirements:**

Shiden will provide a basic configuration for reference, which guarantees that all blocks can process in time. If the hardware is inferior to that, there is a chance it will be malfunctioning.

**Basic configuration:**

* System: Linux or macOS, Ubuntu 18.04 is recommended
* CPU: at least 2 cores, Intel Core
* Memory: at least 8 GB
* Hard disk: at least 120 GB, regularly evaluated

**Recommended configuration:**

* System: Linux or macOS, Ubuntu18.04
* CPU: 4 cores, Intel Core
* Memory: 8-16 GB
* Hard Disk: 250 GB

## How to deploy your node 

{% page-ref page="become-a-collator.md" %}

## Validator election mechanism

### Election process

In an era \(24 hours\), the Shiden Network will lock the data in the last 15 minutes of the fifth epoch. Then, the nominators will not be able to nominate. When the sixth epoch begins, the system will rank the collators nominated SDN and select top validators for the next era. Those who successfully nominated to selected validators will be rewarded in the next era.  


![Polkadot wiki - https://wiki.polkadot.network](https://lh6.googleusercontent.com/ntn7pHijyAtI9bP-yuLuNpItKE1RQrjiq-08xAf6pSzeldvpKctdZOobKQ0zmyC9ZZRB1FFixzhdEBrCazmj9q5SkQY_pRumnPCdz2aFGov23pUzcQfdHBE2JS4Fg2cyX8U9M5h8)

### Withdrawal

Withdrawal refers to the behavior of removing a validator from the incumbent ones in the next [NPoS](https://medium.com/web3foundation/how-nominated-proof-of-stake-will-work-in-polkadot-377d70c6bd43) cycle.  
Withdrawal means to withdraw from the incumbent validators and no longer produce blocks or confirm transactions. Those who nominated them will not be rewarded.

There are two cases of withdrawal:

* Voluntary withdrawal by the collator. For example, there are some problems with the collator’s server hosting provider, so the collator may choose to withdraw to avoid being slashed. When the request is submitted, it will affect the next epoch, and the collator will become inactive then. However, the SDN nominated for the validator is still there.
* When the validator does some actions that harm the operation of the system, they will be 'expelled' as a punishment. It will take effect immediately in the current epoch. The SND nominated to the validator will be automatically distributed to other validators.

## Validator reward distribution mechanism

In the Shiden network, the system records each validator's rewards in an epoch cycle and issues rewards in an era cycle. A collator can claim rewards when an era ends. 

When a collator claims the rewards, part of them will be distributed to their nominator\(s\) according to the protocol by the ratio set in advance. 

**Note**: If the reward is not claimed within 84 Era \(84 days\), it will be destroyed. So please do not forget to claim!

Suppose the collective reward for collator is 10 SDN. If a collator sets commission 'collator\_payment = 40%', it will receive 4 SND, and the remaining 6 SDN will be distributed to nominators by the amount of SDN they used to nominate. If the validator itself pledged SDN, it would also get a portion from that 6 SDN. That can be understood as the collator nominated itself. The reward can be sent to the Stash account or Controller. A collator can choose to continue to pledge their rewards back or not.

## Slash mechanism

### Offline/not responding

If the validator does not produce any block or send an online signal in an Era, it will be marked as offline/not responding. When there is a certain number of offline/unresponsive nodes, the system will begin to confiscate part of the pledged SDN in the verification pool of the bad-behaving validator to ensure the normal operation of the network. Some of the SDN in that pool are from nominators.

In general, the minimum ratio of slash is 0 and the maximum is 7%. When less than 10% of all nodes are offline, a node will not be slashed if it is offline or unresponsive. When 1/3 of the nodes are offline at the same time, slash ratio is close to 5%.

### Double signature

In the block-production stage \(Babe consensus\) and voting stage \(Grandpa consensus\), voting on different chains in a single round or generating two new blocks at the same height will be deemed evil to protect systemic security.

In general, the penalty for double signature is much more serious than offline. The largest slash ratio is 1, which means that the validator may be fined all of their stake.  
  


