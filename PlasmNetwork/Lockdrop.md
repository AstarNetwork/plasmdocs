# Lockdrop

[Lockdrop](https://blog.edgewa.re/full-details-on-the-edgeware-lockdrop) is a new low-risk economic incentivization mechanism, where it uses opportunity costs rather than legal tender (or assets) as collateral. Plasm Network uses this mechanism to issue tokens with monetary value. Throughout this section, we will explain Plasm Network's token issuance mechanism. The concept of a lockdrop was first conceived by Edgeware, and the one used for Plasm Network is an expansion of its original mechanism. The native token used in the Plasm Network is written PLM and pronounced as "plum". PLM will only calculate from the 15th decimal place and truncate any numbers below that. For more information regarding the role of the Token, please refer to the PLM Token Economics section.

## Lockdrop Overview

For our first lockdrop, we will be using Ethereum's opportunity cost. Therefore, further sections will make the assumption that the locked token is ETH. However, lockdrop itself is an algorithm that can be implemented to any chains that support TimeLock and is not limited to Ethereum. The below Figure shows an example of how the lockdrop will work on the Plasm Network.

![Lockdrop](https://user-images.githubusercontent.com/6259384/75602291-16953f80-5b07-11ea-9944-311e066f6f21.png)

A lockdrop will work by the following process.

1. Ethereum token holder will send the number ETH locking, and the duration of the lock as a transaction to the LockContract that resides within the Ethereum blockchain.
2. For every token holders who participated in the lockdrop, the number of PLM calculated by `total locked ETH × Lock bonus per duration × α` will be recorded on the Plasm Network genesis block.
3. The Plasm Team will take `total issued amount × 15%` PlasmTokens from the genesis block.
4. Once the lock duration that the token holder specified has passed, the exact number lock ETH will be returned back to the participant after the lockdrop.

Our assumption is that the Ethereum token holder's opportunity cost is proportional to the number of tokens locked and the duration of the lock. PlasmToken is able to generate value via using those opportunity costs as collateral. Furthermore, the final token supply is not decided. This is to ensure fairness to tokens issued from post-genesis lockdrops. 15% of the total tokens circulating from the lockdrop will go to the Plasm team as part of the development fee. To elaborate, the tokens will be distributed multiple times via the following method.

## Multi-Lockdrop

Multi-Lockdrop is a mechanism in which we repeat the aforementioned lockdrop multiple times. Plasm Network will do this in a total of 3 times. Because of this, Plasm Network's total token supply will not be made concrete at genesis. Tokens will be issued every 3rd lockdrop, and additional tokens will be used via utilizing the "Staking" function, which will be later explained in detail.

There are two main reasons why we have decided to divide the lockdrop into multiple times. First, is to prevent uneven token distribution, as if the number of early bird participants was low, it is possible that there might be someone who holds the majority of the total supply. Furthermore, if we commence a rollback to the previous block state to fix this issue, the integrity of the network itself may be damaged. In a blockchain, it is important to establish a rule before the launch, we must avoid any situation in which we go against the predefined rules. To solve this problem, we have developed an algorithm that does not define the total token supply at genesis. The second reason is to create room for experiments so that the team can ensure that the Plasm Network can scale and be decentralized without any hiccups. The strong security and integrity of a blockchain rely on the distribution of nodes and token holders. It is not desirable to hold the security after the official launch at Stake. With this, repeating the lockdrop three times allows us to understand the distribution of tokens amongst the holders beforehand, which also leads to reducing maintenance costs for fixing these issues and preventing any risks that are followed by such a fix. This aligns with our goal of making Plasm Network a complete public blockchain.

Furthermore, Plasm Network will accept the following tokens for the 1st, 2nd and 3rd lockdrop.

- 1st: ETH
- 2nd: ETH, BTC
- 3rd: ETH, BTC, DOT

### Defenitions

We define the amount of distributed PLM (TotalPLM^{genesis}) from the first lockdrop to be as the following.

$$TotalPLM^{genesis} = 500,000,000$$

The total amount will be distributed to the lockdrop participants in accordance with the token issue rate (IssueRatio). The IssueRatio is proportional to the number of locked tokens, the exchange rate in dollars  $$ DollarRate_{token} $$  of the locked tokens at the time of the lockdrop and the number of days multiplied by 1.0005 to the power of days  $$ Days * 1.0005^{Days} $$ . The value of 1.0005 is based on Polkadot's interest rate. To elaborate, by default, Polkadot defines its maximum average annual interest rate to be 20% ([reference](https://research.web3.foundation/en/latest/polkadot/Token%20Economics.html)). Converting this into daily interest rates with compound interest gives us an approximate value of 0.05%.

The users have the option to choose the lockdrop duration from the following 4 + 1 options. The $$ IssueRatio $$ will be determined by the duration fo the lock which comes directly after evaluating the value of the locked tokens in Dollars.

![LockdropTable](https://user-images.githubusercontent.com/6259384/75602324-6d9b1480-5b07-11ea-9501-576eaefd155f.png)

※ The 2 years option is only available for locking DOT tokens. Furthermore, the DOT lockdrops are special in that they are only allowed to lock for 2 years. More information can be found from the **Polkadot auctions Lockdrop** section.

Based on the aforementioned information, the IssueRatio will be defined as the following.

- $$Locked_{token}$$ is the number of locked tokens for the lockdrop
- $$DolalrRate_{token}$$ is the value for 1 token in Dollars
- $$LockBonus_{days}$$ is the amount of bonus the user will receive according to the locked days

$$ IssueRatio = Locked_{token} \times DollarRate_{token}\times LockBonus_{days}  (token \in \{ETH,BTC,DOT\}) $$

The number of tokens to be got who Lockdrop participant has is determined based on the calculated IssueRatio. The algorithm for determining the token distribution amount is as follows. 

- $$n$$ is the number of Lockdrop participant.
- $$IssueRatio_i$$ is $$ IssueRatio $$ for user $$i$$.
- We define 15% (3/20) of the total issued tokens as development costs we hold.
- $$PLM_i$$ is the amount of tokens user $$i$$ can get.

$$PLM_{i}=TotalPLM^{genesis} \times \frac{17}{20} \times \frac{IssueRatio_i}{\sum_{j=0}^{n}IssueRatio_j}$$

In other words, PLM will be distributed by the ratio of your $$ IssueRatio $$ to the total $$ IssueRatio $$  At this time, 75,000,000 PLM, which is 3/20 as development cost, will be used. Here, we define $$ TotalIssueRatio $$  which is the sum of $$ IssueRation $$ 

$$TotalIssueRatio=\sum^{n}_{j=0}{IssueRatio_j}$$

Also, $α_1$ is the amount of PLM issued per unit $$ IssueRatio $$ in the first Lockdrop. This is an important value to determine the amount of PLM issued in the second and subsequent Lockdrops.

$$\alpha_1 = \frac{PLM_{i}}{IssueRatio_i} = TotalPLM^{genesis} \times \frac{17}{20} \times \frac{1}{TotalIssueRatio}$$

Define the number of PLM issues per unit $$ IssueRatio $$ for the second and third times to satisfy a_2 and a_3 the following equation.

$$\alpha_1:\alpha_2:\alpha_3 = 6:5:4$$

From the above, the amount of PLM distributed to the second and third user $$i$$ is as follows.

$$\alpha_j \times IssueRatio_i\:\:\:\:(j=2,3)$$

This allows the user to get the amounts of tokens proportional to $$ IssueRatio $$ on the second and subsequent Lockdrops. This solves the problem that if a large number of users do Lockdrop after the first Lockdrop, the amount of PLM that users can get will be excessively small relative to the overall ratio.

The following the below figure shows an example of how the amounts of tokens distribution changes in multiple Lockdrops. Here, $$ DollarRate $$ is fixed.

![MultiLockdrop](https://user-images.githubusercontent.com/6259384/75602454-ac7d9a00-5b08-11ea-80a1-d3e697f1c776.png)

### Why issue Lockdrop tokens?

- We do not hold the assets of the Lockdrop user.
- Users do not need to consider the risk of stealing assets by scammers. Issue a PLM with the opportunity cost as collateral. Assets locked by the user will return after the Lock period has expired.
- Users can join Lockdrop at a low cost. Anyone who can run a smart contract can participate in Lockdrop. All token holders have the opportunity to participate.
- Unlike Airdrop, Lockdrop participants pay a cost to get a PLM. You can issue tokens with a non-zero value.

### Why split Lockdrop multiple times?

- If all PLMs are issued on the first Lockdrop, a small number of token holders may own a huge amount of PLM. If you do, there is a risk that a healthy ecosystem will not work. Prevent excessive first-mover benefits.
- Users can increase their chances of acquiring tokens by performing multiple Lockdrops. Allow more people to earn a PLM.

## Real-Time Lockdrop

Real-Time Lockdrop is a mechanism for 2-nd and 3-rd Lockdrop in Multi-Lockdrop described in the previous chapter. In 1-st Lockdrop, after the period, tokens are issued at once in the Genesis block. Real-Time Lockdrop allows you to get a PLM token immediately after you lock during the Lockdrop period. The details are [here](https://docs.plasmnet.io/PlasmNetwork/RealtimeLockdrop.html).

## Polkadot auctions Lockdrop

Polkadot auctions Lockdrop means the Lockdrop using DOT described in the previous chapter. It is independent and distinct from 1-st, 2-nd, and 3-rd Lockdrop. DOT at Polkadot has some roles. Some of the important roles are staking and Parachain deposit. Staking is used in the NPoS consensus algorithm to secure the chain. Parachain deposit is depositing a DOT for a certain period to join as Parachain on Polkadot. Parachain means a blockchain that connects to Polkadot. By becoming a Parachain it can borrow Polkadot's validator and share security and get Interoperability with other Parachains by using [XCMP](https://research.web3.foundation/en/latest/polkadot/networking/4-xcmp.html).

Polkadot auctions Lockdrop uses Parachain deposit. Locked DOT will be used to deposit Plasm Network into Parachain. The lock period of DOT expects about two years, during which Plasm Network operates as Parachain. Keep in mind that this Lockdrop can fail because the decision to join Parachain is made at auction. If unsuccessful, DOT will be returned without being locked and PLM will not be got. If successful, DOT is locked and you can get PLM tokens. The below figure shows the procedure of Lockdrop in Polkadot.

![PolkadotLockdrop](https://user-images.githubusercontent.com/6259384/75602519-84426b00-5b09-11ea-9551-1608c947bb20.png)

This system uses the [crowdfund module](https://github.com/paritytech/polkadot/blob/master/runtime/common/src/crowdfund.rs). Also, note that the DOT will not be available during the auction too and it may fail. Because of this, there is a certain risk compared to other Lockdrops, and the LockBonus of Lockdrop by DOT is the highest. (Refer to Multi-lockdrop in the previous chapter)

Plasm Network's Lockdrop cost design is based on the cost of DOT Lockdrop. The cost performance of Lockdrop can be calculated by benchmarking DOT Lockdrop and DOT Staking which is a trade-off relationship.

## Lockdrop Affiliate Program

The Lockdrop Affiliate Program is a program made to incentivize those who have shared any information regarding Plasm Network to their peers. Via the affiliate program, participants of the Lockdrop will be able to receive PLM tokens with a bonus rate. In this section, we will discuss the mechanism of the 1st Lockdrop affiliate program.

The affiliate program mainly has these three rules:

- Any participants can reference their introducer’s Ethereum public address (this is optional for the lockdrop)
- Given that the referenced introducer’s address is valid, the token issuing rate for the address being referenced will gain an additional 1% of the participant’s issuing PLMs.
- Any participants who have referenced a valid introducer will receive another 1% increase in their initial PLMs.

The PLM given as a bonus is allocated in from the tokens held by the community of Plasm Network (15% of the total). The method of becoming a valid introducer is released in the [Plasm Network’s Discord server](https://discord.gg/Dnfn5eT). Furthermore, the valid introducers for the 2nd and 3rd lockdrop will be pooled from the participants of the 1st lockdrop. The details are [here](https://medium.com/stake-technologies/lockdrop-with-friends-the-plasm-network-affiliation-program-b385c1cd800d).

## Unlocking Tokens

Lockdrop's Lock Contract contains the following anonymous function.

    /**
    * @dev Withdraw function once timestamp has passed unlock time
    */

    function () external payable {
     assembly {
      switch gt(timestamp, sload(0x01))
      case 0 { revert(0, 0) }
      case 1 {
       switch call(gas, sload(0x00), balance(address), 0, 0, 0, 0)
      case 0 { revert(0, 0) }
      }
     }
    }

This enables the contract to return the locked balance to the original token locker's address by sending an empty transaction to this contract address.
However, the timestamp of the transaction must be greater than the timestamp of the lock including the lock duration.
When someone sends a transaction before the duration of the locks is passed, the transaction will return a error.
Sending a transaction to the lock (i.e. unlocking the tokens) can be done by anyone given that they have enough funds to pay for the transaction fee.
But the the locked tokens will only return to the original locker rather than the address that sent the transaction.
So it is possible to allow another address to unlock the locked token on behalf of the original locker, but they cannot claim the tokens for themselves.
One minor inconvenience that this contract has is that once the lock duration is over, the contract will act as a normal contract without any transaction rejections, meaning even if the token was returned to the original locker, anyone can still send a transaction to the contract without any errors.
Once the token is claimed it will not be able to return any more tokens, but it makes it hard for the original locker to check if the tokens were unlocked or not without comparing their post-unlock wallet balance, effectively giving a potential issue of wasting transaction fee for attempting to claim the locked tokens that was already unlocked.

![unlock image](https://user-images.githubusercontent.com/40356749/77284164-608dd180-6d11-11ea-83e5-464b63b45b0f.jpg)

The Lockdrop Web Application comes with an intuitive form that displays any lock information.
Under the `Unlock Tokens` tab, it will display a list of locks that was locked by the current address in a Web3 enabled browser wallet extension.
Once the lock duration is over, the lock icon on the right will change to a lighter color.
Clicking this icon will allow you to send to transaction of 0 ETH to the lock address, unlocking the tokens.
This form allows you to easily check the lock information, time until the lock is over and unlock once it is over.
However, as mentioned above, it is hard to check if the lock has been already claimed or not, so even if the locks were successfully claimed, the UI elements will still look the same.
