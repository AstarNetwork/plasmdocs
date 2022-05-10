# AstarBase

There are a couple of facts about the Astar ecosystem:

* Majority of the crowdloan participants used their Polkadot native addresses (ss58) and these users are the majority of dApps-Staking participants.
* While Astar is building a multi Virtual-Machine future, today most of the dApps are using Ethereum Virtual Machine (EVM) which uses Ethereum address space, usually referred to as MetaMask accounts or H160.
* Astar's unique feature is dApps Staking which provides a basic income for developers and a staking mechanism for the users. Both dApps developers and users benefit from it.

The goals of the AstarBase product are:

* Bring more users to EVM dApps;
* Create more opportunities for end-users to participate in the Astar ecosystem;
* Enable EVM dApps to attract and reward users even though they have the majority of their funds staked on dApps Staking;
* Encourage users to stake and use the dApp Staking mechanism.

### Interface

AstarBase is an on-chain EVM database. AstarBase contains a mapping of the user's EVM and Native SS58 address. Such mapping on its own does not bring any benefit to the projects since anyone can register this address pair. What brings the value is the call `checkStakerStatus()` which checks if the ss58 address of the pair is an active staker. The AstarBase contracts are available on each of Shibuya/Shiden/Astar Networks. The deploy addresses can be found in the [AstarBase github repository](https://github.com/AstarNetwork/astarbase/blob/main/contract/contracts/info.md).

There are 2 interface functions that can be used.

* `isRegistered()` checks if the given address was registered in Astarbase

```
    function isRegistered(address evmAddress) 
        external view 
        returns (bool);
```

* `checkStakerStatus()` Checks if pair of addresses (ss58, evm) is an active staker in dApps-staking and returns staked amount

```
    function checkStakerStatus(address evmAddress)
        external view
        returns (uint128);
```

### Use from Client side

The `abi` for the contract can be found in [AstarBase Github repository](https://github.com/AstarNetwork/astarbase/blob/main/public/config/register\_abi.json).\
The following is an example of usage of the Astarbase from the client-side.

```
  if (metamaskIsInstalled) {
    Web3EthContract.setProvider(ethereum);
    try {
      
      const smartContract = new Web3EthContract(
        abi,
        CONFIG.ASTARBASE_ADDRESS
      );

      const stakerStatus = await smartContract.methods.checkStakerStatus(user).call();
      const isRegistered = await smartContract.methods.isRegistered(user).call();

      return isRegistered && stakerStatus > 0;
    } catch (err) {
      console.log(err);
      return false;
    }
  } else {
    console.log('Install Metamask.');
  }
```

### Use from Contract side

The following is an example usage when EVM contract wants to check staker status for `H160` address

```
import "./AstarBase_flat.sol"
contract A {
    // Deployed on Shiden
    AstarBase public ASTARBASE = AstarBase(0x20044438CfaF684e251d1FfC70f999291D49e9a7);
    ...
    
    function stakedAmount(address user) private view returns (uint128) {

        // The returned value from checkStakerStatus() call is the staked amount,
        return ASTARBASE.checkStakerStatus(user);
    }
}
```

### Example use case: NFT discount price

In the [minting-dapp Github repository](https://github.com/AstarNetwork/minting-dapp/blob/main/contract/contracts/ShidenPass\_flat.sol) you will find an example NFT minting dApp which uses AstarBase to mint free NFT for active dApp stakers. The same example could be easily adapted to give a discount price instead of free NFT.

### Example use case: ERC20 airdrop claim.

A new project coming to Astar ecosystem would like to attract users by ERC20 token airdrop. But they want users who are active participants in the ecosystem and not one-time users who will disappear once the airdrop is claimed. AstarBase can be used to allow airdrop claim only to registered users.

1. if ASTARBASE.checkStakerStatus(user) > 0 ;

### Example use case: Rewards for stakers

A project is using dApps-staking as basic income but would also like to reward stakers who are staking on them. Since those stakes use their native Astar address (s58) for staking and this project is based on EVM, there was no way to give EVM-based rewards. Astarbase gives the possibility to reward such users if they are registered in AstarBase

1. Collect all stakers' addresses from the client-side
2. Verify the Astarbase mapping for ss58->evmAddress
3. Allow reward claiming to evmAddress for verified stakers

### Example use case: Bot protection

There is no absolute protection against bots, but at least their usage might be financially questionable. The reason is the minimum staked amount for the dApps-staking and the unbound period. By using AstarBase you force bots to use active stakers' addresses in case they want to reap your project's rewards.





### ECDSA address registration

[ECDSA](https://en.wikipedia.org/wiki/Elliptic\_Curve\_Digital\_Signature\_Algorithm) address requires a manual generation of a public key by a user as ECDSA public key cannot be extracted from the ss58 address. Never share your seed phrase or private keys with anyone.

For generating ECDSA address public key here are the steps:

* Install [subkey](https://docs.substrate.io/v3/tools/subkey/) tool.
* Go to command line and run: `curl https://getsubstrate.io -sSf | bash -s -- --fast`
* Install subkey from cargo:

`cargo install --force subkey --git https://github.com/paritytech/substrate --version 2.0.1 --locked`

* Inspect your seed phrase with ECDSA schema.

`subkey inspect --scheme ecdsa "Your 12 words mnemonic seed phrase"`

You will get following output:

```
> subkey inspect --scheme ecdsa "caution juice atom organ advance problem want pledge someone senior holiday very" 
Secret phrase: caution juice atom organ advance problem want pledge someone senior holiday very 
Network ID: substrate Secret seed: 0xc8fa03532fb22ee1f7f6908b9c02b4e72483f0dbd66e4cd456b8f34c6230b849 
Public key (hex): 0x03b2217d2c348df72c4789947291e2e63ba7798baebaa937f40fd5d68f022dd4b4 
Account ID: 0x9bd03f5c43588e0e8110463dde4122bce1279d683de87e95975f7c717f00d617 
Public key (SS58): KWCjsULBCExp8BTVhVjVjWrqMYxSi4a1CRyU2tyzNiAs4mLk8 
SS58 Address: 5Fb19AznKQqtHLf82PfMXKwWPqAWPB9g7fW6AhP8BVJ8Soqo`
```

* You will be asked to input a public key during Astar pass registration.
* Paste the Public key (hex) value in the input field
