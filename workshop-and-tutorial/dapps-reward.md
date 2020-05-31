# DApps Reward 🍦

## Preparation

Just like what we did in our previous tutorial, we need to deploy a Contract. After that, when you go to your sidebar and press DappsStaking, it should show like the following. Once you’re here, our preparation is over!

{% page-ref page="operator-trading.md" %}

![DppsStaking board](https://user-images.githubusercontent.com/6259384/77172548-775dd980-6b01-11ea-9c32-c360a6f09759.png)

## The concept of Dapps Rewards

The overall logistics of how the Dapps Rewards works is like the following.

1. Select a Smart Contract to stake. \(this is also referred as nominate\)   
2. The nominator and the Smart Contract operator who’s nominated will gain economic incentives from Plasm chain that is proportional to the amount that has been staked.

![](../.gitbook/assets/sukurnshotto-2020-05-30-160230png%20%281%29.png)

Let’s try this ourselves!

### ① Let’s Nominate a Smart Contract!

Click **DappsStaking -&gt; Account** **actions**. If you have not previously staked anything, your screen should look something like the following. From here press + New stake button in the top right corner.

![rightcorner](https://user-images.githubusercontent.com/6259384/77172540-762cac80-6b01-11ea-9215-053c0584f327.png)

After that, you should be able to see a screen appear that looks like the following image. There are four input parameters in here and we’ll go through all of them.

* **Stash account**: Specifies which account’s tokens to use. Think of this as a “bank account”.
* **Controller account**: Specifies the account that will be controlling the nomination status. For security reasons, it is recommended to have different accounts for the Stash account and Controller account, but for this demo, I’ll be using Bob’s account for both.
* **Value bonded**: Specifies the amount of token used for staking.
* **Payment destination**: Specifies the recipient of the Rewards.

![Bonding](https://user-images.githubusercontent.com/6259384/77172537-75941600-6b01-11ea-8a13-907d18ae8cf1.png)

After you’ve finished the inputs, press Bonding -&gt; sign and Submit to issue a transaction. Now you should be able to see something like the following image, a new card should appear with the same value that was given in the Bonding Preferences menu.

![The specified amount bonded and the receiving account is the same as the value we provided](https://user-images.githubusercontent.com/6259384/77172536-74fb7f80-6b01-11ea-970d-6f649ad28af8.png)

With this, we have successfully locked our token. But this is not enough to say that we’ve Nominated someone. For that, we must press the Nominate button in the right side of the card.

![pressent](https://user-images.githubusercontent.com/6259384/77172535-7462e900-6b01-11ea-8d94-06f8ffba6cb5.png)

Pressing that will show the following form. Here, we get to choose the Smart Contract that will be nominated. Let’s select the demo Contract named “SAMPLE.WASM” that we uploaded from the last article! Please note that we can only choose a Smart Contract that has the canBeNominate parameter as Yes.

![Press Nominate](https://user-images.githubusercontent.com/6259384/77172533-73ca5280-6b01-11ea-9a67-01357aa6f9eb.png)

Press Nominate -&gt; Sign and Submit to issue a transaction. After a few moments, as we can see in the following image, we see a new section named Nominating with the Smart Contract that we chose in the previous step.

![Smart Contract](https://user-images.githubusercontent.com/6259384/77172532-7331bc00-6b01-11ea-93df-6b7dd61fec66.png)

Now we have finished nominating a Smart Contract!

### ② Let’s receive some Dapps Rewards!

Receiving a Dapps Reward is very simple! We wait! You see, Dapps Rewards is issued for each Era, which is a specific time cycle of the blockchain defined by the GRANDPA finality gadget. At the end of each Era, the Plasm chain will process the following. 

1. pay the incentives for every staking enabled nominator and the Contract operator.   
2. enable staking for newly added nominations in this Era. In other words, nominations in Era1 will be enabled at the end of Era1 and receive incentives at the end of Era2. 

The timing between each Era is by default set to around an hour. So, at the very most, we just need to wait for around 2 hours to receive our incentives!! Well, “why in the name of bologna would I wait for that much for a demo,” you say? Fortunately, if you’re using a local node, you can fast-forward the Era as you want, meaning you can just skip to the Era where you get paid without having to wait! Let’s see how we can do this. First, go to the sidebar and choose Extrinsics. Then with your root user \(Alice in this case\) to issue the following transaction. **Sudo\(forceNewEra\(\)\)**.

![sudo](https://user-images.githubusercontent.com/6259384/77172531-7331bc00-6b01-11ea-98d4-8d132a91ee58.png)

Issuing this transaction allows us to only once skip to the next Era. To check if we did move on to the next Era, we can see that from the Chain state. Check the value of forceEra\(\) in the plasmStaking, if it says ForceNew that means the Era has not been changed if it’s NotForcing that means the Era has changed.

![we can see that the Era has changed](https://user-images.githubusercontent.com/6259384/77172529-72992580-6b01-11ea-88ef-cb9588cdf829.png)

After a few minutes the Era will change, so let’s go to DappsStaking -&gt; Staking overview to check if our staking status has been enabled for SAMPLE.WASM. As we can see from the following image, it is indeed enabled.

![Staking overview](https://user-images.githubusercontent.com/6259384/77172527-72008f00-6b01-11ea-9898-a07f8b1f2929.png)

Additionally, we can check the amount of token Bob and Alice has from the Accounts side menu.

![Accounts side menu 1](https://user-images.githubusercontent.com/6259384/77172525-7167f880-6b01-11ea-8198-6b13863c0f3c.png)

Again, if you use the same method mentioned above to fast-forward the Era and check Alice and Bob’s token…

![Accounts side menu 2](https://user-images.githubusercontent.com/6259384/77172516-6f059e80-6b01-11ea-8c73-0a0dd424a432.png)

A little hard to notice but if we look closely, we can see that Alice and Bob’s token has increased! If you are interested in understanding the algorithm for how the blockchain determines the amount of token to increase, please consider reading this article. The TL;DR version of it is that the rewards are proportional to the number of staked tokens. Additionally, the operator gains more rewards than the nominator. With this, we have finished the demo! Thank you for following me this far!

### Summary <a id="summary"></a>

* We have played with Dapps Staking!
* In Plasm, there is a system for incentivizing \(rewarding\) the Smart Contract owner!
* The amount being incentivized will be different from the users’ nomination!

We have introduced some new functionality of Plasm through this and the previous article. But there is room for improvements and changes we can make to these features. In which case we’ll update everyone so please stay tuned!

Any questions? Feel free  to ask us on [Discord Tech Channel](https://discord.gg/Z3nC9U4).

