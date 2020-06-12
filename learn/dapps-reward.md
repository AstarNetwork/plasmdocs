# dApps Rewards 🍭

dApps Rewards is a reward mechanism for developers or administrators of smart contracts. 50% of Plasm Network's staking reward goes to application developers who have enhanced the value of the Plasm Network. Plasm allows the assignment of a smart contract administrator, called an "operator." "Operators" can be "Nominated" by other dApps "Nominators." As shown below, the operator of the smart contract receiving many nominations can receives newly minted PLM token from the chain.

![](../.gitbook/assets/sukurnshotto-2020-05-31-195848png.png)

Operator and Nominator reward algorithms, respectively. Define the following variables:

* $$Rewards_{nominate}$$ : The total rewards allocated to Nominator.
* $$Rewards_{contract}$$ : The total rewards allocated to smart contracts.
* $$Rewards_{nominate_{i,j}}$$ : The rewards allocated to the j-th Nominate for the i-th smart contract.
* $$Rewards_{contract_i}$$ : The rewards allocated to the operator of the i-th smart contract.
* $$n$$ : The number of smart contract.
* $$m_i$$ : The number of Nominate against the i-th smart contract.
* $$stake_{i,j}$$ : The amount of PLM staked by the j-th Nominate for the i-th smart contract.

Then, $$Nominate_ {i, j}$$ gives the following reward:

$$Rewards_{nominate_{i,j}}=Rewards_{nominate} \times \frac{\sum_{j}^{m_i}stake_{i,j}}{\sum_i^n\sum_j^{m_i}stake_{i,j}}$$

The nominator can get a reward proportional to the ratio of their stake amount to the total stake amount for the smart contract nominated. The operator of $$contract_i$$ will receive the following rewards:

$$Rewards_{contract_i}=Rewards_{contract}\times\frac{stake_{i,j}}{\sum_i^n\sum_j^{m_i}stake_{i,j}}$$

Also, the operator can get a reward proportional to the ratio of the stake of the smart contract owned by oneself to the stake of the smart contract. This creates an incentive for the nominator to stake on smart contracts that would simply increase the value of the token. Operators can also receive semi-permanent rewards by receiving stakes on smart contracts managed by themselves. This is one solution to the difficult problem of monetizing application developers \(administrators\) on the chain.

{% hint style="info" %}
**The operators and nominators have to wait to receive rewards.**
{% endhint %}


