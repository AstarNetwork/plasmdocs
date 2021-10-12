# Ethereum Contract on Dusty Network

In this section, I am going to walk through how to deploy Ethereum smart contracts on Dusty Network. 

{% hint style="info" %}
Check out our demo below
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=5C8l9XWCWoI&t=67s" %}

First of all, let's open [Remix](https://remix.ethereum.org) and create a new file. 

![](../../../.gitbook/assets/screen-shot-2021-03-14-at-15.23.26.png)

As a next step, write your Solidity or Vyper contract and compile it. To deploy your contract on Dusty Network, you need to set up your Metamask.  

{% tabs %}
{% tab title="Select Network" %}
![Click the tab and select Custom RPC](../../../.gitbook/assets/screen-shot-2021-03-14-at-15.31.14.png)

Click the tab  and select "Custom RPC"

then enter the following values:

**RPC server Dusty:**\
****Network Name: Dusty\
New RPC URL: https://rpc.dusty.plasmnet.io:8545\
Chain ID: 80\
Currency Symbol: PLD
{% endtab %}

{% tab title="Configure Dusty Settings" %}
![](../../../.gitbook/assets/screen-shot-2021-03-14-at-15.29.59.png)

Fill out the blanks as follows

* Network Name: Dusty
* New RPC URL: [https://rpc.dusty.plasmnet.io:8545](https://rpc.dusty.plasmnet.io:8545)
* Chain ID: 80
* Current Symbol: PLD
{% endtab %}
{% endtabs %}

Then your Metamask is connected to Dusty Network. 

![](../../../.gitbook/assets/screen-shot-2021-03-14-at-15.05.05.png)

Currently, you don't have any PLDs and all you can see on Metamask is your Ethereum address. 

But no worries. Hoon Kim, our core developer made a [converter from Ethereum address to Plasm address](https://hoonsubin.github.io/evm-substrate-address-converter/index.html).

Once you put your Ethereum address, you can see your Dusty Network address. (In my case, it is `"5GE3BSRDERKkdGEnbkbBjH8iV3WroPgWM15AKQzuTAWprnSK"`)

![](../../../.gitbook/assets/screen-shot-2021-03-14-at-17.38.50.png)

Lastly, please let us know your Dusty Network address on [Discord](https://discord.gg/PTtZZFxneP) so that we can send PLDs to your wallet. 

The last thing is to deploy your contract on the network. Select "Injected Web3" and click "deploy" 

![](../../../.gitbook/assets/screen-shot-2021-03-14-at-17.46.04.png)

Once Metamask is launched and you press "Confirm", you can deploy the contract to the network. 
