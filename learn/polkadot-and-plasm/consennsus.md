# Consensus

![](../../.gitbook/assets/undraw_business_deal_cpi9-1-.png)

To increase security, the [Plasm Network](https://www.plasmnet.io/) will have consensus and reward algorithm upgrades over time. Plasm will start using a Proof of Authority model run by community selected validators.

The next upgrade will change reward and consensus to [collator](https://wiki.polkadot.network/docs/en/maintain-collator) which is a [Parachain](https://wiki.polkadot.network/docs/en/learn-parachains) requirement. Ultimately Plasm will move to NPoS which is used by Polkadot's Relaychain. More details about reward distribution can be found in the PLM Token Ecosystem chapter.

{% page-ref page="../token-economics/token-economy.md" %}

## Proof of Authority

Proof of Authority is a consensus-building algorithm that operates only with a validator selected by the community. Public blockchains can be vulnerable when there are a low amount of reliable validators. For this reason, PoA will operate until sufficient token distribution and potential validators can be confirmed. The validator reward structure will follow PoS convention.

## Nominated Proof of Staking

[Plasm Network](https://www.plasmnet.io/) uses NPoS a Polkadot relay chain feature. This consensus algorithm consists of 3 steps:

1. A Nominator selects a validator [NPoS](https://research.web3.foundation/en/latest/polkadot/NPoS/)
2. A validator verifies transactions and makes a new block [BABE](https://research.web3.foundation/en/latest/polkadot/BABE/Babe/)
3. Validator finalizes the block that was delivered in the network [GRANDPA](https://research.web3.foundation/en/latest/polkadot/GRANDPA/)

The block reward is distributed to the validator who created the block and the respective Nominator. A reward is also paid to the [Plasm Network](https://www.plasmnet.io/) contributors.

