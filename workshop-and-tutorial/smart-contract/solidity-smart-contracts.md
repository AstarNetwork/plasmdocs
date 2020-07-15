---
description: Ethereum like smart contracts in Plasm Network.
---

# Solidity smart contracts

## Install

In this tutorial the [Solang compiler](https://github.com/hyperledger-labs/solang) will be used. Solang is Hyperledger Labs developed compiler for Solidity language. Install compiler using original instruction below.

{% embed url="https://solang.readthedocs.io/en/latest/installing.html" %}

Or using Cargo command:

```text
sudo apt install llvm openssl libxml2-dev
cargo install --git https://github.com/hyperledger-labs/solang --tag m8
```

The `solang` binary should be available in your environment.

## Compile

The Solidity written analog of `flipper` contract source code available below.

{% embed url="https://github.com/hyperledger-labs/solang/blob/master/examples/flipper.sol" %}

Let's compile it using `substrate` target that makes it compatible with Plasm Network smart contracts.

```text
wget https://raw.githubusercontent.com/hyperledger-labs/solang/master/examples/flipper.sol
solang flipper.sol
```

As result in your current directory should be available two files: `flipper.wasm` \(optimized WASM binary\) and `flipper.json` \(smart contract metadata\).

## Deploy

Let's deploy compiled `flipper.wasm` and `flipper.json` using standard [Plasm Portal UI](https://apps.plasmnet.io)Plasm Portal UI.

![Deploy smart contract WASM code on Dusty Network.](../../.gitbook/assets/flipper.png)

Next step is creating an instance of uploaded smart contract WASM code.

![Sent smart contract instance transaction.](../../.gitbook/assets/instance_flipper.png)

As result we can interact with smart contract using UI as same as in case with Ink! smart contract described some sections above.

![Read data from smart contract using RPC call.](../../.gitbook/assets/call_flipper.png)

![Write data into smart contract via transaction sent.](../../.gitbook/assets/call_flipper2.png)

More examples available in Solang repository:

{% embed url="https://github.com/hyperledger-labs/solang/tree/master/examples" %}

Have fun and good luck!





