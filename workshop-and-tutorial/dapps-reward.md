# DApps Reward 🍦

## Preparation

Just like what we did in our previous tutorial, we need to deploy a Contract. After that, when you go to your sidebar and press Staking, it should show like the following. Once you’re here, our preparation is over!

{% page-ref page="operator-trading.md" %}

![Dapps Staking Board](../.gitbook/assets/screen-shot-2020-06-11-at-16.26.00.png)

## The concept of Dapps Rewards

The overall logistics of how the Dapps Rewards works is like the following.

1. Select a Smart Contract to stake. \(this is also referred as nominate\)   
2. The nominator and the Smart Contract operator who’s nominated will gain economic incentives from Plasm chain that is proportional to the amount that has been staked.

![](../.gitbook/assets/sukurnshotto-2020-05-30-160230png%20%281%29.png)

Let’s try this ourselves!

### ① Let’s Nominate a Smart Contract!

Click **Staking -&gt; Account** **actions**. If you have not previously staked anything, your screen should look something like the following. From here press + New stake button in the top right corner.

![](../.gitbook/assets/screen-shot-2020-06-11-at-16.29.20.png)

After that, you should be able to see a screen appear that looks like the following image. There are four input parameters in here and we’ll go through all of them.

* **Stash account**: Specifies which account’s tokens to use. Think of this as a “bank account”.
* **Controller account**: Specifies the account that will be controlling the nomination status. For security reasons, it is recommended to have different accounts for the Stash account and Controller account, but for this demo, I’ll be using Bob’s account for both.
* **Value bonded**: Specifies the amount of token used for staking.
* **Payment destination**: Specifies the recipient of the Rewards.

![Bonding](../.gitbook/assets/screen-shot-2020-06-11-at-16.31.22.png)

After you’ve finished the inputs, press Bonding -&gt; sign and Submit to issue a transaction. Now you should be able to see something like the following image, a new card should appear with the same value that was given in the Bonding Preferences menu.

![](../.gitbook/assets/screen-shot-2020-06-11-at-16.33.28.png)

With this, we have successfully locked our token. But this is not enough to say that we’ve Nominated someone. For that, we must press the Nominate button in the right side of the card.

![](../.gitbook/assets/screen-shot-2020-06-11-at-16.35.14.png)

Pressing that will show the following form. Here, we get to choose the Smart Contract that will be nominated. Let’s select the demo Contract named “SAMPLE.WASM” that we uploaded from the last article! Please note that we can only choose a Smart Contract that has the canBeNominate parameter as Yes.

![](../.gitbook/assets/screen-shot-2020-06-11-at-22.54.43.png)

Press Nominate -&gt; Sign and Submit to issue a transaction. After a few moments, as we can see in the following image, we see a new section named Nominating with the Smart Contract that we chose in the previous step.

![](../.gitbook/assets/screen-shot-2020-06-11-at-16.38.25.png)

Now we have finished nominating a Smart Contract!

### ② Let’s **receive some Dapps Rewards**!

If you nominate a smart contract on the era \(E\), you can receive rewards after the next era \(E + 1\) is finished \(The term of an era is one day and the term of a session is ten minutes at Dusty\). Actually, we need to wait until the era \(E + 2\), but we can fast-forward the era by using ForceNewEra on your local node. First, go to the sidebar and choose Extrinsics. Then with your root user \(Alice in this case\) to issue the following transaction two times. Sudo\(forceNewEra\(\)\).

![](../.gitbook/assets/screen-shot-2020-06-11-at-21.23.53.png)

Now, you can claim rewards with "Claim for Nominator" tab and "Claim for Operator" tab. Click "Claim for Nominator" tab on Staking page and click "Claim" button. Then, you can see the following modal. 

![](../.gitbook/assets/screen-shot-2020-06-11-at-23.07.30.png)

To claim rewards for nominators, select nominator address and latest era, and push "Claim" button. You can use "Claim for Operator" tab for the same way.

![](../.gitbook/assets/screen-shot-2020-06-11-at-22.58.13.png)

### Summary <a id="summary"></a>

* We have played to nominate a smart contract!
* In Plasm, there is a system for incentivizing \(rewarding\) the Smart Contract owner!
* The amount being incentivized will be different from the users’ nomination!

We have introduced some new functionality of Plasm through this and the previous article. But there is room for improvements and changes we can make to these features. In which case we’ll update everyone so please stay tuned!

Any questions? Feel free  to ask us on [Discord Tech Channel](https://discord.gg/Z3nC9U4).

