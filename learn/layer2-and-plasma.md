# Layer2 e Plasma ⚡

## A **necessidade de escalabilidade**

No momento da redação deste artigo, a segunda maior blockchain que atua como plataforma Dapp é o [Ethereum](https://www.ethereum.org/), que pode processar cerca de 15 transações por segundo \(ref: [Ethereum Transaction Throughput](https://www.coindesk.com/information/will-ethereum-scale)\). Em contraste, VISA ou Alipay podem processar cerca de 1.700 transações \(ref: [Taxa de transferência de transações Visa](https://hackernoon.com/the-blockchain-scalability-problem-the-race-for-visa-like-transaction-speed-5cce48f9d44)\) e 256.000 transações, respectivamente \(ref: [Taxa de transferência de transação ALIPAY](https://www.barrons.com/articles/alibaba-records-25-3-billion-in-singles-day-sales-1510538618)\). É verdade que a velocidade de transação do Dapps é muito lenta para os usuários utilizarem essa tecnologia em todo o seu potencial. Para resolver esse problema, várias soluções de escalabilidade de blockchain estão sendo propostas.  


## **Algumas soluções de dimensionamento de blockchain**

Estas são algumas das soluções conhecidas de escalabilidade de blockchain.

* [**SegWit**](https://github.com/bitcoin/bips/blob/master/bip-0141.mediawiki)**:** corrigindo a maleabilidade da transação, removendo as informações de assinatura e armazenando-as fora do bloco de transações base.
* \*\*\*\*[**State Channel**](https://l4.ventures/papers/statechannels.pdf)**:** combina transações fora da cadeia entre usuários específicos e apenas o estado final é comprometido com a blockchain principal.
* \*\*\*\*[**Sharding**](https://www.bubifans.com/ueditor/php/upload/file/20181015/1539597837236127.pdf)**:** permite que mais transações sejam processadas em paralelo ao mesmo tempo, criando shards.
* \*\*\*\*[**Plasma**](https://plasma.io/plasma.pdf)**:** armazena transações em cadeias menores separadas e apenas o hash raiz é armazenado na cadeia principal.

Em termos gerais, temos dois tipos de soluções de dimensionamento: soluções da Layer1 e soluções da Layer2.

As soluções da Layer1 tentam fazer mais do que os desenvolvedores podem fazer na  Layer1. Por outro lado, as soluções da Layer2 tentam fazer menos na Layer1 e mais na Layer2 ou fora da cadeia.

Queremos focar no processamento de transações fora da cadeia principal, denominada solução da Layer2. A Layer1 refere-se a blockchains públicas como Ethereum ou Bitcoin. Nos últimos anos, essa camada está sofrendo com o aumento da capacidade de transação, deixando a blockchain "cheia” \(ref: "[O tamanho do Ethereum blockchain excedeu 1 TB e, sim, é um problema](https://hackernoon.com/the-ethereum-blockchain-size-has-exceeded-1tb-and-yes-its-an-issue-2b650b5f4f62)"\).

A partir disso, podemos prever que em cerca de uma década, a blockchain terá um uso diferente, onde a Layer1  é usada como camada de confiança, enquanto a Layer2  é a camada de transação.

Entre todas as soluções da layer2, a razão pela qual nos concentramos no Plasma é que é uma solução de dimensionamento menos dependente do desempenho do processamento da cadeia principal. No plasma, um operador gerencia sua cadeia lateral sem sacrificar a descentralização. Isso significa que muitas transações podem ser tratadas de maneira centralizada, que não requerem um processo de consenso, mas todos os participantes da cadeia lateral podem sair com segurança enviando provas de fraude. As soluções de dimensionamento usadas no sistema centralizado existente podem ser usadas como estão. Portanto, é possível obter alto desempenho de processamento que não é viável com um razão distribuída nativa.

O plasma deve ser reconhecido como uma tecnologia indispensável no futuro, pois pode melhorar drasticamente o desempenho do processamento de todos os livros distribuídos.

