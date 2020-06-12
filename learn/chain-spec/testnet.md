# Testnet

{% hint style="info" %}
The Plasm Testnet is a public test environment for developers and community integration's. This is where debugging should occur prior to mainnet deployment.
{% endhint %}

### Versioning <a id="versioning"></a>

* spec-name: plasm-testnet
* impl-name: plasm-testnet-node

Version naming notation:

* Authoring version: Equals testnet generation spec. Testnet generation will not change authoring interface.
* Spec/Impl Versions: High number = testnet generation; low number = testnet runtime upgrades. Example: 10 for Testnet v1 genesis, 21 for Testnet v2 Patch 1.

Testnet generation my not be backwards compatible with old networks. A periodic blockchain wipe is suggested for compatibility and to keep testnet resources available for other users.

**Testnet generation life cycle is estimated to be between two weeks and two months**

### Testnet Migration Guidelines <a id="testnet-migration-guidelines"></a>

Testnet upgrade types fall into one of two categories:

* Major upgrade
* Minor runtime patch

Runtime patches have a minor impact and end users should not notice any changes. These patches are non breakable features and minor network maintenance patches.

Major upgrades occur when the testnet is completely rebuilt including major upgrades and changes from the previous version. These upgrades increase the version number. These upgrades can include breaking changes or entire blockchain wipes to optimize user resources.

## Dusty Plasm <a id="dusty-plasm"></a>

The Plasm `canary` network is a `beta` Mainnet. **Dusty** observe and debug mainnet code for approximately two weeks.

### Incentives <a id="incentives"></a>

Dusty network participation is incentivized, paying rewards in PLD \(network native token\) to PoA validators and dApps operator nominators.

> When Plasm Network token stake technology is implemented, **0.5%** of the total Plasm token supply will be airdropped to Dusty token holders.

Planned features:

* Multi-lockdrop
* Optimistic Virtual Machine

### Version <a id="version"></a>

* authoring\_version: 4
* spec\_version: 40
* impl\_version: 40

#### Core modules <a id="core-modules"></a>

* System - core substrate functionality
* Timestamp - timestamp runtime oracle
* Session - authority session keys management
* Babe - block producing consensus engine
* Grandpa - block finalizing consensus engine
* Indices - account indexing engine
* Balances - native asset operations
* RandomnessCollectiveFlip - source of random numbers
* Contracts - smart contract support
* Sudo - superuser actions

#### StakeTechnologies modules <a id="staketechnologies-modules"></a>

* Operator - smart contract operator support
* dApps staking - stake on decentralized application to collect operator rewards
* PlasmValidator - authority manager for Plasm network
* PlasmRewards - reward router between dApps operators and validators
* PlasmLockdrop - multi-lockdrop token distribution

## Plasm Testnet v3 <a id="plasm-testnet-v3"></a>

This is a reference network for future mainnet.

Planned features:

* Token distribution according to lockdrop results;
* Operator staking;
* Validator rewards.

### Version <a id="version"></a>

* authoring\_version: 3
* spec\_version: 30
* impl\_version: 30

#### Core modules <a id="core-modules"></a>

* System - core substrate functionality
* Timestamp - timestamp runtime oracle
* Session - authority session keys management
* Babe - block producing consensus engine
* Grandpa - block finalizing consensus engine
* Indices - account indexing engine
* Balances - native asset operations
* RandomnessCollectiveFlip - random number generator
* Contracts - smart contract support
* Sudo - superuser actions

#### StakeTechnologies modules <a id="staketechnologies-modules"></a>

* Operator - smart contract operator support
* PlasmStaking - Plasm operator nominating and rewards support

## Plasm Testnet v2 <a id="plasm-testnet-v2"></a>

This environment is for testing manual management of community validators and experimenting with permissions for validating blocks. It is the same integration with the ink-playground contract upload sandbox.

### Version <a id="version"></a>

* authoring\_version: 2
* spec\_version: 20
* impl\_version: 20

### Modules <a id="modules"></a>

List of enabled runtime modules.

#### Core modules <a id="core-modules"></a>

* System - core substrate functionality
* Timestamp - timestamp runtime oracle
* Session - authority session keys management
* Babe - block producing consensus engine
* Grandpa - block finalizing consensus engine
* Indices - account indexing engine
* Balances - native asset operations
* RandomnessCollectiveFlip - random number generator
* Contracts - smart contract support
* Sudo - superuser actions

#### StakeTechnologies modules <a id="staketechnologies-modules"></a>

* Operator - smart contract operators
* SessionManager - PoA validator management


