# Real-Time Lockdrop 🍬

**Declaimer:** Este é um módulo experimental. Alguns recursos não funcionam ou funcionam com problemas. Por favor, reporte problemas no [GitHub](https://github.com/staketechnologies/Plasm/issues/new/choose) quando encontrar.   


## **Instalação Rápida**

1. Instale dependências de acordo com[ README](https://github.com/staketechnologies/Plasm/tree/plasm-real-time-lockdrop#building-from-source).
2. Busque a ramificação de bloqueio personalizada do plasm-node

```text
git clone https://github.com/staketechnologies/Plasm -b plasm-real-time-lockdrop && cd Plasm
```

1. Construa o binário do Plasm..

```text
cargo build --release
```

## **Preparando para testes**

1. Ative seu nó em seu ambiente de desenvolvimento:

```text
./target/release/plasm-node --dev
```

> Previous versions of db should be removed before the launch: `./target/release/plasm-node purge-chain --dev`

1. Abra Plasm Portal "[Settings page](https://apps.plasmnet.io/#/settings)".
2. Escolha `local node` \(Nó local\) na seção do node section\(nó remoto\).
3. Confira a guia "Developer" e coloque os sequintes tipos personalizados.

![](../.gitbook/assets/sukurnshotto-2020-05-31-174451png%20%281%29.png)

```text
{
  "ClaimId": "H256",
  "Lockdrop": {
    "type": "u8",
    "transaction_hash": "H256",
    "public_key": "[u8; 33]",
    "duration": "u64",
    "value": "u128"
  },
  "TickerRate": {
    "authority": "u16",
    "btc": "DollarRate",
    "eth": "DollarRate"
  },
  "DollarRate": "u128",
  "AuthorityId": "AccountId",
  "AuthorityVote": "u32",
  "ClaimVote": {
    "claim_id": "ClaimId",
    "approve": "bool",
    "authority": "u16"
  },
  "Claim": {
    "params": "Lockdrop",
    "approve": "AuthorityVote",
    "decline": "AuthorityVote",
    "amount": "u128",
    "complete": "bool"
  }
}
```

## **Preço Oracle**

Após o lançamento, seu nó de autoridade começa a buscar e enviar o preço atual em dólares do BTC e ETH para sua cadeia. Ao abrir o [explorer](https://apps.plasmnet.io/#/explorer), você pode ver os extrínsecos da taxa do dólar em cada módulo importado. Essa taxa em dólar é usada no Pallet de substrato do Lockdrop para verificar o preço durante os períodos do Lockdrop.

![](../.gitbook/assets/sukurnshotto-2020-05-31-174351png%20%283%29%20%283%29%20%283%29.png)

## **Solicitação de lockdrop**

A equipe da Plasm Network implantou o contrato inteligente da Lockdrop na rede Ethereum Ropsten apenas para fins de teste. Você pode conferir em

{% embed url="https://ropsten.etherscan.io/address/0xeed84a89675342fb04fafe06f7bb176fe35cb168" caption="" %}

Vamos enviar uma transação para o contrato inteligente de bloqueio usando Etherscan e Metamask!

![](../.gitbook/assets/sukurnshotto-2020-05-31-174357png%20%282%29%20%283%29%20%282%29.png)

Depois de bloquear o seu ETH, você pode fazer uma reclamação na sua rede local.  


![](../.gitbook/assets/sukurnshotto-2020-05-31-174402png%20%282%29%20%283%29.png)

Você pode usar os dados de teste abaixo:

```text
0x6c4364b2f5a847ffc69f787a0894191b75aa278a95020f02e4753c76119324e0
0x039360c9cbbede9ee771a55581d4a53cbcc4640953169549993a3b0e6ec7984061
2592000
100000000000000000
```

![](../.gitbook/assets/sukurnshotto-2020-05-31-174408png%20%282%29%20%282%29%20%281%29.png)

E aqui estão os resultados disponíveis na cadeia:

![](../.gitbook/assets/sukurnshotto-2020-05-31-174413png%20%282%29%20%283%29.png)

Alguma pergunta? Não hesite em perguntar-nos no [Discord Tech Channel](https://discord.com/invite/Z3nC9U4).

