# First Rewards Guide

**TO BE REVIEWED**

[日本語版はこちら](https://medium.com/stake-technologies/plasm-first-upgrade-%E3%83%90%E3%83%AA%E3%83%87%E3%83%BC%E3%82%BF%E5%A0%B1%E9%85%AC%E3%81%AE%E8%BF%BD%E5%8A%A0%E3%81%AB%E3%81%A4%E3%81%84%E3%81%A6-b900e47dec73)

### Purpose

We target our number of validators to be anywhere around 100 nodes. There are two major reasons for this decision. First, during the early stages of our main net, the network will have a Proof-of-Authority consensus algorithm, which does not require a large number of validators. The second reason is that 100 nodes is the most sufficient number for us to safely transition our consensus algorithm to Nominated Proof-of-Stake. Our benchmark source is from [https://telemetry.polkadot.io/](https://telemetry.polkadot.io/). Because we want to maintain a certain number of validators, it is essential to create an effective reward system for the validators, which we will be discussing throughout this article. Please note that our Mainnet will apply these features from the beginning of the launch! If you want to be a validator, you can start your journey from our [Validator Guide](../PlasmTestnet/ValidatorGuide.md).

### Algorithm

![first\_rewards](https://user-images.githubusercontent.com/6259384/80910872-7f01d680-8d6d-11ea-84eb-56d27f7b0a26.jpeg)

At genesis, Plasm will use all of the rewards for `ForSecurity`. Performing Dapps Staking in the initial phase will definitely make it rough. Furthermore, countermeasures for malicious actors may not work perfectly as intended. Therefore, at genesis Plasm will adopt a simple reward algorithm.

The target maximum token supply inflation rate per year is $$I \le I_0 = 2.5\%$$

$$I_0$$ is the minimum token supply that should be paid to the block validators to ensure a sufficient number of validators \(here, we assume the sufficient number of validators is 100\). This figure was borrowed from the numbers defined in the Polkadot Ecosystem. Furthermore, this value will be equivalent to the validator rewards when there are 0 Stakes in a NPoS consensus.

Validator compensation per Era is strictly defined as the following. First, we define the meaning of each variable. `TotalForSecurityRewards` is the total amount of compensation paid for the validator. `TotalAmountOfIssue` is the total number of PLM tokens issued by Plasm Network. $$I_0$$ is the minimum token supply that should be paid to the validators to ensure a sufficient number of nodes are interested. `EraDuration` is the length of duration of the Era. `NumberOfValidators` is the actual number of validators in the Network. `TargetsNumber` is 100 that is the sufficient number of validators.

If $$TargetsNumber < NumberOfValidators$$ then:

$$TotalForSecurityRewards = TotalAmountOfIssue \times I_0\% \times \frac{EraDuration}{1year}$$

Else:

$$TotalForSecurityRewards = TotalAmountOfIssue \times I_0\% \times \frac{NumberOfValidators}{TargetsNumber} \times \frac{EraDuration}{1year}$$

Therefore, the reward for each Validator will be:

$$ForSecurityRewards_{validator_i}= \frac{TotalForSecurityRewards}{NumberOfValidators}$$

And that would be the summary of how validators will be rewarded in Dusty and mainnet at genesis

