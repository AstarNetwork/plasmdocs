# Secure Collator Setup

## Overview

{% hint style="info" %}
This tutorial requires a certain technical background if you don't have any background please follow this guide carefully and use Google to learn more about what you are doing.
{% endhint %}

The **Astar/Shiden ecosystem** has raised incredible attention in the past few months, and this is just the beginning. Many individuals joined the adventure and set up their own **collator node**, which is great for decentralization. Running a collator on a mainnet is a lot of **responsibility**!

We recommend monitoring your validator and setting up alerts in case something is going wrong with your server. As a future Astar/Shiden collator, this monitoring is mandatory.&#x20;

This guide is based on [the guide made by one of our ambassadors](https://bldstackingnode.medium.com/monitoring-substrate-node-polkadot-kusama-parachains-validator-guide-922734ea4cdb#efff), [Polkadot Wiki](https://wiki.polkadot.network/docs/en/maintain-guides-how-to-monitor-your-node), [W3F secure validator repo](https://github.com/w3f/polkadot-secure-validator). Creating the ultimate guide to secure your validator.

{% embed url="https://github.com/w3f/polkadot-secure-validator" %}

We are happy to offer any kind of support you need. Keep in mind that you have to follow this guide carefully, no need to ask questions beforehand. In case of any errors please provide us with screenshots and at what step this error occurs. Join our developers community on Discord for all your technical support:

{% embed url="https://discord.com/invite/wUcQt3R" %}



## Understanding

A validator or collator in the Polkadot/Kusama ecosystem plays an essential role in Aster/Shiden network and is responsible for crucial tasks, including block production and transaction confirmation. A collator needs to maintain a high communication response capability to ensure seamless operation of the network. It is also necessary for them to establish a good reputation in the community to attract more nominators who nominate their tokens to improve the network’s security. Based on network affordability and security considerations, validator seats will gradually open after the launch of Plasm/Shiden.

As a future validator, it's very important that you know what you are doing. I don't want to encourage you to move forward but it's important to understand that running a collator comes with responsibility. Also, who doesn't want to learn something new? Reading, learning, understanding, and setting things up would take between **2-4 hours**.&#x20;

## Walkthrough

These are the steps you should walk through when you want to become a validator on Shiden:

{% content-ref url="create-your-environnement.md" %}
[create-your-environnement.md](create-your-environnement.md)
{% endcontent-ref %}

{% content-ref url="secure-your-ssh-connection.md" %}
[secure-your-ssh-connection.md](secure-your-ssh-connection.md)
{% endcontent-ref %}

{% content-ref url="ssh-tunneling.md" %}
[ssh-tunneling.md](ssh-tunneling.md)
{% endcontent-ref %}

Now the fun starts! Let's install all software:

{% content-ref url="plasm-shiden-node.md" %}
[plasm-shiden-node.md](plasm-shiden-node.md)
{% endcontent-ref %}

{% content-ref url="installation-node-monitoring.md" %}
[installation-node-monitoring.md](installation-node-monitoring.md)
{% endcontent-ref %}

{% content-ref url="configuration.md" %}
[configuration.md](configuration.md)
{% endcontent-ref %}

{% content-ref url="services.md" %}
[services.md](services.md)
{% endcontent-ref %}

{% content-ref url="launch-and-active-services.md" %}
[launch-and-active-services.md](launch-and-active-services.md)
{% endcontent-ref %}
