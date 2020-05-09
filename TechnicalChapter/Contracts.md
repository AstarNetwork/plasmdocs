# Plasm Contracts

Plasm Contracts are written in ink!, a Rust--based embedded domain specific language for writing smart contract for Substrate. By using Plasm Contract libraries, developers can make a Plasma parent chain contract that meets a Plasma standard. Plasm Contract provides Trait which describes Plasma standard implementations, a generalized data structure, and a Plasma Cash implementation which is created based on the Plasma Group Specification.

## ink!

ink! is a Rust--based embedded domain specific language for writing smart contracts on Substrate. ink! is currently under development and rapid changes. If you want to use ink!, install Substrate Runtime Module Library into Substrate chain. Internally, WebAssembly is used. A user can deploy smart contracts by uploading the bytecode of WASM file.

For the further information, please check out [this article](https://substrate.dev/docs/en/next/contracts/faq#ink).

## Plasm PGSpec (Plasma Group Specification) Design

Originally, Plasma PGSpec is designed for Ethereum. Of course, ink! has different features from that of Solidity and Vyper. Since we are developing Plasma on Substrate, it is necessary for us to implement a more suitable feature. Ink! which is written in Rust does not have a concept of inheritance, but has a function to describe the characteristics of the structure called Trait.
This function is suitable to express a generalized specification like PGSpec. The Plasm team decided to make a PGSpec by using ink!.

By using this standard implementation, developers can implement their PlasmaContract that meets the Trait depending on their needs.

## Archtecture

Plasm PGSpec has the following structure.

| ![PGSpec structure](https://user-images.githubusercontent.com/6259384/64493921-4cc4d580-d2c1-11e9-9e0b-f0e546be9ae6.png) |
| :--: |
| *Plasm contract architecture* |

<https://github.com/stakedtechnologies/Plasm/tree/master/contracts>

Plasm PGSpec offers the following functions:

### Commitment

This component has all block headers (Merkle Tree) of a child chain. It verifies the block creation of an operator on the child chain and the status.  As a default standard, Merkle Interval Tree (Below) is implemented to reference ranges of state objects simultaneously.

| ![Merkle Interval Tree(ref: https://docs.plasma.group/projects/spec/en/latest/src/01-core/merkle-interval-tree.html)](https://user-images.githubusercontent.com/6259384/64493987-2b181e00-d2c2-11e9-8936-e78c00f767c9.png) |
| :--: |
| *Merkle Interval Tree（ref: https://docs.plasma.group/projects/spec/en/latest/src/01-core/merkle-interval-tree.html)* |

Documentation:

```bash
cd plasm/contracts/commitment
cargo doc --open
```

### Deposit

This manages the assets that were deposited on a Plasma child chain. The deposited assets are transferred on the child chain ,and just the legitimate owner can exit from the child chain to the parent chain. As a standard-setting, a Plasma exit game logic which does not rely on tokens is implemented. Figure5 is a transaction diagram of an exit game. The role of each checkpoint is to prove that all states before the pointed block number are correct.

To Do: Make these sentences understandable.

| ![ExitGame state machine diagram](https://user-images.githubusercontent.com/6259384/64494002-56027200-d2c2-11e9-8b05-7e09acec461e.png) |
| :--: |
| *ExitGame state machine diagram* |

Documentation:

```bash
cd plasm/contracts/deposit
cargo doc --open
```

### Predicate

Predicate is a smart contract that defines an original logic of an exit game. For example, the most fundamental logic is `DeprecateExit` which makes an outdated exit invalid.

Predicates can be used as fully customized extensions to the base plasma cash exit game. In this sense, Predicate is a generalized Plasma Cash. In other words, Plasma Cash can only handle currencies and Predicate extends the ability to assets.

As a standard design, Ownership Predicate is provided. The contract manages the information of token holders. A digital signature of the owner is required when the state is changed.

Documentation:

```bash
cd plasm/contracts/predicate
cargo doc --open
```

### Primitive

Common Plasma contract structures and the features are provided as a set of Primitive libraries.

Documentation:

```bash
cd plasm/contracts/primitives
cargo doc --open
```

### BalanceContract

Every asset on a Plasma contract needs to be confirmed to ERC20 standard. The Plasm team  provides customized balance contracts to use ERC20 on Substrate.

Documentation:

```bash
cd plasm/contracts/balances
cargo doc --open
```

### PlasmaCashContract

Plasma contract which has equivalent functions to Plasma Cash is implemented. More specifically, it consists of Ownership Predicate, Deposit, and Commitment on the figure3.

To do: More explanation is needed.

Documentation:

```bash
cd plasm/contracts/cash
cargo doc --open
```
