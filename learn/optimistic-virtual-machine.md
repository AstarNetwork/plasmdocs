---
description: Plasma and beyond.
---

# Optimistic Virtual Machine 🌔

### **O que é Optimistic Virtual Machine \(Máquina virtual otimista\)?**

Simplificando, o OVM \(Optimistic Virtual Machine\) é a máquina virtual projetada para suportar todos os protocolos layer2 inventados pelo Ethereum Foundation Plasma Group. É uma possível unificação de todas as construções de escalabilidade da Layer2. Isso significa que o Plasm Network não será apenas para aplicativos Plasma, mas também para aplicativos Lightning Network ou quaisquer outros protocolos da Layer2.  


A Plasm Network deve ser uma plataforma que abriga todas as soluções de dimensionamento da Layer2. Os usuários podem escolher qual solução usar e possibilitar seu caso de uso com custos indiretos mínimos.

### **Saiba mais**

OVM é um conceito poderoso para desenvolver aplicativos da Layer2. Podemos expressar lógicas de disputa complexas por uma linguagem OVM simples e essa linguagem contém a Optimistic Game Semantics \(OGS\).

Por exemplo, podemos expressar o ponto de verificação do plasma e sair das declarações com duas definições simples \(chamamos de "propriedade"\) pelo OGS. A Plasm Network separa a OVM do contrato inteligente e a prepara como um módulo para que a OVM possa ser usada de maneira mais simples e conveniente.

### OVM in Plasm Network <a id="ovm-in-plasm-network"></a>

A OVM e sua arquitetura circundante são mostradas na figura abaixo.  


![ovmodule](https://user-images.githubusercontent.com/6259384/75546609-404d5880-5a6c-11ea-84d0-f063e0bc252c.png)

Os aplicativos de plasma \(Plapps\) podem ser criados e executados corretamente por meio do adaptador L1. Os Plapps são compostos pelos módulos OVM, Plasma e Contracts na Plasm Network.

No caso de aplicativos Ethereum Plasma, tudo o que é fornecido nesses módulos foi gerenciado por contratos inteligentes. No entanto, nesse caso, há um problema que é difícil prever: o custo do gás ao executar um aplicativo de plasma contendo lógica complicada. Além disso, a criação de aplicativos que combina vários contratos pode ser confusa para os desenvolvedores.

Por esse motivo, a Plasma Network considerou uma configuração superficialmente concisa e fácil de entender, separando as funções em três módulos. O Módulo OVM implementa uma função chamada Universal Adjudication para causar uma disputa quando o usuário encontra um erro nas informações da layer1. O Módulo Plasma suporta uma implementação comum de alguns dos contratos inteligentes essenciais para o Plasma. Somente as implementações que exigem lógica diferente para cada aplicativo são gerenciadas pelo Módulo de contratos.

Essas lógicas da Plasm Network podem ser combinadas com a implementação fornecida pela implementação do Plasma L2 \(layer2\) descrita acima para criar um aplicativo.

Você pode ver os detalhes abaixo.

## **Contrato Inteligente** <a id="smart-contract"></a>

Os contratos inteligentes nos aplicativos da Layer2 da Plasma Networks exigem contratos ERC20 e contratos de pagamento. Cada desenvolvedor de aplicativos da Layer2 deve implementar seu próprio contrato inteligente.

### **Contrato ERC20**  <a id="erc20-contract"></a>

Contrato ERC20 é um contrato que expressa tokens manipulados pelo aplicativo da Layer2. Consulte esta especificação para o [ERC20](https://eips.ethereum.org/EIPS/eip-20). Implementamos o Contrato embrulhado do PLM como o Contrato ERC20 padrão.

#### **Contrato wPLM**  <a id="wplm--contract"></a>

O contrato wPLM é um contrato agrupado do token PLM. Este é um token ERC20 emitido ao depositar o token PLM, o token básico da Plasm Network no contrato. Em outras palavras, ele tem o mesmo valor que o PLM. Isto é como [wETH](https://weth.io/jp/).

### **Contrato de Pagamento** <a id="payout-contract"></a>

Contrato de pagamento é um contrato que expressa o processo ao retornar tokens da Layer2 para a Layer1. Os desenvolvedores de aplicativos da layer2 devem implementá-lo porque o usuário não pode retirar-se sem este contrato. Implementamos o contrato de pagamento de propriedade como o contrato de pagamento padrão.

O contrato acima pode ser implementado sem depender dos seguintes módulos ovm. O contrato de pagamento deve poder chamar o método finalizeExit. Isso é imposto pela característica.

```text
function finalizeExit(
    address depositContractAddress,
    types.Property memory _exitProperty,
    uint256 _depositedRangeId,
    address _owner
)
```

#### **Contrato de pagamento de propriedade** <a id="ownership-payout-contract"></a>

Contrato de pagamento de propriedade é um contrato que o proprietário do token pode retirar. Especificamente, quando a saída é determinada como verdadeira, o proprietário representado por esse objeto de estado \(nesse caso, OwnershipPredicate\) pode retirar o token. O contrato de pagamento de propriedade é expresso no contrato Ethereum assim.

## **Módulos** <a id="modules"></a>

As operações relacionadas ao OVM são implementadas pelo módulo de tempo de execução do Substrate. Isso é para que os usuários não precisem implantar contratos inteligentes complexos. O objetivo é tornar os custos de implantação de gás baratos e fáceis de estimar. Além disso, isso faz com que os desenvolvedores de aplicativos da Layer2 possam considerar e implementar apenas o "contrato ERC20" e o "Contrato de pagamento" e as propriedades que indicam as regras da transição do estado.

Em seguida, é necessário considerar o armazenamento especial que pode lidar com o aplicativo da Layer2 com o Substrate Runtime Module. Ele trata um aplicativo como um AccountId da mesma maneira que um contrato inteligente.

Especificamente, ele pode ser dividido em Módulos OVM, que executam o processamento geral da OVM, e módulos Plasma, responsáveis pelo processamento específico do plasma. Veja o diagrama da arquitetura para as dependências de cada módulo e contrato.

## **Modulo OVM** <a id="ovm-module"></a>

OVM Module descreve o processamento normalmente executado na OVM. Especificamente, a lógica de execução do Predicate está incluída neste módulo. Além disso, o contrato inteligente é executado usando a verdade do Predicate como gatilho. Este módulo é uma versão modularizada do contrato [Universal Adjudication](https://github.com/cryptoeconomicslab/ovm-contracts/blob/master/contracts/UniversalAdjudicationContract.sol) no contrato inteligente do Ethereum.

### Types <a id="types"></a>

Define o tipo usado pelo módulo OVM.

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

## **Módulo de Plasma** <a id="plasma-module"></a>

Módulo de plasma é o módulo responsável pelo processamento específico do plasma. Ele chama o Módulo OVM e a função de contrato inteligente especificada. O módulo de plasma possui um endereço "Compromisso" e "Depósito" por aplicativo. Estes são definidos por `decl_child_storage`. `decl_child_storage!` é uma macro que implementa o DB no SubTrie. Isso define AccountId como o valor da chave. É como um endereço de contrato. 

Especificamente, implementa com referência ao AccountDb do módulo de contrato.

Trata-se de contratos modularizados de Compromisso, Depósito e Compilado no Ethereum.

### **Tipos** <a id="types"></a>

Define o tipo usado pelo módulo de plasma

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

#### **modulos** <a id="modules"></a>

```text
/// Commitment constructor + Deposit constructor
fn deploy(
    aggregator_address: T::AccountId,
    erc20: T::AccountId,
    state_update_predicate: T::AccountId);
```

### **Commitment** <a id="commitment"></a>

Commitment é algo para salvar a Raiz de Merkle, pertencente à cadeia de filhos de Plasma. O armazenamento filho de Commitment é gerado para cada aplicativo da Layer2. Isso pode ser usado como acessar contratos inteligentes.

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

Deposit é algo para depositar tokens ERC20 da Layer1 para a Layer2. O armazenamento filho de Deposit é gerado para cada aplicativo da Layer2. Isso pode ser usado como acessar contratos inteligentes.

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

### **Compiled Predicate** <a id="compiled-predicate"></a>

O papel do `CompiledPredicate` é otimizar o tamanho da declaração, compilando proposições complexas para um predicado simples. O Módulo Plasma possui um método para executar aplicativos da Layer 2 via Predicate. O processamento de retirada do `PayoutContract` que existe para cada aplicativo da Layer 2 só pode ser chamado via Compiled Predicate. Isso permite que a Layer 2 das transações seja tão segura quanto a Layer1.

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

Alguma pergunta? Não hesite em perguntar-nos no [Discord Tech Channel.](https://discord.gg/Z3nC9U4)

