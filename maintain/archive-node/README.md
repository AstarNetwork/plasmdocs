# Archive Node

## Overview <a href="#introduction" id="introduction"></a>

An **archive node** keeps all the past blocks. It plays a vital role on a blockchain: it connects users and dApps to the blockchain through WS and RPC endpoints. The public endpoints you can see in [network details](../../integration/network-details.md) are running archive nodes.

**Dapp projects** need to run their own archive node to retrieve blockchain data they use in order not to rely on public infrastructure that will respond slower because of the large amount of users connected.

_Note: be careful of the confusion with a **full node** that has a prunned database: a full node only keeps the past 256 blocks and uses much less storage space._

We are manitaining 3 different networks: the testnet Shibuya, Shiden as a parachain of Kusama, and Astar as a parachain of Polkadot.

| Astar chain |       Relay Chain       |   Name  | Token |
| :---------: | :---------------------: | :-----: | :---: |
|   Testnet   | Osaka (hosted by Astar) | Shibuya |  $SBY |
|    Shiden   |          Kusama         |  Shiden |  $SDN |
|    Astar    |         Polkadot        |  Astar  | $ASTR |

## Requirements

Requirements for running any node are similar to what we recommend to our collators. Depending on the amount and frequency of data requested by a dApp, it may require a larger server. Read more about this [here](../collator/learn-about-collators.md).

{% hint style="info" %}
Running a node for our testnet 'Shibuya' requires less. It's a perfect place to test your node infrastructure and costs.
{% endhint %}

The Astar node runs in **parachain configuration**: they will listen at different ports by default for both the parachain and the embeeded relay chain.

|       Protocol       | Parachain port | Relay Chain port | Custom port command |
| :------------------: | :------------: | :--------------: | :-----------------: |
|          P2P         |      30333     |       30334      |       `--port`      |
|          WS          |      9944      |       9945       |     `--rpc-port`    |
|          RPC         |      9933      |       9934       |     `--rpc-port`    |
| Prometheus (metrics) |      9615      |       9616       | `--prometheus-port` |

You can change these ports using the corresponding custom command.

## Installation <a href="#installation" id="installation"></a>

There are 2 different ways to run an Astar node:

* [Using Binary](binary.md) - run the node from binary file and set it up as _systemd_ service
* [Using Docker](docker.md) - run the node within a Docker container

{% content-ref url="binary.md" %}
[binary.md](binary.md)
{% endcontent-ref %}

{% content-ref url="docker.md" %}
[docker.md](docker.md)
{% endcontent-ref %}

