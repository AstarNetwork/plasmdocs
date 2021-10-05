# Configure Metamask

## Add Network to your Metamask

It's easy to configure your Metamask to interact with Aster/Shiden network family. Open Metamask, click network tab, and click the Custom RPC. In the screen shown, please enter the necessary information as follows:

{% tabs %}
{% tab title="Local" %}
* Network Name:  Shiden Local
* New RPC URL: [http://localhost:9933](http://localhost:9933)
* Chain ID: 4369
* Currency Symbol: ASTL
{% endtab %}

{% tab title="Shibuya" %}
* Network Name:  Shibuya
* New RPC URL: [https://rpc.shibuya.astar.network:8545](https://rpc.shibuya.astar.network:8545)
* Chain ID: 81
* Currency Symbol: SBY
{% endtab %}

{% tab title="Shiden" %}
* Network Name:  Shiden
* New RPC URL: [https://rpc.shiden.astar.network:8545](https://rpc.shiden.astar.network:8545)
* Chain ID: 336
* Currency Symbol: SDN
{% endtab %}
{% endtabs %}

If you want to know more about Metamask Support, please take a look following page:

{% page-ref page="../../integration/metamask/" %}

## Get your local token on Metamask

Currently, you see that you have no tokens on Metamask. So let's transfer some local token to the account on Metamask.   
But before proceeding, you must study the address format of Substrate and EVM. Substrate uses SS58 format and Metamask\(EVM\) uses H160 format. This means you need to convert H160 address to SS58 address to receive local tokens. You can learn more details on the following page:

{% page-ref page="../../integration/metamask/sending-tokens.md" %}

You can convert your H160 address to SS58 address on the following page:  
[https://polkatools.hoonkim.me/index.html](https://polkatools.hoonkim.me/index.html)  
Just enter your address in the 'Input address' field, switch on EVM and you will get your SS58 address. In my case, SS58 and H160 address was as follows:

* SS58: W6FALw8rEThak16wwtPoRBYJMuA5hHmoM6mhKzfzTzfg3xR
* H160: 0x2C49dD5611A6427E9C621350218651F505D2F011

OK, now you are ready to receive some local tokens on your Metamask! Go to account page on the explorer and click the send button of Alice. In the screen shown, you can input your SS58 address in `send to address` field and designate the amount to send. Then click the `Make Transfer` button.

![](../../.gitbook/assets/image%20%28102%29.png)

Congratulations!  Now you see your local token on Metamask. And you are almost ready to deploy your first smart contract on Shiden local network now!

![](../../.gitbook/assets/image%20%28106%29.png)



