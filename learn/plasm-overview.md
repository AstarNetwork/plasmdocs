# Visão geral do Plasma  🔮

Iremos percorrer as funções básicas do plasma nesta página. O plasma é uma das soluções de escala de blockchain inventadas por Joseph Poon e Vitalik Buterin.

[White paper](https://plasma.io/plasma.pdf)

O plasma é um framework para fazer uma cadeia lateral e conectá-la a uma cadeia principal \(por exemplo, Ethereum\). A cadeia lateral e a cadeia principal se comunicam.

## **Porque Plasma?**

As blockchains são lentas e caras por definição. As cadeias de blocos não podem ser uma infraestrutura do mundo sem uma alta escalabilidade. Nós, implementadores do plasma, tentamos torná-lo rápido e barato, sem sacrificar a segurança e a descentralização, para que todos possam usar blockchains.  


## **Na Plasm Network**

O plasma é uma das soluções de escala na blockchain. A idéia básica do Plasma é gerenciar e processar transações em uma árvore Merkle fora da cadeia em alta velocidade e gravar apenas a raiz Merkle na blockchain. A pessoa responsável por executar o processamento fora da cadeia e enviar o hash para a blockchain é chamada de Agregador no contexto do Plasma.

![](../.gitbook/assets/sukurnshotto-2020-05-31-183650png.png)

A Plasm Network suporta "Plasma", que é baseado no Plasma-Cash. Seu estado é NFT e ele não é uma transação nas folhas da árvore Merkle. As regras para executar a transição de estado podem ser definidas pelo OVM \(Optimistic Virtual Machine\), conforme descrito posteriormente.

{% page-ref page="optimistic-virtual-machine.md" %}

A figura abaixo mostra um exemplo de uma transição de estado NFT que possui propriedade como um estado e a transação necessária.

![](../.gitbook/assets/sukurnshotto-2020-05-31-183843png.png)

Nesse caso, para fazer uma transição de estado,

1. Deve ser assinado pelo "Proprietário"  
2. Um novo estado deve ser especificado para a saída  
3. Um estado já não deve ter sido transferido de outra maneira, isso é descrito usando o OVM. A lógica descrita aqui é chamada "Predicado". É descrito na lógica de primeira ordem. Quando o OVM recebe a transação aceita, ele altera o estado e atualiza a rota Merkle.

No plasma, um único agregador lida com essas transações e envia a rota Merkle. Se o Agregador trapaceia, a transação enviada pelo usuário pode ser falsificada. O plasma pode contestar a exatidão das transações e estados na cadeia principal usando OVM e Predicado descritos acima para tal violação. Isso permite que o Plasma combine o poder de processamento rápido de transações por um único agregador e a forte segurança da blockchain. 

