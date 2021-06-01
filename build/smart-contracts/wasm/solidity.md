---
description: Ethereum like smart contracts on Plasm Network.
---

# Solidity to WASM Compiler

Plasm Network also supports solidity. Solidity is a smart contract language mainly used on Ethereum. If you have already built applications by using Solidity, you can also deploy the contracts on Plasm Network.

## Install

In this tutorial, we will use the [Solang compiler](https://github.com/hyperledger-labs/solang), a compiler for solidity language developed by Hyperledger Labs. Let's install the compiler using the original instruction below.

{% embed url="https://solang.readthedocs.io/en/latest/installing.html" %}

Or using the following cargo command:

```text
sudo apt install llvm openssl libxml2-dev
cargo install --git https://github.com/hyperledger-labs/solang --tag m8
```

{% hint style="warning" %}
M1 chip macs may need to do build llvm from source:

read more on the issue [here](https://github.com/hyperledger-labs/solang/issues/421)

```
git clone git://github.com/solana-labs/llvm-project
cd llvm-project

// install cmake, ninja, and any other dependencies //

cmake -G Ninja -DLLVM_ENABLE_ASSERTIONS=On '-DLLVM_ENABLE_PROJECTS=clang;lld'  \
        -DLLVM_ENABLE_TERMINFO=Off -DCMAKE_BUILD_TYPE=Release \
        -DCMAKE_INSTALL_PREFIX=installdir -B build llvm
        
cmake --build build --target install

//mac users do:
export PATH=installdir/bin:$PATH
```
{% endhint %}

The `solang` binary should be available in your environment.

## Compile

You can write any solidity contracts just like the development on Ethereum. Since this is a tutorial, we will use a `flipper` contract which is available below.

{% embed url="https://github.com/hyperledger-labs/solang/blob/master/examples/flipper.sol" %}

Let's compile it using `substrate` target to make it compatible with Plasm Network.

```text
wget https://raw.githubusercontent.com/hyperledger-labs/solang/master/examples/flipper.sol
solang flipper.sol
```

As a result, two files should be available in your current directory : `flipper.wasm` \(optimized WASM binary\) and `flipper.json` \(smart contract metadata\).

## Deploy

Let's deploy the compiled `flipper.wasm` and `flipper.json` using our standard [Plasm Portal UI](https://apps.plasmnet.io).

![Deploy your smart contract WASM code on Dusty Network.](../../../.gitbook/assets/flipper.png)

The next step is to create an instance of the uploaded smart contract WASM code.

![Sent smart contract instance transaction.](../../../.gitbook/assets/instance_flipper.png)

After making the instance, we can interact with the smart contract using the UI portal just like an ink! smart contract described in the previous chapter.

![Read data from smart contract using RPC call.](../../../.gitbook/assets/call_flipper.png)

![Write data into smart contract via a transaction.](../../../.gitbook/assets/call_flipper2.png)

More examples are available in the Solang repository:

{% embed url="https://github.com/hyperledger-labs/solang/tree/master/examples" %}

Have fun and good luck!

## Windows setup

Here you will find a tutorial:

{% embed url="https://medium.com/plasm-network/compile-smart-contracts-written-in-solidity-for-plasm-network-on-windows-1ed18993f82e" %}



Any questions? Feel free to ask us on our [Discord tech channel](https://discord.com/invite/kH3Njpr).[  
](https://docs.plasmnet.io/workshop-and-tutorial/smart-contract/deploy-your-smart-contract-on-plasm)

