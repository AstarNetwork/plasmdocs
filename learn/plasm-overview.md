# Panoramica su Plasma

Plasma è una soluzione per la scalabilità della blockchain inventata da Joseph Poon e Vitalik Buterin.

[White paper](https://plasma.io/plasma.pdf)

Plasma è un framework per creare una side chain e collegarla alla catena principale \(ad es. Ethereum\). La side chain e la catena principale comunicano tra di loro.

## Perché Plasma?

Le blockchains sono lente e costose da progetto. Le blockchains non possono essere un'infrastruttura mondiale senza un'elevata scalabilità. Plasma intende rendere le blockchains veloci ed economiche senza sacrificare la sicurezza e la decentralizzazione.

## In Plasm Network

Plasma è una famosa soluzione per la scalabilità della blockchain. Plasma gestisce ed elabora le transazioni in un Merkle tree \(albero\) all'esterno della catena ad alta velocità, ed incide solamente la Merkle root \(radice\) sulla blockchain. L'attore responsabile dell'esecuzione per l'elaborazione off-chain e per l'invio dell'hash alla blockchain è chiamato Aggregator in Plasma.

![](../.gitbook/assets/sukurnshotto-2020-05-31-183650png.png)

Plasm Network supporta "Plasma" il quale è basato su Plasma-Cash. Ha uno stato NFT, non una transazione, alle foglie del Merkle tree. Le regole per eseguire la transizione di stato possono essere definite da Optimistic Virtual Machine \(OVM\) e sono descritte in seguito.

{% page-ref page="optimistic-virtual-machine.md" %}

Di seguito viene mostrato un esempio di transizione di stato NFT che ha la proprietà e la transazione come stato.

![](../.gitbook/assets/sukurnshotto-2020-05-31-183843png.png)

Workflow della transizione di stato:

1. Il proprietario firma la transazione
2. Un nuovo stato deve essere specificato per l'output   
3. Uno stato non deve essere già stato trasferito in un altro modo, questo è descitto utilizzando OVM. La logica qui descritta si chiama "Predicate" \(o "Predicato"\). È descritto nella logica di primo ordine. Quando OVM riceve la transazione accettata, cambio lo stato ed aggiorna il Merkle route \(percorso\).

In Plasma, un singolo Aggregator gestisce le transazioni ed invia il Merkle route. Se l'Aggregator imbroglia, la transazione inviata dall'utente può essere falsificata. Plasma può contestare la correttezza delle transazioni e degli stati sulla catena principale utilizzando OVM e Predicate, sopra descritti. Ciò consente a Plasma di combinare sia la potenza di elaborazione rapida delle transazioni di un singolo Aggregator, sia la forte sicurezza della blockchain.

