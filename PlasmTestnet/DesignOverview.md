Plasm Testnet Design
====================

> Main aim of Plasm Testnet is experimental network for community integration and public tests.

Versioning
----------

- spec-name: plasm-testnet
- impl-name: plasm-testnet-node

Version naming notion:

- For authoring version, it just equals to the testnet generation spec, testnet generation will not change authoring interface.
- For spec/impl versions, two numbers are used, the high number is for testnet generation, the low number for testnet runtime upgrades (probably we will have no more than 9 patch fixes for testnet generation). Example: 10 for Testnet v1 genesis, 21 for Testnet v2 patch 1.

Testnet generation could be or not compatible with old network. In my opinion, for testnets periodic blockchain wipe isn't bad, it helps resource saving for testnet participants.

**Estimated life cycle for testnet generation is approximately from two weeks to two months.**

## Testnet migration guidelines

Testnet upgrade could be two types:

- major upgrade
- minor runtime patch

Runtime upgrade is acceptable for minor patches, end users should not notice a change of this upgrade. It’s an easy way to introduce small non breakable features / patches for the network.

For the major upgrade the high version number is changed and testnet version is increased. This mean that testnet started from scratch. Major updates could be used for introducing breakable features or blockchain wipes for network participants' resource-saving.

# Plasm Testnet v2

This testnet is used for testing manual management of community validators and experiment with permission for validating blocks for community members as same as integration with ink-playground contract upload sandbox.

## Version

- authoring_version: 2
- spec_version: 20
- impl_version: 20

## Modules

List of enabled runtime modules.

### Core modules

- System - core substrate functionality.
- Timestamp - timestamp runtime oracle.
- Session - authority session keys management.
- Babe - block producing consensus engine.
- Grandpa - block finalizing consensus engine.
- Indices - account indexing engine.
- Balances - native asset operations.
- RandomnessCollectiveFlip - source of random numbers.
- Contracts - smart contract support.
- Sudo - superuser actions.

### StakeTechnologies modules

- Operator - smart contract operators.
- SessionManager - PoA validator management.

# Plasm Testnet v3

This is a reference network for future mainnet. 

Planned features:

- token distribution according to lockdrop results;
- operator staking;
- validator rewards.

## Version

- authoring_version: 3
- spec_version: 30
- impl_version: 30

### Core modules

- System - core substrate functionality.
- Timestamp - timestamp runtime oracle.
- Session - authority session keys management.
- Babe - block producing consensus engine.
- Grandpa - block finalizing consensus engine.
- Indices - account indexing engine.
- Balances - native asset operations.
- RandomnessCollectiveFlip - source of random numbers.
- Contracts - smart contract support.
- Sudo - superuser actions.

### StakeTechnologies modules

- Operator - smart contract operator support.
- PlasmStaking - Plasm operator nominating and rewards support.
