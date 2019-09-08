# About Plasm Contracts

Plasm has chosen to implement it as a smart contract using ink! As a way to implement this specification in Substrate. This is because Plasma Chain must be freely customizable and deployable by the user. Such flexibility cannot be realized by implementation using a module that customizes Substrate (commonly known as SRML: Substrate Runtime Module Library).

## ink!
ink! is a standard smart contract that can be handled by Substrate above. This is currently under development and can be described using a programming language called Rust. If you want to use smart contracts with ink !, install SRML Contract Module in Substrate Chain. Internally, WebAssembly is used like SRML. The user can deploy smart contracts by uploading the bytecode of WASM that was compiled at hand on Substrate. Please check [here](https://substrate.dev/docs/en/next/contracts/faq#ink).

## Plasm PGSpec Design
Plasma PGSpec is designed on the assumption that the standard implementation is done with Ethereum. Substrate's smart contract ink! Has different specifications from Ethereum's smart contract Solidity (Vyper), so it is necessary to implement a more suitable implementation. Ink! Written in Rust does not have an inheritance, but has a function to describe the characteristics of the structure called Trait. This function that describes the properties that a Contract must-have is considered suitable for expressing general specifications such as PGSpec. Therefore, Plasm decided to take the form that provides the standard implementation and the characteristics that must be combined as PGSpec. Depending on the various use cases, developers can implement their PlasmaContract that meets the Trait provided by Plasm regarding the standard implementation. By doing so, the Rust compiler will verify that it meets the specifications for PlasmaContract. Developers can develop PlasmaContract whose specifications are guaranteed by the compiler.

## Archtecture
Plasm PGSpec has the following structure.

| ![](https://user-images.githubusercontent.com/6259384/64493921-4cc4d580-d2c1-11e9-9e0b-f0e546be9ae6.png) |
| :--: |
| *Plasm contract archtecture* |

Plasm PGSpec offers the following functions:

### Commitment
Holds the PlasmaChain block header (MerkleRoot). The operator creates a new block and verifies that the block contains a state.
The standard implementation provides an implementation that assumes the use of block inclusion proof using MerkleIntervalTree.

| ![Merkle Interval Tree(ref: https://docs.plasma.group/projects/spec/en/latest/src/01-core/merkle-interval-tree.html)](https://user-images.githubusercontent.com/6259384/64493987-2b181e00-d2c2-11e9-8936-e78c00f767c9.png) |
| :--: |
| *Merkle Interval Tree（ref: https://docs.plasma.group/projects/spec/en/latest/src/01-core/merkle-interval-tree.html)* |

Documentation:
```
$ cd plasm/contracts/commitment
$ cargo doc --open
```

### Deposit
Manage assets deposited in PlsmaChain. Deposited assets are traded on PlasmaChain, providing a mechanism that only the rightful owner can exit to the parent chain. This includes most of the logic of PlasmaExitGame.
The standard implementation provides an ExitGame implementation that does not rely on PlasmaChain tokens. Here is a state transition diagram for ExitGame that focuses on the checkpoints for the following states: Checkpoints ensure that all state transitions before a specified block height for a given NFT are correct.

| ![ExitGame state machine diagram](https://user-images.githubusercontent.com/6259384/64494002-56027200-d2c2-11e9-8b05-7e09acec461e.png) |
| :--: |
| *ExitGame state machine diagram* |

Documentation:
```
$ cd plasm/contracts/deposit
$ cargo doc --open
```

### Predicate
Define your own ExitGame rules. The most basic is to write DeprecateExit, which is the logic that invalidates some exits. Normally, this logic is used to prove that a transaction has been invalidated. Predicate is a generalized PlasmaCash. Therefore, PlasmaCash can be expressed using Predicate.
The standard implementation provides a Predicate called Ownership Predicate that has only owner information as a state object. The state transition requires the signature of the owner of the state object before the transition. This provides the full functionality needed for PlasmaCash.

Documentation:
```
$ cd plasm/contracts/predicate
$ cargo doc --open
```

### Primitive
Provided as a Primitive library for structures and properties commonly used in PlasmsaContract.

Documentation:
```
$ cd plasm/contracts/primitives
$ cargo doc --open
```

### BalanceContract
Assets handled by PlasmaContract must be prepared according to ERC20. Plasm will prepare BalanceContract as standard to treat Substrate's key currency as an ERC20 compliant contract. Think of it as WrappedETH in Ethereum.

Documentation:
```
$ cd plasm/contracts/balances
$ cargo doc --open
```

### PlasmaCashContract
PlasmaContract with functions corresponding to PlasmCash is implemented as a standard implementation. This is achieved by combining the standard implementation of Ownership Predicate, which is the standard implementation of Predicate, and the standard implementation of Deposit, Commitment.

Documentation:
```
$ cd plasm/contracts/cash
$ cargo doc --open
```
