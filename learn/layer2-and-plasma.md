# Layer2 e Plasma

## Informazioni sulla scalabilità

Al momento in cui scrivo, la seconda più grande blockchain che funge da piattaforma per DApps è [Ethereum](https://www.ethereum.org/), che può elaborare circa 15 transazioni al secondo \(rif:[Ethereum Transaction Throughput](https://www.coindesk.com/information/will-ethereum-scale)\). VISA o Alipay possono processare circa 1,700 transazioni al secondo \(rif:[Visa Transaction Throughput](https://hackernoon.com/the-blockchain-scalability-problem-the-race-for-visa-like-transaction-speed-5cce48f9d44)\) e 256,000 transazioni al secondo rispettivamente \(rif:[ALIPAY Transaction Throughput](https://www.barrons.com/articles/alibaba-records-25-3-billion-in-singles-day-sales-1510538618)\). La velocità di transazione per le DApp è lenta e proibitiva per portare nuovi utenti in questa tecnologia. Per risolvere questo problema, sono state proposte diverse soluzioni di scalabilità per la blockchain.

## Soluzioni per la scalabilità della blockchain

Queste sono alcune tra le più note soluzioni per la scalabilità della blockchain:

1. [**SegWit**](https://github.com/bitcoin/bips/blob/master/bip-0141.mediawiki): Correzzione della malleabilità delle transazioni rimuovendo le informazioni sulla firma e memorizzandole al di fuori del blocco di base della transazione;
2. [**State Channel**](https://l4.ventures/papers/statechannels.pdf): Esecuzione delle transazioni in modalità off-chain tra utenti particolari, fornendo alla blockchain principale solo lo stato finale;
3. [**Sharding**](https://www.bubifans.com/ueditor/php/upload/file/20181015/1539597837236127.pdf): Consentire a più transazioni di essere elaborate contemporaneamente in parallelo suddividendole in frammenti \(shards\);
4. [**Plasma**](https://plasma.io/plasma.pdf): Memorizzare le transazioni in catene secondarie \(child chains\), e solamente l'hash root viene memorizzato all'interno della catena principale.

Le soluzioni per la scalabilità possono essere classificate come livello 1 \(layer 1\) o livello 2 \(layer 2\).

Le soluzioni di livello 1 esistono solamente sul livello 1 della mainnet di Ethereum. Le soluzioni di livello 2 possono combinare assieme le soluzioni di livello 1, livello 2 ed off-chain per prestazioni e scalabilità maggiori.

L'elaborazione delle transazioni deve essere fatta al di fuori della catena principale di livello 1, poichè sta raggiungendo limiti di prestazioni critici \(rif:["The Ethereum-blockchain size has exceeded 1TB, and yes, it’s an issue"](https://hackernoon.com/the-ethereum-blockchain-size-has-exceeded-1tb-and-yes-its-an-issue-2b650b5f4f62)\).

Infine, **il modello di blockchain potrebbe evolversi, dove il livello 1 viene utilizzato come livello di fiducia, e il livello 2 come livello di transazione**.

Plasma è una soluzione per la scalabilità di livello 2 che è la **meno** dipendente dalle prestazioni di elaborazione della catena principale. Plasma è una side-chain gestita da un operatore decentralizzato. **Le transazioni possono essere gestite in modo centralizzato, il quale non richiede consenso, ma i partecipanti alla side-chain possono uscirne in sicurezza solamente presentando le opportune prove della loro legittimità**. Le soluzioni per la scalabilità utilizzate in un esistente sistema centralizzato, possono essere utilizzate così come sono.

Plasma potrebbe diventare una tecnologia indispensabile in futuro, migliorando notevolmente le prestazioni di elaborazione per tutti i registri distribuiti \(distributed ledgers\).

