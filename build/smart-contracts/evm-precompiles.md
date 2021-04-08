---
description: >-
  This article explains useful precompiled smart contracts available in Plasm
  Network runtime.
---

# EVM Precompiled Contracts

Precompiles in Solidity is a native way to speed up general but expensive functions and interacts with something outside the VM. For example, ECRecover precompiled smart contracts definitely boost public key recovery functions because of execution almost on the hardware level. From another side, the Plasm Network includes dispatch precompiled smart contracts, that permit Solidity developers to interact with other Plasm runtime modules.

### The ECRecover precompile

The ECRecover is a standard Solidity precompiled smart contract available at the address `0x01`. It is used in most contracts to improve ECDSA performance during recovering signature signer account.

### The Dispatch precompile

On standard Plasm Parachain runtime `Dispatch` smart-contract available at the address:

* `0x0000000000000000000000000000000000000006`

Internally, this contract just decodes input data as `Call` structure

```text
let call = T::Call::decode(&mut &input[..]).map_err(|_| ExitError::Other("decode failed".into()))?;
```

and then executes it as a transaction from smart contract origin.

```text
let origin = T::AddressMapping::into_account_id(context.caller);
match call.dispatch(Some(origin).into()) {
...
```

That  means each EVM smart contract could call any available method of runtime using Solidity standard `call()` function to the precompiled contract address.

### Solidity SCALE codec

The difficulty for Solidity developers is that the [SCALE](https://substrate.dev/docs/en/knowledgebase/advanced/codec) codec isn't available for Solidity. As a  result, they should encode call parameters manually that could be complex and expensive.

But for calling standard or trivial methods it's not a big problem. For example, call `Balances::transfer()` for `5FHneW46xGXgs5mUiveU4sbTyGBzmstUspZC92UhjJM694ty` and `42` looks like:

```text
0x0400008eaf04151687736326c9fea17e25fc5287613693c912909cb226aa4794f26a48a8
```

Where `0x04` is a module index, following `0x00` is a method index in the module and next is address and balance parameters. If your contract should constantly transfer the same amount to the same destination, then a constant call string could be used.

