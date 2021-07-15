# Calling Your Contract

## Smart contract messages

We use "messages" to communicate with smart contracts. There are 2 types of messages:

* messages that change a smart contract's state should be sent as transactions
* messages that don't change a state can be made by using RPC calls

![](../../../../.gitbook/assets/image%20%2868%29.png)

The Plasm Network Portal UI helps us to make RPC message calls automatically so you don't have to manually call them. You can see what is stored in the `value`variable in the smart contract is `false`. This is the intended behaviour as defined by our smart contract logic. 

![](../../../../.gitbook/assets/image%20%2867%29.png)

Next, let's change the smart contract state by sending a transaction that calls the `flip()` function. 

![](../../../../.gitbook/assets/0%20%281%29.gif)

As expected, the value that was stored in the smart contract changed from `false`to `true` after the `flip()` transaction is successfully mined.

Using these two kinds of messages, your DApp can easily write and read the smart contract data. Have fun!

Any questions? Feel free to ask [us](https://discord.gg/kH3Njpr).

