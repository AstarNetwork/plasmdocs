# Polkadot

![](../.gitbook/assets/sukurnshotto-2020-06-07-221155png.png)

[Polkadot](https://polkadot.network/) è un progetto open source gestito da [Web3 Foundation](https://web3.foundation/). È un protocollo frammentato che collega diverse reti blockchain.

### Nozioni di base di Polkadot

![](../.gitbook/assets/sukurnshotto-2020-06-07-230056png.png)

Polkadot è composta da due parti: Relaychain e Parachain.

* **Relaychain:** Questo è il nucleo di Polkadot responsabile della sicurezza delle rete, del consenso e dell'interoperabilità cross-chain \(tra le blockchain\).
* **Parachain:** Queste sono blockchain sovrane con token personalizzati e funzionalità ottimizzata per casi d'uso specifici. La connessione di una Parachain alla Relaychain ha un prezzo basato sul principio pay-as-you-go \(paga mentre vai\), o su di un contratto di locazione a connettività continua.

[**Plasm Network**](https://www.plasmnet.io/) è costruita su Parity Substrate, rendendola una delle prime Polkadot Parachains per smart contract scalabili.

{% page-ref page="substrate.md" %}

Parachain e Relaychain in Polkadot rendono le seguenti cose possibili:

1. **Dati e tokens possono essere trasferiti tra le parachain senza soluzione di continuità;**
2. **Parachains possono importare la sicurezza della Relaychain.**

Ulteriori informazioni su Polkadot:

* **Polkadot Lightpaper:** [https://polkadot.network/Polkadot-lightpaper.pdf](https://polkadot.network/Polkadot-lightpaper.pdf)
* **Pagina web di Polkadot:** [https://polkadot.network/](https://polkadot.network/)
* **Polkadot wiki:** [https://wiki.polkadot.network/](https://wiki.polkadot.network/)

## Plasm Network e Polkadot

Questa sezione descrive come [Plasm Network](https://www.plasmnet.io/) si integra con l'ecosistema Polkadot. [Plasm Network](https://www.plasmnet.io/) vuole diventare la prima Polkadot Parachain per smart contract scalabili.

### Smart Contract

La Relaychain di [Polkadot](https://polkadot.network/) non supporta gli smart contracts. Plasm implementerà questa funzionalità rendendola anche facilmente scalabile. Gli sviluppatori sono liberi di creare una varietà di DApps sapendo che possono scalare facilmente.

### Scalabilità

La scalabilità di [Plasm Network](https://www.plasmnet.io/) si basa su soluzioni di livello 2 \(layer 2\), come Optimistic Virtual Machine.

{% page-ref page="../learn/optimistic-virtual-machine.md" %}

La scalabilità è la più grande sfida di tutte le blockchain. Per diffondere l'adozione della tecnologia blockchain, sono necessarie prestazioni più elevate. La scalabilità è un problema critico che Plasm Network cerca di ottimizzare.

Esistono due tipi di scalabilità:

* **Livello 1 \(layer 1\) - scalabilità orrizzontale:** più efficace sulla blockchain di livello 1 \(per esempio: sharding e Segwit\);
* **Livello 2 \(layer 2\) - scalabilità verticale:** meno efficace sulla blockchain di livello 1, ma più efficace sulla blockchain di livello 2 o off-chain \(per esempio: Plasma e State Channel\).

Polkadot utilizza la tecnologia sharding che consente una maggiore scalabilà. [Plasm](https://www.plasmnet.io/) incorpora funzionalità verticali di livello 2 \(layer 2\).

![](../.gitbook/assets/sukurnshotto-2020-06-07-234905png.png)

Il livello 1 \(layer 1\) ed il livello 2 \(layer 2\) offrono soluzioni diverse ma complementari.

Ulteriori vantaggi dell'architettura di Plasm Network sono:

* **First Finality;**
* **Sviluppo flessibile di DApps;**
* **Costi di transazione \(gas\) significativamente più bassi.**

La capacità di supportare smart contract, combinata con l'architettura di livello 2, rende possibili molte DApps interessanti su [Plasm Network](https://www.plasmnet.io/) \(per esempio Gaming, IoT, Payment, DEX, e Bridge\).

![](../.gitbook/assets/sukurnshotto-2020-06-08-00739png.png)

Domande? Partecipa alle discussioni su [Discord Tech Channel](https://discord.gg/Z3nC9U4), dove i membri del team e della community sapranno aiutarti a trovare le risposte che cerchi.

