# Optimistic Virtual Machine

## Optimistic Virtual Machine（OVM）とは何か？

Plasma を扱う上で私達は OVM という技術を用います。これは、前述した Plasma を記述するために使用するプロトコルです。

{% page-ref page="./" %}

さらに、**OVM は Plasma だけでなくすべてのレイヤー2ソリューションを抽象化したプロトコルです。**レイヤー2ソリューションには前述した State Channel や、Plasmaの無限のスケーラビリティとトレードオフに取引履歴の可用性に関する問題を解決した Optimistic Rollup などがあります。**OVMを用いることでこれらのような Plasma 以外のレイヤー2ソリューションも扱えるようにする発展性を持ち合わせることが出来ます。**

[Plasm Network](https://www.plasmnet.io/) では OVM をスマートコントラクトと切り離してモジュールとして用意することでより簡潔で便利に OVM を利用できるようにします。[Plasm Network ](https://www.plasmnet.io/)内では OVM とその周囲のアーキテクチャは以下のようになっています。

![](../../.gitbook/assets/sukurnshotto-2020-05-29-161123png.png)

専用のクライアントアプリケーションである L1 adapter を介すことで適切に Plasmaアプリケーションを作成、動作させることが出来ます。アプリケーションは [Plasm Network ](https://www.plasmnet.io/)において OVM, Contracts module によって構成されます。Ethereum における Plasma 開発では、これらのモジュールで提供されているものはすべてスマートコントラクトで管理されていました。しかし、その場合だと複雑なロジックを内包しているPlasmaアプリケーションを実行する際のガスコストを予測しづらいという問題が発生します。

また、複数のコントラクトを組み合わせたアプリケーション構築は開発者に度々混乱を招くことが予想されます。そのため、[Plasm Network](https://www.plasmnet.io/) では3つのモジュールに役割を分離することで表面的に簡潔且つわかりやすい構成を考えました。

OVM Module ではユーザが Layer1 に上がっている情報に過ちを見つけた際に紛争を起こすための Universal Adjudication と呼ばれる機能が実装されています。Plasma Module は幾つかの Plasma のために必要不可欠なスマートコントラクトの共通実装をサポートしています。そして、各アプリケーションごとに異なるロジックが必要な実装のみを Contracts Module で管理しています。

このPlasm Networkロジックは、上述したPlasma Layer 2の実装と組み合わせてアプリケーションを構築することができます。 詳細は以下を参照してください。

## スマートコントラクト <a id="smart-contract"></a>

Plasm Networkのレイヤー2アプリケーションにおけるスマートコントラクトには、**ERC20コントラクト**と**ペイアウトコントラクト**が必要です。各レイヤー2アプリケーションの開発者は、独自のスマートコントラクトを実装する必要があります。

### ERC20コントラクト <a id="erc20-contract"></a>

ERC20コントラクトは、レイヤー2アプリケーションで扱うトークンを表現するコントラクトです。ERC20については本仕様書\([ERC20](https://eips.ethereum.org/EIPS/eip-20)\)を参照してください。PLMラッピングされたコントラクトは、デフォルトのERC20コントラクトです。

#### wPLMコントラクト <a id="wplm--contract"></a>

wPLMコントラクトは、PLMトークンのラッピングコントラクトです。Plasm Networkの基本トークンであるPLMトークンをコントラクトに預けることで発行されるERC20トークンです。つまり、 [wETH](https://weth.io/jp/)のようにPLMと同じ価値を持っています。

### ペイアウトコントラクト <a id="payout-contract"></a>

ペイアウトコントラクトとは、レイヤー2からレイヤー1へのトークンの返却を処理するコントラクトです。レイヤー2アプリケーションの開発者は、ユーザがレイヤー1から引き出せるようにするために、このコントラクトを含める必要があります。**Ownership payout contract**はデフォルトのペイアウトコントラクトです。

ペイアウトコントラクトは `finalizeExit` メソッドをcallすることができます。

```text
function finalizeExit(
    address depositContractAddress,
    types.Property memory _exitProperty,
    uint256 _depositedRangeId,
    address _owner
)
```

#### Ownership payout contract <a id="ownership-payout-contract"></a>

Ownership payout contractとは、トークンの所有者が引き出すことができる契約である。具体的には、チャレンジゲームでExitがtrueと判定された場合、そのState Object（この場合はOwnershipPredicate）で表される所有者がトークンを引き出すことができます。Ownership payout contractは、Ethereumのコントラクトでは[このように](https://github.com/cryptoeconomicslab/ovm-contracts/blob/master/contracts/Predicate/plasma/OwnershipPayout.sol)表現されています。

## モジュール <a id="modules"></a>

OVMに関連した操作は、Substrateランタイムモジュールによって実装されています。これは、ユーザーが複雑なスマートコントラクトをデプロイする必要がないようにするためです。これにより、デプロイ時のガスコストを安くし、また見積もることが容易になります。さらに、これにより、レイヤー2アプリケーションの開発者は、必要な「ERC20コントラクト」と「ペイアウトコントラクト」とプロパティのみを実装するだけで済むようになっています。

レイヤー2アプリケーションを扱うことができる特別なストレージは、Substrateランタイムモジュールで検討する必要があります。スマートコントラクトと同じように1つのアプリケーションを1つのAccountIdとして扱います。

一般的なOVM処理を行うOVMモジュールと、Plasma固有の処理を担当するPlasmaモジュールに分けることができます。各モジュールとコントラクトの依存関係については、アーキテクチャ図を参照してください。

## OVMモジュール <a id="ovm-module"></a>

OVMモジュールは、OVMで一般的に行われる処理を記述しています。具体的には、predicateの実行ロジックがこのモジュールに含まれます。また、predicateの真偽をトリガーとしてスマートコントラクトを実行します。このモジュールは、Ethereumスマートコントラクトの中の[Universal Adjudication contract](https://github.com/cryptoeconomicslab/ovm-contracts/blob/master/contracts/UniversalAdjudicationContract.sol) をモジュール化したものです。

### Types <a id="types"></a>

OVM モジュールで使用されるタイプを定義します。

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

Plasma Moduleは、Plasma特有の処理を担当するモジュールです。OVMモジュールと指定されたスマートコントラクト関数を呼び出します。Plasmaモジュールは、アプリケーションごとに1つの "Commitment "と "Deposit "アドレスを持っています。これらはそれぞれ `decl_child_storage` で定義されています。 `decl_child_storage!` は SubTrie の DB を実装したマクロです。これはAccountIdをキー値として設定しています。これはコントラクトモジュールのAccountDbを参照して実装するコントラクトアドレスのようなものです。 これはEthereumの [Commitment](https://github.com/cryptoeconomicslab/ovm-contracts/blob/master/contracts/CommitmentContract.sol), [Deposit](https://github.com/cryptoeconomicslab/ovm-contracts/blob/master/contracts/DepositContract.sol) そして [CompiledPredicate](https://github.com/cryptoeconomicslab/ovm-contracts/blob/master/contracts/Predicate/CompiledPredicate.sol) のコントラクトをモジュール化したものです。

### Types <a id="types"></a>

Plasma モジュールで使用されるタイプを定義します。

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

コミットメントは、Plasmaの子チェーンが所有するMerkle Rootを保存するためのものです。コミットメントの子ストレージはレイヤー2アプリケーションごとに生成されます。これはスマートコントラクトにアクセスするために使用することができます。

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

Deposit は、ERC20 トークンをレイヤー1 からレイヤー2 にデポジットすることができます。Depositの子ストレージはレイヤー2のアプリケーションごとに生成されます。これはスマートコントラクトにアクセスするような使い方ができます。

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

`CompiledPredicate`の役割は、複雑な命題を1つの単純な述語にコンパイルすることで、クレームサイズを最適化することです。Plasmaモジュールには、Predicateを介してレイヤー2アプリケーションを実行するためのメソッドがあります。各レイヤー2アプリケーションに存在する`PayoutContract`の出金処理は、Compiled Predicateを介してのみ呼び出すことができます。これにより、レイヤー2上のトランザクションをレイヤー1と同じように安全に実行することができます。

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

質問があれば、[Tech Chat](https://discord.gg/Cyjnrxv)の日本語チャネルでご質問ください。

