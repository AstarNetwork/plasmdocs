# Calling Your Contract

## Smart contract messages

To communicate with Smart contracts. We use "messages".

![](../../../../.gitbook/assets/messages.png)

It's possible to pass two kinds of messages:

* messages that change a smart contract's state should be sent as transactions;
* messages that don't change a state could be called by using RPC calls.

Let's try to read our smart contract value by `get()` message call.

![This smart contract was deployed with enabled state flag.](../../../../.gitbook/assets/get_interaction.png)

Second, let's change a smart contract state by sending a "message", send `flip()` message that flips smart contract boolean flag.

![Flip call is a transaction.](../../../../.gitbook/assets/flip.png)

![New contract flag value reached.](../../../../.gitbook/assets/get_new.png)

Using these two kinds of messages, your DApp can easily write and read the smart contract data. Have fun!

Any questions? Feel free to ask [us](https://discord.gg/kH3Njpr).

