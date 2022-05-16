---
description: Using XC20 Tokens with Metamask
---

# Metamask and XC20 Tokens

Using XCM within the EVM environment is also simple as our network uses the XC20 interface, which maps the Assets pallet to an ERC20-compatible interface that EVM dApps can use.

First, let’s approach this at a high level, and then move on to a more technical example for dApps. Let’s say I want to move the KSM token from Kusama to `0xd2C6929A72e466213D1c2Df8359194784650A50e`. From the Kusama side of things, the payload for sending the KSM tokens will be similar to the ones we used in the previous section. However, the `Beneficiary` address (account ID) will be a mapped SS58 address of the recipient’s EVM address as that is the only address format that XCM can accept. You can read [this article](https://medium.com/astar-network/using-astar-network-account-between-substrate-and-evm-656643df22a0) on how to create the mapped address. To keep things short, address mappings are:

* **H160:** `0x107bAe763DC63e0686C574FdE1B58115c7d19280`
* **SS58:** `Zag6jpFEU93xsEfczHbJucBUJAHMZFVsk4b3amvV5oXbJoo` (with prefix 5 for Shiden/Astar)
* **public key:** `0xa1363005871407f62f4b7e5752a7bc2934447699c08f4caf1b8c393287c0f502`

So our payload for `reserve_transfer_asset` will look something like this:

```
    // the target parachain connected to the current relaychain
    const dest = {
        V1: {
            interior: {
                X1: {
                    Parachain: 2007,
                },
            },
            parents: 0,
        },
    };
    // the account ID within the destination parachain
    const beneficiary = {
        V1: {
            interior: {
                X1: {
                    AccountId32: {
                        network: 'Any',
                        id: '0x6c65500b73e2cec702f06dcd5299b31e4d0b6cf7728937b7d5edac79611292f2',
                    },
                },
            },
            parents: 0,
        },
    };
    // amount of fungible tokens to be transferred
    const assets = {
        V1: [
            {
                fun: {
                    Fungible: amount,
                },
                id: {
                    Concrete: {
                        interior: 'Here',
                        parents: 0,
                    },
                },
            },
        ],
    };
```

Signing this transaction will send the KSM token from Kusama to the specified EVM address in Shiden Network. Now that we know who to receive the tokens, how can we actually see and use them within EVM? Because the XCM asset (KSM in this case) is managed within the Assets pallet, it will be accessible through the XC20 interface, which is essentially an ERC20 with a unique contract address.

To obtain the asset address for EVM, we need to get the token asset ID that we wish to use. In our case, we will be using KSM, which has the asset ID of `340282366920938463463374607431768211455`. Now we need to convert the ID to hex and prefix it with `0xffffffff`. The resulting address will be `0xffffffffFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF`. We can directly load this address with the ERC20 interface and use it within our Solidity smart contract or use it within MetaMask.

![Importing tokens in Metamask](../../.gitbook/assets/100\_metamask\_asset\_import.png)

![Local Shiden Assets including KSM](../../.gitbook/assets/101\_local\_shiden\_assets.png)

As you can see from the above image, importing an asset from the created address will correctly read the XCM asset and add it to our wallet. The Shidenator account has some SDN as well as **15 KSM**.
