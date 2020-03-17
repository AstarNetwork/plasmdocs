# OVM

OVM(Optimistic Virtual Machine) is a powerful concept to develop Layer 2. We can express complex dispute logic by simple OVM language, and that language consists of [Optimistic Game Semantics](https://plasma.group/optimistic-game-semantics.pdf). For example, we can express Plasma checkpoint and exit claims with 2 simple definitions (we call these "property") by OGS. Plasm Network separates the OVM from the smart contract and prepares it as a module so that OVM can be used more simply and conveniently.

## OVM in Plasm Network

The OVM and its surrounding architecture are as shown in the below figure.

![ovmodule](https://user-images.githubusercontent.com/6259384/75546609-404d5880-5a6c-11ea-84d0-f063e0bc252c.png)

Plasma applications (Plapps) can be created and run properly through the dedicated client application L1 adapter. Plapps are composed of OVM, Plasma and Contracts modules in Plasm Network. In Plasma development at Ethereum, everything provided in these modules was managed by smart contracts. However, in that case, there is a problem that it is difficult to predict the gas cost when running a plasma application containing complicated logic. Also, building applications that combine multiple contracts can be confusing to developers. For this reason, Plasma Network has considered a superficially concise and easy-to-understand configuration by separating the roles into three modules. The OVM Module implements a function called Universal Adjudication to cause a dispute when the user finds a mistake in the information on Layer1. The Plasma Module supports a common implementation of some of the essential smart contracts for Plasma. Only the implementations that require different logic for each application are managed by the Contracts Module.

These Plasm Network logics can be combined with the implementation provided by the Plasma L2 Implementation described above to build an application.


---
Below are the technical details.


---

# Smart Contract

Smart contracts in Plasm Network's Layer2 applications require **ERC20 Contracts** and **Payout Contracts**. Each Layer2 application developer must implement their own smart contract.

## ERC20 Contract

ERC20 Contract is a contract that expresses tokens handled by Layer2 application. Refer to this specification for [ERC20](https://eips.ethereum.org/EIPS/eip-20). We implement PLM's wrapped Contract as the default ERC20 Contract.

### wPLM  contract

wPLM contract is a wrapped contract of PLM token. This is an ERC20 token issued by depositing the PLM token, the basic token of Plasm Network with the contract. In other words, it has the same value as PLM. This is like [wETH](https://weth.io/jp/).

## Payout Contract

Payout Contract is a contract that expresses the process when returning tokens from Layer2 to Layer1. Layer2 application developers must implement it because user can not withdraw without this contract. We implement **Ownership payout contract** as the default Payout Contract.

The above contract can be implemented without depends on the following ovm modules. Payout Contract must be able to call the finalizeExit method. This is enforced by the trait.

```javascript
function finalizeExit(
    address depositContractAddress,
    types.Property memory _exitProperty,
    uint256 _depositedRangeId,
    address _owner
)
```

### Ownership payout contract

Ownership payout contract is a contract that the token owner can withdraw. Specifically, When the Exit is determined to be true in the Challenge Game, the owner represented by that State Object (in this case, OwnershipPredicate) can withdraw the token. The Ownership Payout contract is expressed in the Ethereum contract like [this](https://github.com/cryptoeconomicslab/ovm-contracts/blob/master/contracts/Predicate/plasma/OwnershipPayout.sol).

# Modules

Operations related to OVM are implemented by the Substrate runtime module. This is so that users do not have to deploy complex smart contracts. This is intended to make gas costs of deployment cheap and easy to estimate. In addition, this makes developers of Layer2 applications can consider and implement only the essentially required "ERC20 contract" and "Payment contract" and properties that indicate the rules of state transition.

Then, it is necessary to consider special storage that can handle the Layer2 application with the Substrate Runtime Module. It treats one application as one AccountId in the same way as a smart contract.

Specifically, it can be divided into OVM Modules, which perform general OVM processing, and Plasma modules, which are responsible for plasma-specific processing. See the architecture diagram for the dependencies of each module and contract.


# OVM Module

OVM Module describes the processing commonly performed in OVM. Specifically, the execution logic of Predicate is included in this module. In addition, the smart contract is executed by using the truth of Predicate as a trigger. This module is a modularized version of [Universal Adjudication contract](https://github.com/cryptoeconomicslab/ovm-contracts/blob/master/contracts/UniversalAdjudicationContract.sol) in the Ethereum Smart contract.


## Types
Defines the type used by OVM Module.
```rust
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

## Universal Adjudication

### Contants
```rust
/// During the dispute period defined here, the user can challenge. If nothing is found, the state is determined after the dispute period.
type DISPUTE_PERIOD: T::Moment = 7;
```
### Storage
```rust
decl_storage! {
	Predicate get(fn predicate): map T::AccountId => T::Predicate;
	DisputePeriod get(fn dispute_period): T::Moment;
	InstantiatedGames get(fn instantiated_games): map T::Hash => T::ChallengeGame;
}
```
### Modules
```rust
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
### Events
```rust
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

# Plasma Module

Plasma Module is a module that is responsible for processing specific to Plasma. It calls the OVM Module and the specified smart contract function. The Plasma Module has one "Commitment" and "Deposit" address per application. These are each defined by `decl_child_storage`. `decl_child_storage!` is a macro that implements DB in SubTrie. This sets AccountId as the key value. This is like a contract address. Specifically, implements with reference to [AccountDb](https://github.com/paritytech/substrate/blob/master/frame/contracts/src/account_db.rs) of contract module.

This is modularized  [Commitment](https://github.com/cryptoeconomicslab/ovm-contracts/blob/master/contracts/CommitmentContract.sol), [Deposit](https://github.com/cryptoeconomicslab/ovm-contracts/blob/master/contracts/DepositContract.sol) and [CompiledPredicate](https://github.com/cryptoeconomicslab/ovm-contracts/blob/master/contracts/Predicate/CompiledPredicate.sol) contracts in the Ethereum.

## Types
Defines the type used by Plasma Module.
```rust
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

### modules
```rust
/// Commitment constructor + Deposit constructor
fn deploy(
	aggregator_address: T::AccountId,
	erc20: T::AccountId,
	state_update_predicate: T::AccountId);
```
## Commitment

Commitment is something to save the Merkle Root owned by the Plasma child chain. Child storage of Commitment is generated for each Layer2 application. This can be used like accessing smart contracts.

### Storage
```rust
// Commitment storage: Plapps address => Commitment Child Storage.
Commitment get(fn commitment): T::AccountId => Commitment;
```

```rust
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
## Modules
```rust
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
## Events
```rust
// Event definitions (AccountID: PlappsAddress, BlockNumber, Hash: root)
BlockSubmitted(AccountId, BlockNumber, Hash);
```
## Deposit


Deposit is something to deposit ERC20 tokens from Layer1 to Layer2. Child storage of Deposit is generated for each Layer2 application. This can be used like accessing smart contracts.

### Storage
```rust
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
### Modules
```rust
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
### Events
```rust
// (checkpointId: Hash, checkpoint: Checkpoint);
CheckpointFinalized(Hash, Checkpoint);
// (exit_id: Hash)
ExitFinalized(Hash);
// (new_range: Range)
DepositedRangeExtended(Range);
// (removed_range: Range)
DepositedRangeRemoved(Range);
```
## Compiled Predicate

The role of CompiledPredicate is optimizing claim size by compiling complex proposition to one simple predicate. The Plasma Module has method for running Layer2 applications via Predicate. PayoutContract withdrawal processing that exists for each Layer2 application can only be called via Compiled Predicate. This makes you can process Layer2 as secure of Layer1.

### Storage
```rust
/// predicate address => payout address
PayoutContractAddress get(fn payout_contract_address): map T::AccountId => T::AccountId;
```
### Modules
```rust
fn decide_true(predicate_address: T::AccountId, inputs: Vec<u8>, witness: Vec<u8>);

/// callable
fn is_valid_challenge(predicate_address: T::AccountId, inputs: Vec<u8>, challenge_inputs: Vec<u8>, challenge: T::Property);
fn decide(predicate_addres: T::AccountId, inputs: Vec<u8>, witness: Vec<u8>);
```