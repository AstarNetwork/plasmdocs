---
description: Polkadot parachain
---

# Plasm Network

This page describes the specs of Plasm mainnet in detail. The behavior of Plasm mainnet changes as the network grows.

Note that the past status is also listed here. Each detailed spec is annotated at the beginning of the page, whether it is "Latest" or "Deprecated".

## Previous Works

### Core Modules

* **System** - core substrate functionality
* **Timestamp** - timestamp runtime oracle
* **Session** - authority session keys management
* **Babe** - block producing consensus engine
* **Grandpa** - block finalizing consensus engine
* **Indices** - account indexing engine
* **Balances** - native asset operations
* **RandomnessCollectiveFlip** - source of random numbers
* **Contracts** - smart contract support
* **Sudo** - superuser actions
* **EVM**  - Ethereum Virtual Machine support

### Plasm Network Original modules

* **Operator** - smart contract operator support
* **PlasmValidator** - authority manager for Plasm network
* **PlasmRewards** - this module split block rewards between dApps operators and validators
* **DApps Staking** - Basic income for dApps developers
* **OVM** - Optimistic Virtual Machine support
* **Plasma** - Plasma supports

Learn more from [here](https://github.com/PlasmNetwork/Plasm/blob/dusty/bin/node/runtime/Cargo.toml).

## Road Map

The below is the milestone for Plasm Network as a public blockchain. The milestone in this context refers to the rough timeline and the journey that Plasm Network will have to take in order to become a fully public DAO, which is our vision. The items and their date described here are not strict nor completely dependent like a waterfall framework. The purpose of this milestone is to understand what are the requirements for Plasm Network to become a DAO and how far we are until achieving that goal.

### 2021 May and June

* Complete staking functionalities \(both PoS and DApps Staking\)
* Launch Shiden Network as a Kusama Parachain & Plasm Network Portal 
* Start Shiden Grant Program
* Start Plasm Grit Acceleration Program

### 2021 July and August

* Rebranding  
* Complete L2 implementation with OVM and ZK Rollups

### 2021 September and October

* Redenomination
* Launch Plasm Network as a Polkadot Parachain
* Enable transaction
* Start Plasm Grant Program

### 2022

* Implement and enable treasury and democracy modules
* Make Plasm team into a full DAO

  If you would like to learn more,  please join our [Discord](https://discord.gg/Z3nC9U4).

