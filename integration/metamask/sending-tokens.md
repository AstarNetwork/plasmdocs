---
description: from/to MetaMask <> Polkadot.js.org
---

# Sending tokens

## Overview

Now that EVM is enabled, more and more developers are deploying their dApps in our ecosystem. One frequently asked question is: "How can I transfer my tokens from MetaMask to[ polkadot.js.org](https://polkadot.js.org/apps/)". In this tutorial, we will explain how to do this.

**Q:** Why would you need to do this?  
**A:** It's not possible to transfer SDN tokens from MetaMask to an exchange. This is because MetaMask is using an address format of H160 and SDN uses SS58 format. Meaning, you have to transfer your tokens first to an SS58 address before sending them to an exchange.

**Q:** Can I import my wallet with SDN in MetaMask?  
**A:** No, you first need to create or import an H160 wallet on MetaMask before sending SDN to that address.

**Q:** Why can't you just make it compatible?  
**A:** Astar ecosystem does not only support EVM but also will support WASM and other L1 ecosystems on Astar. Converting everything into H160 will make it a lot more difficult in the future. In the end, we are not just making a copy of Ethereum.

## The difference

![SS58 address](../../.gitbook/assets/image%20%2891%29.png)

![H160 address](../../.gitbook/assets/image%20%2892%29.png)

In this example, you can see that I'm using our testnet Shibuya. Shibuya is the Shiden’s parachain testnet with EVM functionalities which is the closest to the Shiden mainnet. Shibuya has the same chain specifications as Shiden and creates the best test environment for developers who want to launch their dApp on Shiden mainnet. This tutorial will work the same with Shiden. 

**SS58 address**: YvWEPYi6BRqpLeKQRQP1XZoWc6JM3LoZDCXgMNgtswXULvb  
**H160 address**: 0x0Ba1Aa8e98257EFb07cCa9bDCC410a38056897d1

What's the difference, think it obvious when you look at the example above.   
How to connect to Shiden or Shibuya, please have a look at the page below:

{% page-ref page="../network-details.md" %}

## Send tokens to MetaMask

The first step you need to take is converting your H160 address into SS58. You can do this on the page our lead dev created, Hoon Kim: [https://polkatools.hoonkim.me/index.html](https://polkatools.hoonkim.me/index.html)

![Convert H160 into SS58](../../.gitbook/assets/image%20%2890%29.png)

Just enter your address in the 'Input address' field, switch on EVM and you will get your SS58 address. Now I can send my SDN tokens to MetaMask. Just send it to the converted address.

![Sending tokens to MetaMask](../../.gitbook/assets/image%20%2894%29.png)

In the example, you can see that I'm sending 50 SBY tokens \(testnet tokens\) to `XAUAyrNUwhLskmt71mnuuQgo4Wji6jZQ1bRhf4Jt48vsnYR` this is the H160 address I just converted into SS58 through the website mentioned above. Click 'Make Transfer' and sign the message and wait until the transaction is confirmed. 

![MetaMask](../../.gitbook/assets/image%20%2893%29.png)

As you can see, the tokens are now visible on MetaMask. You can now use it to pay the gas fee for deploying smart contracts or use it on MetaMask. 

{% hint style="info" %}
**DO NOT SEND FROM METAMASK TO AN EXCHANGE! THIS IS NOT AN ERC20 TOKEN!**
{% endhint %}

## Send tokens to Polkadot JS

Let's send our tokens now to a wallet on [https://polkadot.js.org/apps/](https://polkadot.js.org/apps/).  
**NOTE**: make sure you are connected to Shibuya if you use SBY tokens or Shiden if you use SDN tokens.

![Wallet on Polkadot.JS](../../.gitbook/assets/image%20%2889%29.png)

For this tutorial, I just made a new wallet. What I need to do now to transfer tokens from MetaMask to this address, is to convert the SS58 address to H160 using this website: [https://polkatools.hoonkim.me/index.html](https://polkatools.hoonkim.me/index.html)

![](../../.gitbook/assets/image%20%2887%29.png)

You can see that I now converted my SS58 address into a H160 address. With this address, it's now possible to send tokens from MetaMask to an SS58 wallet.

![MetaMask](../../.gitbook/assets/image%20%2884%29.png)

In this example, I'm sending 10 SBY \(testnet tokens\) to my converted SS58 address. Click on 'Next' and confirm your transaction. 

![Transaction completed](../../.gitbook/assets/image%20%2883%29.png)

EVM to Substrate or H160 to SS58 is a two-phase process. Meaning, you need to call for your EVM balance and you should send `evm:withdraw()` transaction.

![Call your EVM asset](../../.gitbook/assets/image%20%2886%29.png)

In the screenshot above, my SS58 address calls for the funds sent to my account from H160. After signing the transaction, your funds will be transferred to your account. You can verify on Subscan.

Shibuya: [https://shibuya.subscan.io](https://shibuya.subscan.io)  
Shiden: [https://shiden.subscan.io](https://shibuya.subscan.io)

![](../../.gitbook/assets/image%20%2885%29.png)

