# Lockdrop 🔒

## For Lockdrop participants, you can claim PLM token from 👇

[https://lockdrop.plasmnet.io/\#/lock-form](https://lockdrop.plasmnet.io/#/lock-form)

## Introduction

[Lockdrop](https://blog.edgewa.re/full-details-on-the-edgeware-lockdrop) is a new low-risk economic incentivization mechanism, where it uses opportunity costs rather than legal tender \(or assets\) as collateral. [Plasm Network](https://www.plasmnet.io/) uses this mechanism to issue tokens with monetary value. Throughout this section, we will explain [Plasm Network](https://www.plasmnet.io/)'s token issuance mechanism. The concept of a lockdrop was first conceived by [Edgeware](https://edgewa.re/), and the one used for [Plasm Network](https://www.plasmnet.io/) is an expansion of its original mechanism. The native token used in the [Plasm Network](https://www.plasmnet.io/) is written PLM and pronounced as "PLUM". PLM will only calculate from the 15th decimal place and truncate any numbers below that. For more information regarding the role of the Token, please refer to the PLM Token Economics section.

## Lockdrop Overview

For our first lockdrop, we will be using Ethereum's opportunity cost. Therefore, further sections will make the assumption that the locked token is ETH. However, lockdrop itself is an algorithm that can be implemented to any chains that support TimeLock and is not limited to Ethereum. The below Figure shows an example of how the lockdrop will work on the [Plasm Network](https://www.plasmnet.io/).

![Lockdrop](https://user-images.githubusercontent.com/6259384/75602291-16953f80-5b07-11ea-9944-311e066f6f21.png)

A lockdrop will work by the following process.

1. Ethereum token holder will send the number ETH locking, and the duration of the lock as a transaction to the LockContract that resides within the Ethereum blockchain.
2. For every token holders who participated in the lockdrop, the number of PLM calculated by `total locked ETH × Lock bonus per duration × α` will be recorded on the [Plasm Network](https://www.plasmnet.io/) genesis block.
3. The Plasm Team will take `total issued amount × 15%` PlasmTokens from the genesis block.
4. Once the lock duration that the token holder specified has passed, the exact number lock ETH will be returned back to the participant after the lockdrop.

Our assumption is that the Ethereum token holder's opportunity cost is proportional to the number of tokens locked and the duration of the lock. PLM is able to generate value via using those opportunity costs as collateral. Furthermore, the final token supply is not decided. This is to ensure fairness to tokens issued from post-genesis lockdrops. 15% of the total tokens circulating from the lockdrop will go to the Plasm team as part of the development fee. To elaborate, the tokens will be distributed multiple times via the following method.

## Multi-Lockdrop

Multi-Lockdrop is a mechanism in which we repeat the aforementioned lockdrop multiple times. [Plasm Network](https://www.plasmnet.io/) will do this in a total of 3 times. Because of this, [Plasm Network](https://www.plasmnet.io/)'s total token supply will not be made concrete at genesis. Tokens will be issued every 3rd lockdrop, and additional tokens will be used via utilizing the "Staking" function, which will be later explained in detail.

{% page-ref page="dapps-reward.md" %}

There are two main reasons why we have decided to divide the lockdrop into multiple times.

First, is to prevent uneven token distribution, as if the number of early bird participants was low, it is possible that there might be someone who holds the majority of the total supply. Furthermore, if we commence a rollback to the previous block state to fix this issue, the integrity of the network itself may be damaged. In a blockchain, it is important to establish a rule before the launch, we must avoid any situation in which we go against the predefined rules. To solve this problem, we have developed an algorithm that does not define the total token supply at genesis. 

The second reason is to create room for experiments so that the team can ensure that the [Plasm Network](https://www.plasmnet.io/) can scale and be decentralized without any hiccups. The strong security and integrity of a blockchain rely on the distribution of nodes and token holders. It is not desirable to hold the security after the official launch at Stake. With this, repeating the lockdrop three times allows us to understand the distribution of tokens amongst the holders beforehand, which also leads to reducing maintenance costs for fixing these issues and preventing any risks that are followed by such a fix. This aligns with our goal of making [Plasm Network](https://www.plasmnet.io/) a complete public blockchain.

Furthermore, Plasm Network will accept the following tokens for the 1st, 2nd and 3rd lockdrop.

* 1st: ETH
* 2nd: ETH, BTC
* 3rd: ETH, BTC, DOT

### Definitions

We define the amount of distributed PLM \( $$TotalPLM^{genesis}$$ \) from the first lockdrop to be as the following.

$$
TotalPLM^{genesis} = 500,000,000
$$

The total amount will be distributed to the lockdrop participants in accordance with the token issue rate \(IssueRatio\). The IssueRatio is proportional to the number of locked tokens, the exchange rate in dollars $$DollarRate_{token}$$ of the locked tokens at the time of the lockdrop and the number of days multiplied by 1.0005 to the power of days $$Days * 1.0005^{Days}$$ . The value of 1.0005 is based on Polkadot's interest rate. To elaborate, by default, Polkadot defines its maximum average annual interest rate to be 20% \([reference](https://research.web3.foundation/en/latest/polkadot/Token%20Economics.html)\). Converting this into daily interest rates with compound interest gives us an approximate value of 0.05%.

The users have the option to choose the lockdrop duration from the following 4 + 1 options. The $$IssueRatio$$ will be determined by the duration fo the lock which comes directly after evaluating the value of the locked tokens in Dollars.

![LockdropTable](https://user-images.githubusercontent.com/6259384/75602324-6d9b1480-5b07-11ea-9501-576eaefd155f.png)

{% hint style="info" %}
The 2 years option is only available for locking DOT tokens. Furthermore, the DOT lockdrops are special in that they are only allowed to lock for 2 years. More information can be found from the **Polkadot auctions Lockdrop** section.
{% endhint %}

Based on the aforementioned information, the IssueRatio will be defined as the following.

* $$Locked_{token}$$ is the number of locked tokens for the lockdrop
* $$DolalrRate_{token}$$ is the value for 1 token in Dollars
* $$LockBonus_{days}$$ is the amount of bonus the user will receive according to the locked days

$$IssueRatio = Locked_{token} \times DollarRate_{token}\times LockBonus_{days} (token \in \{ETH,BTC,DOT\})$$

The number of tokens to be got who Lockdrop participant has is determined based on the calculated IssueRatio. The algorithm for determining the token distribution amount is as follows.

* $$n$$ is the number of Lockdrop participant.
* $$IssueRatio_i$$ is $$IssueRatio$$ for user $$i$$.
* We define 15% \(3/20\) of the total issued tokens as development costs we hold.
* $$PLM_i$$ is the amount of tokens user $$i$$ can get.

$$PLM_{i}=TotalPLM^{genesis} \times \frac{17}{20} \times \frac{IssueRatio_i}{\sum_{j=0}^{n}IssueRatio_j}$$

In other words, PLM will be distributed by the ratio of your $$IssueRatio$$ to the total $$IssueRatio$$ At this time, 75,000,000 PLM, which is 3/20 as development cost, will be used. Here, we define $$TotalIssueRatio$$ which is the sum of $$IssueRation$$

$$TotalIssueRatio=\sum^{n}_{j=0}{IssueRatio_j}$$

Also, $$α_1$$ is the amount of PLM issued per unit $$IssueRatio$$ in the first Lockdrop. This is an important value to determine the amount of PLM issued in the second and subsequent Lockdrops.

$$\alpha_1 = \frac{PLM_{i}}{IssueRatio_i} = TotalPLM^{genesis} \times \frac{17}{20} \times \frac{1}{TotalIssueRatio}$$

Define the number of PLM issues per unit $$IssueRatio$$ for the second and third times to satisfy $$α_2$$ and $$α_3$$ the following equation.

$$\alpha_1:\alpha_2:\alpha_3 = 6:5:4$$

From the above, the amount of PLM distributed to the second and third user $$i$$ is as follows.

$$\alpha_j \times IssueRatio_i\:\:\:\:(j=2,3)$$

This allows the user to get the amounts of tokens proportional to $$IssueRatio$$ on the second and subsequent Lockdrops. This solves the problem that if a large number of users do Lockdrop after the first Lockdrop, the amount of PLM that users can get will be excessively small relative to the overall ratio.

The following the below figure shows an example of how the amounts of tokens distribution changes in multiple Lockdrops. Here, $$DollarRate$$ is fixed.

![MultiLockdrop](https://user-images.githubusercontent.com/6259384/75602454-ac7d9a00-5b08-11ea-80a1-d3e697f1c776.png)

