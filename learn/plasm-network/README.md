# Plasm Network

このページでは、Plasm mainnetのスペックについて詳しく説明します。Plasm mainnetの挙動はネットワークの成長に伴って変化します。 

過去のステータスも記載していますのでご注意ください。各詳細なスペックは、ページの冒頭に「最新」か「非推奨」かの注釈が付けられています。

## Previous Works

### Version

* authoring\_version: 1
* spec\_version: 1
* impl\_version: 1

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

### Plasm Network Original modules

* Operator - smart contract operator support
* PlasmValidator - authority manager for Plasm network
* PlasmRewards - this module split block rewards between dApps operators and validators

## Road Map

### 2020 Q2

* [dAppsStaking](https://github.com/staketechnologies/plasmdocs/tree/6321fe1f19becdbf1e329e0732b98b5d41274bc9/PlasmNetwork/dAppsRewards.md) module will be available

### 2020 Q3

* [Ovm + Plasma](https://github.com/staketechnologies/plasmdocs/tree/6321fe1f19becdbf1e329e0732b98b5d41274bc9/TechnicalChapter/OVM.md) module will be available
* [Real time Lockdrop](https://github.com/staketechnologies/plasmdocs/tree/6321fe1f19becdbf1e329e0732b98b5d41274bc9/PlasmNetwork/RealtimeLockdrop.md) module will be available

### 2020 Q4

* First L2 application will be released
* L2 interoperability between ETH
* Migrate to NPoS from PoA

### 2020

* Plasm Network joins Polkadot as a Parachain

