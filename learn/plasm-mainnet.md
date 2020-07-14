# Plasm Mainnet 🆙

This page describes the specs of Plasm mainnet in detail. In addition, the behavior of Plasm mainnet changes as the network grows. 

Note that the past status is also listed here. Each detailed spec is annotated at the beginning of the page, whether it is "Latest" or "Deprecate".

## Previous Works

### Version

* authoring\_version: 1
* spec\_version: 1
* impl\_version: 1

### Core Modules

* **System** - core substrate functionality.
* **Timestamp** - timestamp runtime oracle.
* **Session** - authority session keys management.
* **Babe** - block producing consensus engine.
* **Grandpa** - block finalizing consensus engine.
* **Indices** - account indexing engine.
* **Balances** - native asset operations.
* **RandomnessCollectiveFlip** - source of random numbers.
* **Contracts** - smart contract support.
* **Sudo** - superuser actions.

### Plasm Network Original modules

* Operator - smart contract operator support.
* PlasmValidator - authority manager for Plasm network.
* PlasmRewards - this module split block rewards between Dapp operators and validators.

## Future Works

### 2020 Q2

* [Dapps Staking](../PlasmNetwork/DappsRewards.md) module will be available.

### 2020 Q3

* [Ovm + Plasma](../TechnicalChapter/OVM.md) module will be available.
* [Real time Lockdrop](../PlasmNetwork/RealtimeLockdrop.md) module will be available.

### 2020 Q4

* First L2 application will be released.
* L2 interoperability between ETH.
* Migrate to NPoS from PoA.

### 2020

* Plasm Network as Parachain join the Polkadot.

