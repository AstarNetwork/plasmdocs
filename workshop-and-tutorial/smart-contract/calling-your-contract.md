# Calling Your Contract

## Smart contract messages

To communicate with Smart contracts in Substrate used conception of messages.

![](../../.gitbook/assets/messages.png)

It's possible to pass two kind of messages:

* messages that change smart contract state should be send as transactions;
* messages that don't change state could be called using RPC calls.

The first, let's try to read our smart contract value by `get()` message call.

![This smart contract was deployed with enabled state flag.](../../.gitbook/assets/get_interaction.png)

The second kind of messages changes smart contract state, let's send `flip()` message that flips smart contract boolean flag.

![Flip call is a transaction.](../../.gitbook/assets/flip.png)

![New contract flag value reached.](../../.gitbook/assets/get_new.png)

Using this two kind of messages your DApp can easy write and read smart contract data. Have fun!



