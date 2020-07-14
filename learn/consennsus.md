# Consensus 🎬

The [Plasm Network](https://www.plasmnet.io/) changes consensus algorithms and reward designs step by step to maintain security. Specifically, it initially takes the form of a Proof of Authority that is run solely by Validators selected by the community. 

Next, we will change to rewards centered on [collator](https://wiki.polkadot.network/docs/en/maintain-collator) to participate as [Parachain](https://wiki.polkadot.network/docs/en/learn-parachains). Eventually, we will move to NPoS, which is also used by Polkadot's Relaychain. Please refer to the PLM Token Ecosystem chapter for details on how to distribute rewards.

{% page-ref page="token-economy.md" %}

## Proof of Authority

Proof of Authority is a consensus-building algorithm that operates only with a validator selected by the community. Public blockchains can be vulnerable when few are launching reliable validators. For this reason, PoA will be operated until a sufficient distribution of token holders and the existence of potential validators can be confirmed. The validator at this time will be paid according to the specified parameters as in the case of PoS.

## Nominated Proof of Staking

[Plasm Network](https://www.plasmnet.io/) uses NPoS which is used on the Polkadot relay chain. This consensus algorithm consists of 3 steps.

1. A Nominator selects a validator [NPoS](https://research.web3.foundation/en/latest/polkadot/NPoS/)
2. A validator verifies transactions and make a new block [BABE](https://research.web3.foundation/en/latest/polkadot/BABE/Babe/)
3. Finalize the block that was delivered in the network [GRANDPA](https://research.web3.foundation/en/latest/polkadot/GRANDPA/)

The block reward is distributed to the validator who created the block and his/her Nominator. In addition to that, the reward is also paid to the [Plasm Network](https://www.plasmnet.io/) contributors as follows.



