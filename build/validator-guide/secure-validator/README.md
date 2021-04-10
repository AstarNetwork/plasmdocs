---
description: This guide is for running a secure validator on Plasm / Shiden.
---

# Secure Validator Setup

## Overview

{% hint style="info" %}
This tutorial requires a certain technical background if you don't have any background please follow this guide carefully and use Google to learn more about what you are doing.
{% endhint %}

{% hint style="info" %}
Before joining Plasm/Shiden mainnet, it's great to test everything out on our testnet 'Dusty', build up your skills.
{% endhint %}

The **Plasm/Shiden ecosystem** has raised incredible attention in the past few months, and this is just the beginning. Many individuals joined the adventure and set up their own **validator node**, which is great for decentralization. Running a validator on a mainnet is a lot of **responsibility**! You will be accountable for not only your own stake, but also the stake of your current nominators. If you make a mistake and get slashed, your money and your reputation will be at risk. **However**, running a validator can also be very rewarding, knowing that you contribute to the security of a decentralized network while growing your stash.

We recommend monitoring your validator and set up alerts in case something is going wrong with your server. As a future Plasm/Shiden validator and want to use our Azure services, this monitoring is mandatory. 

This guide is based on [the guide made by one of our ambassadors](https://bldstackingnode.medium.com/monitoring-substrate-node-polkadot-kusama-parachains-validator-guide-922734ea4cdb#efff), [Polkadot Wiki](https://wiki.polkadot.network/docs/en/maintain-guides-how-to-monitor-your-node), [W3F secure validator repo](https://github.com/w3f/polkadot-secure-validator). Creating the ultimate guide to secure your validator.

{% embed url="https://github.com/w3f/polkadot-secure-validator" %}

We are happy to offer any kind of support you need. Keep in mind that you have to follow this guide carefully, no need to ask questions beforehand. In case of any errors please provide us with screenshots and at what step this error occurs. Join our developers community on Discord for all your technical support:

{% embed url="https://discord.com/invite/wUcQt3R" %}



## Understanding

A validator or collator in the Polkadot/Kusama ecosystem plays an essential role in Plasm/Shiden network and is responsible for crucial tasks, including block production and transaction confirmation. A validator needs to maintain a high communication response capability to ensure seamless operation of the network. It is also necessary for them to establish a good reputation in the community to attract more nominators who nominate their tokens to improve the network’s security. Based on network affordability and security considerations, validator seats will gradually open after the launch of Plasm/Shiden. In the future, we aim to have 100 validator seats on Plasm and 100 seats on Shiden.

As a future validator, it's very important that you know what you are doing. I don't want to encourage you to move forward but it's important to understand that running a validator comes with responsibility. Also, who doesn't want to learn something new? Reading, learning, understanding, and setting things up would take between **2-4 hours**. 

**The final setup will look like this:**

![&#xA9; bLd Nodes](../../../.gitbook/assets/image%20%2816%29.png)

## Walkthrough

These are the steps you should walk through when you want to become a validator on Shiden:

{% page-ref page="create-your-environnement.md" %}

{% page-ref page="secure-your-ssh-connection.md" %}

{% page-ref page="ssh-tunneling.md" %}

Now the fun starts! Let's install all software:

{% page-ref page="plasm-shiden-node.md" %}

{% page-ref page="installation-node-monitoring.md" %}

{% page-ref page="configuration.md" %}

{% page-ref page="services.md" %}

{% page-ref page="launch-and-active-services.md" %}







1. Configuration 
2. Setting services 
3. Test Alert Manager 
4. Run Grafana dashboard 
5. Conclusion

Let's get to work! 



