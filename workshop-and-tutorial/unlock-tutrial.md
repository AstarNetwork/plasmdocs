# Unlock Tutorial 🔓

Lockdrop's Lock Contract contains the following anonymous function.

```text
/**
* @dev Withdraw function once timestamp has passed unlock time
*/

function () external payable {
 assembly {
  switch gt(timestamp, sload(0x01))
  case 0 { revert(0, 0) }
  case 1 {
   switch call(gas, sload(0x00), balance(address), 0, 0, 0, 0)
  case 0 { revert(0, 0) }
  }
 }
}
```

This enables the contract to return the locked balance \(the entire contract balance\) to the original token locker's address by sending an empty transaction to this contract address. However, the timestamp of the transaction must be greater than the timestamp of the lock including the lock duration. When someone sends a transaction before the duration of the locks is passed, the transaction will return a error. Sending a transaction to the lock \(i.e. unlocking the tokens\) can be done by anyone given that they have enough funds to pay for the transaction fee. But the the locked tokens will only return to the original locker rather than the address that sent the transaction. So it is possible to allow another address to unlock the locked token on behalf of the original locker, but they cannot claim the tokens for themselves. One point to note is that once the lock duration is over, the contract will not have any transaction rejections, meaning even if the token was returned to the original locker, anyone can still send a transaction to the contract without any errors. Once the token is claimed it will not be able to return any more tokens,as the contract balance will be 0, but it makes it hard for the original locker to check if the tokens were unlocked or not without having to check the contract balance or track their balance, effectively giving a potential issue of wasting transaction fee for attempting to claim the locked tokens that was already unlocked.

![](../.gitbook/assets/sukurnshotto-2020-05-31-191620png.png)

The Lockdrop Web Application comes with an intuitive form that displays any lock information. Under the `Unlock Tokens` tab, it will display a list of locks that was locked by the current address in a Web3 enabled browser wallet extension. Once the lock duration is over, the lock icon on the right will change to a lighter color. Clicking this icon will allow you to send to transaction of 0 ETH to the lock address, unlocking the tokens. This form allows you to easily check the lock information, time until the lock is over and unlock once it is over. However, as mentioned above, it is hard to check if the lock has been already claimed or not, so even if the locks were successfully claimed, the UI elements will still look the same.

Any questions? Feel free  to ask us on [Discord Tech Channel](https://discord.gg/Z3nC9U4).

