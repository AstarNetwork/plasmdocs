# Polkadot 🔴

![](../.gitbook/assets/sukurnshotto-2020-06-07-221155png.png)

O [Polkadot](https://polkadot.network/) é um protocolo fragmentado que permite que as redes blockchain operem juntas de maneira integrada. É um projeto de código aberto liderado pela [Web3 Foundation](https://web3.foundation/).

### Polkadot Basics

![](../.gitbook/assets/sukurnshotto-2020-06-07-230056png.png)

O Polkadot consiste principalmente em duas partes: Relaychain e Prachain.

 **Relaychain:** O coração de Polkadot, responsável pela segurança, consenso e interoperabilidade da cadeia cruzada da rede.

 **Parachain:** Blockchains soberanas que podem ter seus próprios tokens e otimizar sua funcionalidade para casos de uso específicos. Para conectar-se à Relay Chain, os parachains podem pagar conforme o necessário ou alugar um slot para conectividade contínua.

A Plasm Network pretende ser o primeiro contrato inteligente escalável da Polkadot Parachain. \(A Plasm Network pode ser um Parachain, pois é construído no Parity Substrate\)

{% page-ref page="substrate.md" %}

Por meio dessa arquitetura, o Polkadot possibilita o seguinte:

1. **Ao conectar o Parachain ao Relaychain, os dados e token podem ser transferidos entre Parachains sem problemas.**
2. **O Parachain pode importar a segurança do Relaychain.**

Se você está interessado no Polkadot, pode aprender mais nas seguintes páginas da web:

* **Polkadot Lightpaper:** https://polkadot.network/Polkadot-lightpaper.pdf
* **Site Polkadot:** https://polkadot.network/
* **Wiki de Polkadot:** https://wiki.polkadot.network

## **Plasm Network e Polkadot**

Nesta seção, descreveremos os papéis da Plasm Network no ecossistema Polkadot. A Plasm Network pretende ser o primeiro contrato inteligente escalável da Polkadot Parachain.

### **Contrato Inteligene**

O Polkadot Relaychain, por design, não suporta contratos inteligentes. Isso permite que a Plasm tenha a oportunidade de preencher essa lacuna. A escalabilidade é obviamente uma das demandas mais cruciais dos desenvolvedores do DApp. Idealmente, os desenvolvedores podem criar quaisquer aplicativos na Plasm Network sem precisar considerar sua escalabilidade.

### **Escalabilidade**

A Plasm Network é escalável, porque estamos implementando soluções de Layer2, especialmente a Máquina Virtual Otimista.  


{% page-ref page="../learn/optimistic-virtual-machine.md" %}

A escalabilidade é um dos problemas mais cruciais que o blockchain tem. Para tornar a blockchain uma infraestrutura social, ela precisa de alto desempenho de processamento. Resolver esse problema de escalabilidade no ecossistema blockchain é uma tarefa urgente para nós.

Quando dizemos escalabilidade, existem 2 tipos:

1. **Escalabilidade da Layer1 \(horizontal\):** o conceito de escalabilidade da Layer1 é fazer mais no blockchain da Layer1. \(por exemplo, sharding e Segwit\)
2. **Escalabilidade da Layer2 \(vertical\):** o conceito de escalabilidade da Layer2 é fazer menos na Layer1 e fazer mais na Layer2 ou fora da cadeia \(por exemplo, canal de plasma e estado\).

O Polkadot tem a escalabilidade layer1 porque é uma arquitetura de sharding. O Plasm também é escalável porque possui escalabilidade vertical na layer2.

![](../.gitbook/assets/sukurnshotto-2020-06-07-234905png.png)

Plasma, State Channel -&gt; Escalabilidade vertical, mais flexível e menos unidos.  
Sharding -&gt; Escalabilidade horizontal, menos flexível. mais unidos.  
  
As soluções Layer1 e Layer2 são completamente diferentes e se complementam.  
  
Além disso, a escalabilidade não é o único benefício que podemos obter através das soluções da layer2. Também podemos obter os seguintes:

* **Primeira Finalidade**
* **Desenvolvimento flexível de DApps**
* **Custo de transação \(gás\) mais barato**

Por meio de soluções inteligentes de contrato e de layer2, esperamos ver vários casos de uso na Plasm Network \(por exemplo: jogos, IoT, pagamento, DEX e Bridge\).  


![](../.gitbook/assets/sukurnshotto-2020-06-08-00739png.png)

Alguma pergunta? Não hesite em perguntar-nos no [Discord Tech Channel.](https://discord.gg/Z3nC9U4)  


