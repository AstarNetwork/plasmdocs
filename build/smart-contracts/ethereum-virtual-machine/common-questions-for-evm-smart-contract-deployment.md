---
description: 'Updated: 04/22 by Mario'
---

# FAQ for EVM smart contract deployment

*   **Is there a step by step guide on how to deploy smart contract in the Astar ecosystem?**

    * Yes, please follow [this tutorial ](../../../tutorial/develop-and-deploy-your-first-smart-contract-on-aster-shiden-evm/)in our documentation.


*   **Can I use** [**Remix**](http://remix.ethereum.org/#optimize=false\&runs=200\&evmVersion=null\&version=soljson-v0.8.1+commit.df193b15.js) **for smart contract deployment?**

    * Yes of course.


*   **Can I use** [**Hardhat**](https://hardhat.org) **for smart contract deployment?**

    * Yes, please follow [this tutorial](using-hardhat.md) in our documentation as example.


*   **What is the name of the native tokens in the Astar ecosystem?**

    * SBY (Shibuya - Testnet tokens)
    * SDN (Shiden Network)
    * ASTR (Astar Network)


*   **How do I connect to our networks, RPCs, Network name, Chain ID?**

    * Go to this [page](../../../integration/network-details.md).


*   **How can I get test tokens (SBY)?**

    * Use our faucet. Follow this [tutorial](../../testnet-faucet.md).

    ****
*   **Is there a block explorer?**

    * yes, Go to this [page](../../../integration/network-details.md).


*   **Is it possible to import Substrate (Polkadot) address to Metamask?**

    * No. Polkadot (Substrate framework) uses 256 bit address while Metamask uses 160 bit address


*   **Can I interact with EVM contracts by using existing Substrate account (non-ecdsa)?**

    * Any Substrate account could call EVM in Substrate, the address will be mapped into EVM compatible representation


* **I was able to deploy contracts in other networks, but contracts deployed in this network show "out of gas" error with the error code of 0. How do I fix it?**
  * Contract size limits may differ in the network, it is recommended to lower optimizer runs of the same smart contract for adjusting the compatible size for the network. Please try testnet to tune it.
