# Consensus 🎬

A Plasm Network altera algoritmos de consenso e recompensa projetos passo a passo para manter a segurança. Especificamente, ele inicialmente assume a forma de uma Prova de Autoridade, que é executada exclusivamente por Validadores selecionados pela comunidade.

Em seguida, mudaremos para recompensas centradas no [collator](https://wiki.polkadot.network/docs/en/maintain-collator) para participar como Parachain. Eventualmente, mudaremos para o NPoS, que também é usado pelo Relaychain da Polkadot. Consulte o capítulo do Ecossistema de Tokens PLM para obter detalhes sobre como distribuir recompensas.

{% page-ref page="token-economy.md" %}

## **Prova de autoridade**

A Prova de Autoridade é um algoritmo de construção de consenso que opera apenas com um validador selecionado pela comunidade. Bloqueios públicos podem ser vulneráveis quando poucos estão lançando validadores confiáveis. Por esse motivo, o PoA será operado até que exista uma distribuição suficiente de titulares de token e a existência de validadores em potencial que possam ser confirmadas. O validador no momento será pago de acordo com os parâmetros especificados, como no caso de PoS.

## **Nomeada Prova de Staking** 

A Plasm Network usa NPoS, que é usado na cadeia de retransmissão Polkadot. Este algoritmo de consenso consiste em 3 etapas.

1. Um nomeador seleciona um validador[ NPoS](https://research.web3.foundation/en/latest/polkadot/NPoS/)
2. Um validador verifica transações e cria um novo bloco[ BABE](https://research.web3.foundation/en/latest/polkadot/BABE/Babe/)
3. Finalize o bloco que foi entregue na rede[ GRANDPA](https://research.web3.foundation/en/latest/polkadot/GRANDPA/)

A recompensa do bloco é distribuída ao validador que criou o bloco e ao seu Nominador. Além disso, a recompensa também é paga aos colaboradores da Plasm Network 

