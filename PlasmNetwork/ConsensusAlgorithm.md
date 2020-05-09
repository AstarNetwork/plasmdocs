# Consensus Algorithm

The Plasm Network changes the consensus algorithm and the reward mechanism step by step to maintain security. Specifically, it initially takes the form of a Proof-of-Authority consensus that is solely maintained by Validators that are selected by the community. However, in the near future we will change the reward mechanism to one that is centered on [collators](https://wiki.polkadot.network/docs/en/maintain-collator) to participate as a [Parachain](https://wiki.polkadot.network/docs/en/learn-parachains). Eventually, we will move to Nominated Proof-o-Stake, which is also used by Polkadot's Relaychain. Please refer to the PLM Token Ecosystem chapter for details on how the rewards are distributed.

## Proof of Authority

Proof of Authority is a consensus-building algorithm that operates only with a validator that is selected by the community. Public blockchains can be vulnerable during early launch as there are very few reliable validators within the network. For this reason, PoA will be operated until a sufficient distribution of token holders and the existence of potential validators can be confirmed. The validator at this time will be paid according to the specified parameters as in the case of PoS.

## Incentives of Collator

Incentives of Collator is an incentive mechanism for operating Collator in a Parachain. The Plasm Network is expected to become a Parachain of Polkadot, therefore, the Network needs a Collator to collect transactions, monitor the transactions in the block and send the block certificate to the Relaychain validator. Collators must be a full node, which is why it is important to incentivize these people for joining Plasm Network as a collator. At first, the Plasm Network Collator is selected by the community, similar to how it works in PoA as mentioned above. After that, the Network will be changed to impalement a election system by NPoS described later. In other words, the node that was acting as a validator function as a Collator while the Plasm Network is a Parachain.

## Nominated Proof of Staking

Plasm Network will use NPoS consensus which is used on the Polkadot relay chain. This consensus algorithm consists of 3 steps.

1. A Nominator selects a validator [NPoS](https://research.web3.foundation/en/latest/polkadot/NPoS/)
2. A validator verifies transactions and make a new block [BABE](https://research.web3.foundation/en/latest/polkadot/BABE/Babe/)
3. Finalize the block that was delivered in the network [GRANDPA](https://research.web3.foundation/en/latest/polkadot/GRANDPA/)

The block reward is distributed to the validator who created the block and his Nominator. In addition to that, the reward is also paid to the Plasm Network contributors as well.
