---
description: >-
  Patract Labs is building a tool called Redspot, "Truffle" for Polkadot
  ecosystem. In this section, we will walk you through how to use Redspot on
  Plasm Network.
---

# Redspot by Patract Labs

## What is Redspot?

[Redspot ](https://docs.patract.io/en/redspot/introduction.html)is a contract integration builder that allows developers to simplify the process of testing and interacting with contracts by projecting the development of contracts such as ink! This tool is developed by [Patract Labs](https://patract.io/products). Kudos!

{% hint style="info" %}
Please lear more from [here](https://docs.patract.io/en/redspot/introduction.html).
{% endhint %}

## Set Up

First of all, let's install [Node.js](https://nodejs.org/). The version have to be version &gt;= 12.0. You can check your version by using following command. `$ node --version`

Second, ink! contract requires a WASM compile environment. Let's install toolchain.

```text
rustup install nightly
rustup component add rust-src --toolchain nightly
rustup target add wasm32-unknown-unknown --toolchain nightly
rustup component add rust-src --toolchain nightly
```

And let's  install cargo-contract provided by Parity Technologies. 

```text
cargo install cargo-contract --force
```

## Create a Redspot Project

Redspot provides a sample contract like [Truffle](https://www.trufflesuite.com/) that accelerates secure smart contract developments.  

{% hint style="info" %}
Currently, only ERC20 contract is supported but more templates will be provided by [Patract Labs](https://patract.io/). 
{% endhint %}

```text
npx redspot-new erc20
```

![](../../../.gitbook/assets/screen-shot-2021-04-16-at-17.55.07.png)

## Compile the Contract

Before compiling, install `npm` dependencies first.

```text
npm install
```

Work In Progress

