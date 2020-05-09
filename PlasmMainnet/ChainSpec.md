# Mainnet Chain Spec

This section describes Mainnet's genesis chain spec distributed [here](https://github.com/staketechnologies/Plasm/blob/v1.0.0/bin/node/cli/res/plasm.json).

## System

|Key|Value|Types|Remarks|Refs|
|--|--|--|--|--|
|code|`WASM_BINARY.to_vec()`|`Vec<u8>`|The wasm binary in build.| |
|change_trie_config|`Default::default()`|`Option<ChangesTrieConfiguration>`| | <https://crates.parity.io/sp_core/struct.ChangesTrieConfiguration.html> |

## Balances

|Key|Value|Type|Remarks|Ref|
|----|----|----|----|----|
|balances|`HOLDERS`|`Vec<(T::AccountId, T::Balance)>`|The holders of lockdrop participant(85%) + stake root user(15%).|[https://github.com/staketechnologies/Plasm/blob/dusty/bin/node/runtime/src/constants.rs#L23](https://github.com/staketechnologies/Plasm/blob/dusty/bin/node/runtime/src/constants.rs#L23)|

## Indices

|Key|Value|Type|Remarks|Ref|
|----|----|----|----|----|
|indices|`vec!{}`|`Vec<(T::AccountIndex, T::AccountId)>`|Empty. If new account will be generated, allocates account short address.| |

## Plasm rewards

|Key|Value|Type|Remarks|Ref|
|----|----|----|----|----|
|validators|[initial_authorities](https://github.com/staketechnologies/Plasm/blob/v1.0.0/bin/node/cli/src/chain_spec.rs#L196)|`Vec<T::AccountId>`|Initial authorities address.|[https://github.com/staketechnologies/Plasm/blob/v1.0.0/bin/node/cli/src/chain_spec.rs#L196](https://github.com/staketechnologies/Plasm/blob/v1.0.0/bin/node/cli/src/chain_spec.rs#L196)|

## Session

|Key|Value|Type|Remarks|Ref|
|----|----|----|----|----|
|keys|[initial_authorities](https://github.com/staketechnologies/Plasm/blob/v1.0.0/bin/node/cli/src/chain_spec.rs#L196)|`Vec<(T::AccountId, T::ValidatorId, T::Keys)>`|Initial authorities address. This is same of Plasm Validator's keys.|[https://github.com/staketechnologies/Plasm/blob/v1.0.0/bin/node/cli/src/chain_spec.rs#L196](https://github.com/staketechnologies/Plasm/blob/v1.0.0/bin/node/cli/src/chain_spec.rs#L196)|

## Babe

|Key|Value|Type|Remarks|Ref|
|----|----|----|----|----|
|authorities|`vec![]`|`Vec<(AuthorityId, AuthorityWeight)>`|Empty.
This is automatically inserted by `on_genesis_session`| |

## Grandpa

|Key|Value|Type|Remarks|Ref|
|----|----|----|----|----|
|authorities|`vec![]`|`Vec<(AuthorityId, AuthorityWeight)>`|Empty.
This is automatically inserted by `on_genesis_session`| |

## Contracts

|Key|Value|Type|Remarks|Ref|
|----|----|----|----|----|
|Congig::schedule|`Defeault::default()`|`Schedule`|Please see reference about default values.|[https://crates.parity.io/pallet_contracts/struct.Schedule.html](https://crates.parity.io/pallet_contracts/struct.Schedule.html)|
|Config::existential_deposit|`1 * MILLIPLM`|`BalanceOf<T>`|The default value. depends on `ExistentialDeposit`| |
|Config::tombstone_deposit|`1 * PLM`|`BalanceOf<T>`|The default value. depends on `TombstoneDeposit`| |
|Config::max_depth|`32`|`u32`|The maximum nesting level of a call/instantiate stack. The default value. Depends on `DefaultMaxDepth` on contract module.| |
|Config::max_value_size|`16_384`|`u32`|The maximum size of a storage value in bytes. Depends on `DefaultMaxValue` on contract module.| |
|Config::contract_account_instantiate_fee|`1 * MILLIPLM`|`BalanceOf<T>`|The fee required to instantiate a contract instance. Depends on `ContractFee`.| |
|gas_price|`1 * MILLIPLM`|`BalanceOf<T>`|The price of one unit of gas.| |

## Sudo

|Key|Value|Type|Remarks|Ref|
|----|----|----|----|----|
|key|[root_key](https://github.com/staketechnologies/Plasm/blob/v1.0.0/bin/node/cli/src/chain_spec.rs#L225)|`T::AccountId`|Root address|[https://github.com/staketechnologies/Plasm/blob/v1.0.0/bin/node/cli/src/chain_spec.rs#L225](https://github.com/staketechnologies/Plasm/blob/v1.0.0/bin/node/cli/src/chain_spec.rs#L225)|
