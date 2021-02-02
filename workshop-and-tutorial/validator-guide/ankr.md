---
description: Run your Dusty node with Ankr
---

# Ankr

 _Ankr enables easy node hosting and validating services for Plasm Network on desktop and mobile._

Plasm Network is rolling out an integration with [Ankr](https://www.ankr.com/), your gateway to Web3, connecting consumers, developers, and enterprises to the new internet, in a few easy clicks. [Read the full announcement](https://medium.com/plasm-network/one-click-plasm-testnet-node-on-ankr-1a177f988bcc).

## Create account

Go to the Ankr website and create an account. Once your account is created, you can visit their market. Search for 'Plasm Testnet - Dusty' and click on 'Deploy'.

![](../../.gitbook/assets/image%20%287%29.png)

## Setup your node

When your node is fully deployed and synced to the network, you can proceed with the following steps.

![](../../.gitbook/assets/image%20%288%29.png)

To get real-time stats of the node, please head to the [Polkadot Telemetry Web App](https://telemetry.polkadot.io/#/Dusty). On the Dusty tab, you then search your node name for further information. After the node has finished syncing, you can follow the following steps:

**\#1 -** Go to [Plasm Network UI](https://apps.plasmnet.io/#/accounts) and create an account. Make sure you are connected to 'Dusty' testnet. You can change from network in the top left menu:

![](../../.gitbook/assets/image%20%286%29.png)

**\#2 -** When you don't have an account, you can create one by clicking 'Add Account'. A form pops-up. Choose a name and password. The most important part of this form is your mnemonic seed! Write this down, take a screenshot, … don’t lose it.

Click on ‘**Next**’ and ‘**Save**’. Store your \*.json file somewhere on your computer, cloud, … In case you lose your mnemonic seed, you can always restore your account with this file.

**\#3 -** Copy your 'Session Key' in Ankr dashboard. Go back to Plasm UI and click on ‘**Developer**’ — ‘**Extrinsics**’ — ‘**Session**’ — ‘**setKeys**\(keys, proof\)’ and paste the result in the keys field and in the proof field, enter 0x00.

![Image for post](https://miro.medium.com/max/1869/1*o9mHfP4suI_1i7kzymaxAg.png)

Don’t forget to ‘**Submit Transaction**’ after you paste the key.

**\#4 -** Share your validator account address with **Stake Technologies** team via [Google Form](https://docs.google.com/forms/d/e/1FAIpQLSday0ckkK43TzJgKtQmJdzkudQNFDXspZAuUGi5Y5vfjkis3Q/viewform).

**\#5 -** Follow your submission in the [Dusty validator sheet](https://docs.google.com/spreadsheets/d/1AYsS6V_Ypwde5lYulhZBMAx1X2vZ1u1zDXni_ddz-6c/edit#gid=2013382367).

That's it!

