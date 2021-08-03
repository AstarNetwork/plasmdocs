# API

## Overview

The API provides application developers the ability to query a node and interact with the Polkadot or Substrate chains using Javascript. Here you will find documentation and examples to get you started.

A complete overview on using the API in your projects, from installation all the way through to making it do magic. Have things working and want tips? Have a look at the complete library: [https://polkadot.js.org/docs/](https://polkadot.js.org/docs/)

Separated from the API you will also find the [Substrate metadata](https://polkadot.js.org/docs/substrate) section in the documentation that has an overview of the RPC, extrinsics, events, and errors available on a typical Substrate node.

There are a number of organisations that maintain free RPC WebSocket endpoints for the Astar community.

Shiden:

* Stake Technologies: `wss://rpc.shiden.plasmnet.io`
* OnFinality: `wss://shiden.api.onfinality.io/public-ws`

Plasm:

* Stake Technologies: `wss://rpc.plasmnet.io/`
* Patract Elara: `wss://plasm.elara.patract.io`

Dusty:

* Stake Technologies: `wss://rpc.dusty.plasmnet.io/`

## Installation

Follow these steps to use Polkadot API on Plasm Network. Yes, it really is as simple as installing from npm, so we are not going to waste too much time with the bare basics, just install the necessary APIs via:

```text
npm i @polkadot/api
npm i @plasm/types
```

## Example

This example shows how to subscribe to new blocks. It will listen to our testnet server Dusty. It displays the block number every time a new block is seen by the node you are connected to.

NOTE: The example runs until you stop it with CTRL+C

```text
const { ApiPromise, WsProvider, Keyring } = require('@polkadot/api');
const plasmDefinitions = require('@plasm/types/interfaces/definitions');

async function main() {
  const types = Object.values(plasmDefinitions).reduce((res, { types }) => ({ ...res, ...types }), {
    SmartContract: {
      _enum: {
        Wasm: 'AccountId',
        Evm: 'H160'
      }
    },    
  });

  // Other public RPC endpoints listed above
  const wsProvider = new WsProvider('wss://rpc.dusty.plasmnet.io');

  const api = await ApiPromise.create({
    provider: wsProvider,
    types: {
        ...types,
        // aliases that don't do well as part of interfaces
        'voting::VoteType': 'VoteType',
        'voting::TallyType': 'TallyType',
        // chain-specific overrides
        Address: 'GenericAddress',
        Keys: 'SessionKeys4',
        StakingLedger: 'StakingLedgerTo223',
        Votes: 'VotesTo230',
        ReferendumInfo: 'ReferendumInfoTo239',
    },
    // override duplicate type name
    typesAlias: { voting: { Tally: 'VotingTally' } },
  });

    const [chain, nodeName, nodeVersion] = await Promise.all([
    api.rpc.system.chain(),
    api.rpc.system.name(),
    api.rpc.system.version()
  ]);
  console.log(`You are connected to chain ${chain} using ${nodeName} v${nodeVersion}`);

  api.rpc.chain.subscribeNewHeads(async (header) => {
    console.log(`Chain is at #${header.number}`);
  });
}
main().catch(console.error);
```

When you run this script you will see the following:

![](../.gitbook/assets/image%20%2812%29.png)

## Support

Please join our developer's hub on [Discord](https://discord.com/invite/wUcQt3R).

