---
description: Plasma and beyond.
---

# Optimistic Virtual Machine

### What is Optimistic Virtual Machine?

The OVM \(Optimistic Virtual Machine\) is a virtual machine designed to support all layer 2 protocols. It is a possible unification of all layer 2 protocols meaning: **Plasm Network will not only be for Plasma applications but also for Lightning Network applications or any other layer 2 protocols.**

Plasm Network will house all layer 2 scaling solutions. Users can choose which solution to use and make their use case possible with minimum overhead.

### Learn More

The OVM is a powerful concept in layer 2 applications. We can express complex dispute logics by a simple OVM language and that language contains [Optimistic Game Semantics](https://plasma.group/optimistic-game-semantics.pdf) \(OGS\).

For example, we can express Plasma checkpoint and exit claims with 2 simple definitions \(we call these "property"\) by OGS. Plasm Network separates the OVM from the smart contract and prepares it as a module so that OVM can be used more simply and conveniently.

### OVM in Plasm Network <a id="ovm-in-plasm-network"></a>

The OVM and its surrounding architecture are as shown in the figure below.

![ovmodule](https://user-images.githubusercontent.com/6259384/75546609-404d5880-5a6c-11ea-84d0-f063e0bc252c.png)

Plasma applications \(Plapps\) can be created and run properly through the dedicated client application L1 adapter. Plapps are composed of OVM, Plasma, and contract modules in the Plasm Network.

In the case of Ethereum Plasma applications, everything provided in these modules was managed by smart contracts. This makes it difficult to predict the gas cost when running a plasma application containing complicated logic. Also, building applications that combine multiple contracts can be confusing for developers.

For this reason, Plasma Network has considered a superficially concise and easy-to-understand configuration by separating the roles into three modules. The OVM Module implements a function called Universal Adjudication to initiate a dispute if the user finds a mistake in the information on layer 1. The Plasma Module supports a common implementation of some of the essential smart contracts. Only the implementations that require different logic are managed by the Contracts Module.

This Plasm Network logic can be combined with the Plasma Layer 2 implementation described above to build an application.

You can see the details below.

## Smart Contract <a id="smart-contract"></a>

Smart contracts in Plasm Network's layer 2 applications require **ERC20 Contracts** and **Payout Contracts**. Each layer 2 application developers must implement their own smart contract.

### ERC20 Contract <a id="erc20-contract"></a>

ERC20 Contract is a contract that expresses tokens handled by layer 2 application. Refer to this specification for [ERC20](https://eips.ethereum.org/EIPS/eip-20). PLM wrapped Contracts are the default ERC20 Contract.

#### wPLM contract <a id="wplm--contract"></a>

wPLM contract is a wrapped contract of PLM token. This is an ERC20 token issued by depositing the PLM token, the basic token of Plasm Network with the contract. In other words, it has the same value as PLM, like [wETH](https://weth.io/jp/).

### Payout Contract <a id="payout-contract"></a>

Payout Contract is a contract that handles returning tokens from layer 2 to layer 1. Layer 2 application developers must include this contract for users to be able to withdraw from layer 1. **Ownership payout contract** is the default payout contract.

Payout contract must be able to call the `finalizeExit` method.

```text
function finalizeExit(
    address depositContractAddress,
    types.Property memory _exitProperty,
    uint256 _depositedRangeId,
    address _owner
)
```

#### Ownership payout contract <a id="ownership-payout-contract"></a>

Ownership payout contract is a contract that the token owner can withdraw. Specifically, When the Exit is determined to be true in the Challenge Game, the owner represented by that State Object \(in this case, OwnershipPredicate\) can withdraw the token. The Ownership Payout contract is expressed in the Ethereum contract like [this](https://github.com/cryptoeconomicslab/ovm-contracts/blob/master/contracts/Predicate/plasma/OwnershipPayout.sol).

## Modules <a id="modules"></a>

Operations related to OVM are implemented by the Substrate runtime module. This is so that users do not have to deploy complex smart contracts. This is intended to make gas costs of deployment cheap and easy to estimate. In addition, this allows developers of layer 2 applications to implement only essentially required "ERC20 contract" and "Payment contract" and properties.

special storage that can handle the layer 2 application must be considered with the Substrate Runtime Module. It treats one application as one AccountId in the same way as a smart contract.

It can be divided into OVM Modules, which perform general OVM processing, and Plasma modules, which are responsible for plasma-specific processing. See the architecture diagram for the dependencies of each module and contract.

## OVM Module <a id="ovm-module"></a>

OVM Module describes the processing commonly performed in OVM. Specifically, the execution logic of predicate is included in this module. In addition, the smart contract is executed by using the truth of predicate as a trigger. This module is a modularized version of [Universal Adjudication contract](https://github.com/cryptoeconomicslab/ovm-contracts/blob/master/contracts/UniversalAdjudicationContract.sol) in the Ethereum Smart contract.

### Types <a id="types"></a>

Defines the type used by OVM Module.

```text
pub struct Predicate(Vec<u8>);

pub struct Property<AccountId> {
    predicate_address: AccountId,
  // Every input are bytes. Each Atomic Predicate decode inputs to the specific type.
    inputs: Vec<u8>,
}

pub enum Decision {
    Undecided,
    True,
    False
}

pub struct ChallengeGame<AccountId, BlockNumber> {
    property: Property<AccountId>,
    challenges: Vec<u8>,
    decision: Decision,
    created_block: BlockNumber,
}

pub struct Range<Balance> {
    start: Balance,
    end: Balance,
}
```

### Universal Adjudication <a id="universal-adjudication"></a>

#### Constants <a id="contants"></a>

```text
/// During the dispute period defined here, the user can challenge. If nothing is found, the state is determined after the dispute period.
type DISPUTE_PERIOD: T::Moment = 7;
```

#### Storage <a id="storage"></a>

```text
decl_storage! {
    Predicate get(fn predicate): map T::AccountId => T::Predicate;
    DisputePeriod get(fn dispute_period): T::Moment;
    InstantiatedGames get(fn instantiated_games): map T::Hash => T::ChallengeGame;
}
```

#### Modules <a id="modules"></a>

```text
decl_storage! {
    fn deploy(predicate: T::Predicate);
    fn claim_property(claim: T::Property);
    fn decide_claim_to_true(game_id: T::Hash);
    fn decide_claim_to_false(game_id: T::Hash, challenging_game_id: T::Hash);
    fn remove_challenge(game_id: T::Hash, challenging_game_id: T::Hash);
    fn set_predicate_decision(game_id: T::Hash, decision: bool);
    /**
   * @dev challenge a game specified by gameId with a challengingGame specified by _challengingGameId
   * @param _gameId challenged game id
   * @param _challengeInputs array of input to verify child of game tree
   * @param _challengingGameId child of game tree
   */
    fn challenge(game_id: T::Hash, challenge_inputs: Vec<u8>, challenging_game_id);

    /// callable
    fn is_decided(property: T::Property);
    fn get_game(claim_id: T::Hash);
    fn get_property_id(property: T::Property);
}
```

#### Events <a id="events"></a>

```text
// (predicate_address: AccountId);
DeployPredicate(AccountId);
// (gameId: Hash, decision: bool)
AtomicPropositionDecided(Hash, bool);
// (game_id: Hash, property: Property, createdBlock: BlockNumber)
NewPropertyClaimed(Hash, Property, BlockNumber);
// (game_id: Hash, challengeGameId: Hash)
ClaimChallenged(Hash, Hash);
// (game_id: Hash, decision: bool)
ClaimDecided(Hash, bool);
// (game_id: Hash, challengeGameId: Hash)
ChallengeRemoved(Hash, Hash);
```

## Plasma Module <a id="plasma-module"></a>

Plasma Module is a module that is responsible for processing specific to Plasma. It calls the OVM Module and the specified smart contract function. The Plasma Module has one "Commitment" and "Deposit" address per application. These are each defined by `decl_child_storage`. `decl_child_storage!` is a macro that implements DB in SubTrie. This sets AccountId as the key value. This is like a contract address that implements with reference to [AccountDb](https://github.com/paritytech/substrate/blob/master/frame/contracts/src/account_db.rs) of contract module.

This is modularized [Commitment](https://github.com/cryptoeconomicslab/ovm-contracts/blob/master/contracts/CommitmentContract.sol), [Deposit](https://github.com/cryptoeconomicslab/ovm-contracts/blob/master/contracts/DepositContract.sol) and [CompiledPredicate](https://github.com/cryptoeconomicslab/ovm-contracts/blob/master/contracts/Predicate/CompiledPredicate.sol) contracts in the Ethereum.

### Types <a id="types"></a>

Defines the type used by Plasma Module.

```text
pub struct StateUpdate<AccountId, Balance, BlockNumber> {
    deposit_contract_address: AccountId,
    ragne: Range<Balance>,
    block_number: BlockNumber,
    state_object: Property<AccountId>,
}

pub struct Checkpoint<AccountId, Balance> {
    subsrange: Range<Balance>,
    state_update: Property<AccountId>,
}

pub struct Exit<AccountId, Range, BlockNumber, Property, Balance, Index> {
    state_update: StateUpdate<AccountId, Range, BlockNumber, Property>,
    inclusion_proof: InclusionProof<AccountId, Balance, Index>
}

pub struct InclusionProof<AccountId, Balance, Index> {
    address_inclusion_proof: AddressInclusionProof<AccountId, Index>
    interval_inclusion_proof: IntervalInclusionProof<Balance, Index>,
}

pub struct IntervalInclusionProof<Balance, Index> {
    leaf_index: Index,
    leaf_position: Index,
    sibilings: Vec<IntervalTreeNode<Balance>>
}

pub struct AddressInclusionProof<AccountId, Index> {
    leaf_index: AccountId,
    leaf_position: Index,
    siblings: Vec<AddressTreeNode<AccountId>>,
}

pub struct IntervalTreeNode<Balance> {
    data: Vec<u8>,
    start: Balance,
}

pub struct AddressTreeNode<AccountId> {
    data: Vec<u8>,
    token_address: AccountId,
}
```

#### modules <a id="modules"></a>

```text
/// Commitment constructor + Deposit constructor
fn deploy(
    aggregator_address: T::AccountId,
    erc20: T::AccountId,
    state_update_predicate: T::AccountId);
```

### Commitment <a id="commitment"></a>

Commitment is something to save the Merkle Root owned by the Plasma child chain. Child storage of Commitment is generated for each layer 2 application. This can be used for accessing smart contracts.

#### Storage <a id="storage"></a>

```text
// Commitment storage: Plapps address => Commitment Child Storage.
Commitment get(fn commitment): T::AccountId => Commitment;
```

```text
decl_child_storage! {
    Commitment {
        // Single operator address: OperatorId
        OperatorAddress get(fn operator_address): T::AccountId;
        // Current block number of commitment chain: BlockNumber
        CurrentBlock get(fn current_block): T::BlockNumber;
        // History of Merkle Root
        Blocks get(fn blocks): map u128 => T::Hash
    }
}
```

### Modules <a id="modules"></a>

```text
decl_modules! {
    fn submitRoot(blk_number: u64, root: T::Hash); 

  /**
   * verifyInclusion method verifies inclusion of message in Double Layer Tree.
   * The message has range and token address and these also must be verified.
   * Please see https://docs.plasma.group/projects/spec/en/latest/src/01-core/double-layer-tree.html for further details.
   * @param _leaf a message to verify its inclusion
   * @param _tokenAddress token address of the message
   * @param _range range of the message
   * @param _inclusionProof The proof data to verify inclusion
   * @param _blkNumber block number where the Merkle root is stored
   */
    fn verifyInclusion(leaf: T::Hash, address, T::AccountId, range: T::Range, inclusionProof: InclusionProof, blk_number);
}
```

### Events <a id="events"></a>

```text
// Event definitions (AccountID: PlappsAddress, BlockNumber, Hash: root)
BlockSubmitted(AccountId, BlockNumber, Hash);
```

### Deposit <a id="deposit"></a>

Deposit allows depositing ERC20 tokens from layer 1 to layer 2. Child storage of Deposit is generated for each layer 2 application. This can be used like accessing smart contracts.

#### Storage <a id="storage"></a>

```text
// Deposit storage: Plapps address => Deposit Child Storage.
Deposit get(fn deposit): T::AccountId => Deposit;

decl_child_storage! {
    Commitment {
    ERC20 get(fn erc20): T::AccountId;
    CommitmentContract get(fn commitment_contract): T::AccountId;
    UniversalAdjudicatinonContract get(fn universalAdjudicationContract);
    StateUpdatePredicate get(fn state_update_predicate): T::AccountId;

    TotalDeposited get(fn total_deposited): T::Balance;
    DepositedRanges get(fn deposited_ranges): map T::Balance => T::Range;
    Checkpoints get(fn checkpoints): map T::Hash => T::Checkpoint;
    }
}
```

#### Modules <a id="modules"></a>

```text
decl_modules! {
    fn deposit(amount: T::Balance, initial_state: T::Property);
    fn extend_deposited_ranges(amount: T::Balance);
    fn remove_deposited_range(range: T::Range, depositedRangeId: T::Balance);
    fn finalize_check_point(checkpoint_property: T::Property);
    fn finalizeExit(exit_property: T::Property, deposited_range_id: T::Balance);

    /// callable
    fn is_subrange(subrange: T::Range, surroundingRange T::Range);
}
```

#### Events <a id="events"></a>

```text
// (checkpointId: Hash, checkpoint: Checkpoint);
CheckpointFinalized(Hash, Checkpoint);
// (exit_id: Hash)
ExitFinalized(Hash);
// (new_range: Range)
DepositedRangeExtended(Range);
// (removed_range: Range)
DepositedRangeRemoved(Range);
```

### Compiled Predicate <a id="compiled-predicate"></a>

The role of `CompiledPredicate` is optimizing claim size by compiling complex proposition to one simple predicate. The Plasma Module has a method for running layer 2 applications via Predicate. `PayoutContract` withdrawal processing that exists for each layer 2 application can only be called via Compiled Predicate. This allows for transactions on layer 2 to be as secure as layer 1.

#### Storage <a id="storage"></a>

```text
/// predicate address => payout address
PayoutContractAddress get(fn payout_contract_address): map T::AccountId => T::AccountId;
```

#### Modules <a id="modules"></a>

```text
fn decide_true(predicate_address: T::AccountId, inputs: Vec<u8>, witness: Vec<u8>);

/// callable
fn is_valid_challenge(predicate_address: T::AccountId, inputs: Vec<u8>, challenge_inputs: Vec<u8>, challenge: T::Property);
fn decide(predicate_addres: T::AccountId, inputs: Vec<u8>, witness: Vec<u8>);
```

Questions? find answers here =&gt; [Discord Tech Channel](https://discord.gg/Z3nC9U4).

