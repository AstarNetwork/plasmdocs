# Gas Price API

## Overview

Gas is the unit of measure for how much computational work is required to process transactions and smart contracts. Essentially a transaction fee, the term originates from Ethereum, in which context it refers to computation undertaken on the Ethereum Virtual Machine (EVM). Since Ethereum was founded, numerous EVM-compatible networks have emerged and adopted similar models.

The term can be considered analogous to the gas that powers a car engine: it's the fluctuating, occasionally expensive cost of operation. More complex smart contracts require more gas to power their computation, just as a bigger, more powerful car takes more gas to run.

Gas price API is a service that allows you to get the various gas prices of the astar network for various transaction times. Gas fee are provided in wei.

## API

API is provided in repo [https://github.com/AstarNetwork/gas-station](https://github.com/AstarNetwork/gas-station). node.js is the requirement to run the API server.

Steps to setup the API server.

Clone the repo.

```
> git clone https://github.com/AstarNetwork/gas-station
```

Install Dependencies.

```
> cd gas-station
> yarn install
```

Start the server.

```
> yarn start
```

Server will start on port 3000 or environment variable PORT if provided.

You can get the gas for different chain with these http APIs.

* **Shibuya**: GET http://localhost:3000/api/shibuya/gasnow
* **Shiden**: GET http://localhost:3000/api/shiden/gasnow
* **Astar**: GET http://localhost:3000/api/astar/gasnow

### Response



```
{
    "code":200,
    "data":{
        "slow":"1746510000",
        "average":"5119200000",
        "fast":"9501250000",
        "timestamp":1653037338668,
        "eip1559":{
            "priorityFeePerGas":{
                "slow":"746510000",
                "average":"4119200000",
                "fast":"8501250000"
            },
            "baseFeePerGas":"1000000000"
        },
        "tip":{
            "slow":"746510000000",
            "average":"4119200000000",
            "fast":"8501250000000"
        }
    }
}
```

### Response parameters



* slow: The gas price for a transaction that takes a long time to execute.
* average: The gas price for a transaction that takes a medium time to execute.
* fast: The gas price for a transaction that takes a short time to execute.
* eip1559:

With EIP1559 transactions gas fee are divided in two parts: base fee and priority fee.

The Base Fee, which is determined by the network itself. And is same for a block. Priority Fee, which is optional, determined by the user, is a tip to validators, and incentivizes them to prioritize your transaction.

EIP-1559's purpose is essentially to make gas fees more transparent and predictable for users. Previously, to have your transaction processed, you essentially had to 'bid' with a high enough total fee to make sure the miner was incentivized to pick up your transaction reasonably soon. This meant the market price was constantly moving according to demand.

* priorityFeePerGas: The variable part of the gas fee. Determined by the user.
* baseFeePerGas: The fixed part of the gas fee. Determined by the network.
*   tip: Tips are an optional transaction fee that users can add. Tips are not part of the inclusion fee and are an incentive to block authors for prioritizing a transaction, and the entire tip goes directly to the block author. Tip is provided in gas API and can be used when sending native transactions. Tip is provided for slow, average and fast speed.

    \
