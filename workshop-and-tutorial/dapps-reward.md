# dApp Reward 🍦

## Preparation


Like in the previous tutorial, deploy a smart contract. In the sidebar press dAppStaking; it should show like the following. 


{% page-ref page="operator-trading.md" %}

![Dapps Staking Board](../.gitbook/assets/screen-shot-2020-06-11-at-16.26.00.png)

## The concept of dApp Rewards

dApp Rewards Work Flow:

1. Select a smart contract to stake \(nominate\)   
2. The nominator and operator will receive a reward proportional to the amount that has been staked.

![](../.gitbook/assets/sukurnshotto-2020-05-30-160230png%20%281%29.png)

Try it out:

### ① Nominate a Smart Contract:


Click **Staking -&gt; Account** **actions**. If you have not previously staked anything, your screen should look something like the following. From here press + New stake button in the top right corner.


![](../.gitbook/assets/screen-shot-2020-06-11-at-16.29.20.png)

The following screen should appear that contains four input parameters as follows:

* **Stash account**: Specifies which account tokens to use
* **Controller account**: Specifies the account that will be controlling the nomination status. For security reasons, it is recommended to have different accounts for the Stash account and Controller account, but for this demo, Bob’s account is used for both.
* **Value bonded**: Specifies the amount of token used for staking
* **Payment destination**: Specifies the recipient of the Rewards

![Bonding](../.gitbook/assets/screen-shot-2020-06-11-at-16.31.22.png)

Enter the inputs and press Bonding -&gt; sign and Submit to issue a transaction. The following screen should appear, with a new card and the same value that was given in the Bonding Preferences menu.

![](../.gitbook/assets/screen-shot-2020-06-11-at-16.33.28.png)

Tokens have been successfully locked, but this is not enough to nominated someone. Press the Nominate button in the right side of the card to officially nominate.

![](../.gitbook/assets/screen-shot-2020-06-11-at-16.35.14.png)

Choose the Smart Contract that will be nominated. Select the demo contract named “SAMPLE.WASM” uploaded from the last article! You can only choose a Smart Contract that has the canBeNominate parameter as Yes.

![](../.gitbook/assets/screen-shot-2020-06-11-at-22.54.43.png)

Press Nominate -&gt; Sign and Submit to issue a transaction. After a few moments, as we can see in the following image:

![](../.gitbook/assets/screen-shot-2020-06-11-at-16.38.25.png)

Now we have finished nominating a Smart Contract!


### ② Let’s receive some dApp Rewards!

Receiving a dApp Reward is very simple! Just wait! dApp Rewards are issued for each Era, which is a specific time cycle of the blockchain defined by the GRANDPA finality gadget. At the end of each Era, the Plasm chain will process the following:

1. Pay the incentives for every staking enabled nominator and the Contract operator.   
2. Enable staking for newly added nominations in this Era.  Nominations in Era1 will be enabled at the end of Era1 and receive incentives at the end of Era2. 

The timing between each Era is by default set to an hour. So, at the very most, just wait around 2 hours to receive incentives. 

Well, “Why in the name of bologna would I wait for that much for a demo,” you ask? If you’re using a local node, you can fast-forward the Era. 

First, go to the sidebar and choose Extrinsics. Then with your root user \(Alice in this case\) issue the following transaction. **Sudo\(forceNewEra\(\)\)**.


![](../.gitbook/assets/screen-shot-2020-06-11-at-23.07.30.png)


Issuing this transaction allows us to skip once to the next Era. To check if you moved on to the next Era, refer to the chain state. Check the value of forceEra\(\) in the plasmStaking, if it says ForceNew that means the Era has not been changed if it’s NotForcing that means the Era has changed.

![we can see that the Era has changed](https://user-images.githubusercontent.com/6259384/77172529-72992580-6b01-11ea-88ef-cb9588cdf829.png)

After a few minutes the Era will change.  Go to dAppStaking -&gt; Staking overview to check if the staking status has been enabled for SAMPLE.WASM. The following image shows that it is enabled.

![Staking overview](https://user-images.githubusercontent.com/6259384/77172527-72008f00-6b01-11ea-9898-a07f8b1f2929.png)

You can check the amount of token Bob and Alice have from the Accounts side menu.

![Accounts side menu 1](https://user-images.githubusercontent.com/6259384/77172525-7167f880-6b01-11ea-8198-6b13863c0f3c.png)

Again, if you use the same method mentioned above to fast-forward the Era and check Alice and Bob’s token…

![Accounts side menu 2](https://user-images.githubusercontent.com/6259384/77172516-6f059e80-6b01-11ea-8c73-0a0dd424a432.png)

Looking closely, you can see that Alice and Bob’s token have increased! If you are interested in understanding the algorithm for how the blockchain determines the amount of token to reward, please consider reading this article. The TL;DR version of it is that the rewards are proportional to the number of staked tokens. Additionally, the operator gains more rewards than the nominator. This concludes the demo.

### Summary <a id="summary"></a>

* This tutorial allowed you to play with dApp Reward!


* In Plasm, there is a system for incentivizing \(rewarding\) the Smart Contract owner!
* The amount being incentivized will be different from the users’ nomination!

New functionality of Plasm has been introduced through this and the previous article. As the Plasm Network is improved upon you will find updates to the documentation as well.

Any questions? Feel free  to ask us on [Discord Tech Channel](https://discord.gg/Z3nC9U4).
