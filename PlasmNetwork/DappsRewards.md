# dApp Rewards

dApp Rewards is a mechanism that rewards developers or administrators of smart contracts on an ongoing basis. 50% of Plasm Network's Staking reward goes to application developers who have enhanced the value of Plasm Network. The Plasm Network allows you to assign a smart contract administrator to a smart contract, and this administrator is called an "Operator". The user can also take smart contracts. This action is called Nominate, and the person who does it is called dApp Nominator. As shown below, the operator of the smart contract receiving many nominates can receive the newly issued PLM token from the chain.

![dApp_rewards](https://user-images.githubusercontent.com/6259384/76012083-04792e00-5f59-11ea-97a6-0af8e60b8ff0.png)

We will define how to distribute this reward to Operator and Nominator respectively. Define the following variables:

- $$Rewards_{nominate}$$  : The total rewards allocated to Nominator.
- $$Rewards_{contract}$$  : The total rewards allocated to smart contracts.
- $$Rewards_{nominate_{i,j}}$$  : The rewards allocated to the j-th Nomimate fro the i-th smart contract.
- $$Rewards_{contract_i}$$  : The rewards allocated to the operator of the i-th smart contract.
- $$n$$  : The number of smart contract.
- $$m_i$$  : The number of Nominate against the i-th smart contract.
- $$stake_{i,j}$$  : The amount of PLM staked by the j-th Nominate for the i-th smart contract.

Then, $$Nominate_ {i, j}$$  gives the following reward for this stake.

$$Rewards_{nominate_{i,j}}=Rewards_{nominate} \times \frac{\sum_{j}^{m_i}stake_{i,j}}{\sum_i^n\sum_j^{m_i}stake_{i,j}}$$

The nominator can get a reward proportional to the ratio of your stake amount to the total stake amount for the smart contract regardless of the smart contract selected. The operator of $$contract_i$$  who received Stake will get the following reward.

$$Rewards_{contract_i}=Rewards_{contract}\times\frac{stake_{i,j}}{\sum_i^n\sum_j^{m_i}stake_{i,j}}$$

On the other hand, the operator can get a reward proportional to the ratio of the stake of the smart contract owned by oneself to the stake of the smart contract. This creates an incentive for the nominator to stake on smart contracts that would simply increase the value of the token. Operators can also receive semi-permanent rewards by receiving stakes on smart contracts managed by themselves. We hope this will be an innovative solution to the difficult problem of monetizing application developers (administrators) on the chain. 

**Note: The operators and nominators have to wait to receive rewards.**

However, this system can consider the following bad cases:

- **Malicious sock puppet**
    - The problem worthless operator stakes to himself and get rewards.
- **A few popular operators are staked from almost nominators**
    - A few popular operators are oligopoly.

The below writes about counter measures about each.

## Malicious sock puppet

This is the problem hat malicious operators or nominators stake a worthless operator and get rewards.

![malicious](https://user-images.githubusercontent.com/6259384/76012081-03480100-5f59-11ea-8166-1ba4934abbaf.png)

This solves to install the voting system that people they are staking can vote a Good or Bad to each operator. Operators are punished below depending on voting results.

- If an operator receives voting that the number of Good is more than and equal to 4 times as the number of Bad and already has been running over a certain period of time, it is better. So it and nominate to it can normally get rewards. (i.e $$Good \ge Bad \times 4$$)
- If an operator receives voting that the number of Good is less than 4 times as the number of Bad or already has not been running over a certain period of time, it and nominate to it can not get rewards. (i.e $$ Good < Bad \times 4$$)
- **If an operator receives voting that the number of Good is less than 3 times as the number of Bad, the tokens of staking to it are locked. (i.e $$Good < Bad \times 2$$)**
- **If an operator receives voting that the number of Good is less than 3 times as the number of Bad, the tokens of staking to it are slashed. (i.e $$Good < Bad$$)**

Then, you note that a user can vote with Sybil attack. However, a user has to stake his tokens in order to vote. And, voting doesn't make user profits directly. Therefore, while enough honestly users vote, a malicious user can not Sybil attack. Because a malicious user doesn't have incentives.

For example, Alice has 1 million PLM. Alice can make 1 million users and Sybil voting attacks. But, she is better to stake her tokens, but Sybil voting attack. (In actuality, she needs more tokens in order to make 1 million users because of transaction fees.)


## A few popular operators are staked from almost nominators

When Plasmchain installs to the above system, many user stakes to a few operators that they are already stable running. Then the gap between rich and poor is growing. This solution solves the problem.

![option_rewards](https://user-images.githubusercontent.com/6259384/76012067-004d1080-5f59-11ea-8e10-c3097e138202.png)

As shown in the figure, give smart contracts first-mover benefits. Stakes for smart contracts have the option (optional) to get bonus rewards separately. This allows you to exercise your right to receive the following rewards up to r (≥0) days after receiving your Stake reward. Where $$x^k$$  represents $$x$$  at some point $$k$$ . First, introduce the following variables:

- $$Rewards_{optoion^k_{i,j}}$$ : The rewards of getting by exercising an option that can be obtained at the j-th Nominate for the i-th Smart Contract at a certain location $$k$$ .
- $$Rewards_{contract_i}$$ : The reward of the operator of the i-th smart contract when exercising the option.
- $$stake^{k}_{i,j}$$  : The amount of PLM staked by the j-th Nominate for the i-th smart contract at time $$k$$ .
- $$m^k_i$$  : The number of Nominate against the i-th smart contract at time $$k$$ .
- $$p^k_{contract_i}$$  : A coefficient parameter for determining the option reward obtained when nominating the i-th smart contract at time $$k$$ , the operator of the smart contract can be defined.

$$Rewards_{option_{i,j}^{k}}=Rewards_{contract_{i}}\times \frac{stake_{i,j}^k}{\sum^{m_i^k}_jstake_{i,j}^k}\times p^k_{contract_i}$$

Note that $$Rewards_ {contract_i}$$  and "Operator" indicated by $$Rewards_ {option_i ^ {k}}$$  are equal. $$p$$  allows the operator to specify a value less than 0.2.

When this right is exercised, the operator will be able to distribute the reward from Operator at the time of $$p*100$$ % and the share of Stake to the smart contract at the time of $$k$$ . You. Put simply, $$\sum^{m_i^k}_jstake_{i, j} ^ k$$  is the popularity of smart contract $$ i $$  at time $$ k $$ . Increasing the stake for a smart contract while it is low in popularity will increase the option profits that can be obtained when the popularity of the smart contract increases in the future.

When this right is exercised, the reward that the Operator can receive is reduced by that amount. So Operator can control the value $$ p $$ . Operator can specify $$ r $$ , $$ p $$  first.

Note: The limitation about $$r$$  and $$p$$  provides that malicious operator or nominator receives many staking rewards by misusing the system.

For example, An operator Bob was staked 100 PLM at 0 days and $$p=0.1$$ and $$r=200$$. Then Alice staked 50 PLM to Bob. Alice gets a credit that she would get rewards from Bob someday between 100 days after and 200 days after. The amount of the rewards is 0.5 × 0.1 = 0.05 times as the amount of Bob's rewards at that moment in time.
100 days after, Bob received 1000 PLM. Then Alice executed the credit and get 1000 × 0.05 = 50 PLM.

In general, the risk of staking to operators is higher than one of staking to the validator. Because slashing is difficult to predict compared to slash validators. And getting rewards takes more time. Therefore, we add the above incentive systems for operator staking. We think operator staking is advanced. So the ideal percentage of staking is $$Validator:Operateor=4:1$$.

## Trying

You can try [here](https://medium.com/stake-technologies/lets-play-with-plasm-testnet-v3-%E2%91%A1-dApp-rewards-ab6f637ffe4c).