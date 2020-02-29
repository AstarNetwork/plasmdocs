# Consensus Algorithm

Plasm Network uses NPoS which is used on the Polkadot relay chain. This consensus algorithm consists of 3 steps.

1. A Nominator selects a validator [NPoS](https://research.web3.foundation/en/latest/polkadot/NPoS/)
2. A validator verifies transactions and make a new block [BABE](https://research.web3.foundation/en/latest/polkadot/BABE/Babe/)
3. Finalize the block that was delivered in the network [GRANDPA](https://research.web3.foundation/en/latest/polkadot/GRANDPA/)

The block reward is distributed to the validator who created the block and his Nominator. In addition to that, the reward is also paid to the Plasm Network contributors as follows.