# Mainnet Chain Spec.

## System

- key: code
- type: `Vec<u8>`
- value: `WASM_BINARY.to_vec()`

#### remarks
The wasm binary in build.


|value|remarkds|refs|
|--|--|--|
|`WASM_BINARY.to_vec()`|The wasm binary in build.| - |

### changes_trie_config: `Option<ChangesTrieConfiguration>`

|value|remarkds|refs|
|--|--|--|
|`Default::default()`|The wasm binary in build.| https://crates.parity.io/sp_core/struct.ChangesTrieConfiguration.html |

<!-- 
## Balances
|Key|Value|Remarks|Ref|Type|
|----|----|----|----|----|
|balances|`HOLDERS`|The holders of lockdrop participant(85%) + stake root user(15%).|[https://github.com/staketechnologies/Plasm/blob/dusty/bin/node/runtime/src/constants.rs#L23](https://github.com/staketechnologies/Plasm/blob/dusty/bin/node/runtime/src/constants.rs#L23)|`Vec<(T::AccountId, T::Balance)>`|

## Indices
|Key|Value|Remarks|Ref|Type|
|----|----|----|----|----|
|indices|`vec!{}`|Empty.
If new account will be gerated, allocates account short address.| |`Vec<(T::AccountIndex, T::AccountId)>`| -->