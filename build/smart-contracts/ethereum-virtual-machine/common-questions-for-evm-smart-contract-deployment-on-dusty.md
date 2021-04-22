---
description: 'Updated: 04/22 by Mario'
---

# Common questions for EVM smart contract deployment on Dusty

* **Is there a step by step guide on how to deploy smart contract on Dusty?**
  * yes, please follow [this tutorial](https://docs.plasmnet.io/build/smart-contracts/ethereum-virtual-machine/ethereum-contract-on-dusty-network) in our documentation
* **Can I use** [**Remix**](http://remix.ethereum.org/#optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.1+commit.df193b15.js) **for smart contract deployment on Dusty?**
  * yes of course.
* **Can I use Truffle for smart contract deployment on Dusty?**
  * unfortunately at the moment you can’t use Truffle
  * when Shiden network is launched as Kusama parachain, you will be able to use Truffle
  * please use [Remix](http://remix.ethereum.org/#optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.1+commit.df193b15.js) until then
* **What is the name of the native token on Dusty**
  * PLD
* **How do I connect to Dusty testnet**
  * The best is to use Metamask and set Custom RPC
  * Network Name: Dusty
  * New RPC URL: [https://rpc.dusty.plasmnet.io:8545](https://rpc.dusty.plasmnet.io:8545/)
  * Chain ID: 80
  * Currency Symbol: PLD
* **How can I get test tokens \(PLD\)?**
  1. copy your metamask address \(a1\)
  2. swap to polkadot address [here](http://polkatools.hoonkim.me/index.html) \(a1 -&gt; a2\)
  3. use [faucet](https://plasm-faucet-frontend.vercel.app/) to send PLD to a2
* **I was given 1000 PLD by the faucet but my Metamask wallet shows 1**
  * Metamask uses 18 decimal places to represent PLD \(1 PLD is 1018 Units\), Polkadot uses 15 decimal places
  * this will be fixed on the mainnet
* **Is there a block explorer for Dusty**
  * At the moment there is no block explorer for Dusty
* **Is it possible to import Substrate \(Polkadot\) address to Metamask?**
  * No. Polkadot \(Substrate framework\) uses 256 bit address while Metamask uses 160 bit address
* **Can I interact with EVM contracts by using existing Dusty/Substrate account \(non-ecdsa\)?**
  * Any Substrate account could call EVM in Substrate, address will be mapped into EVM compatible representation

