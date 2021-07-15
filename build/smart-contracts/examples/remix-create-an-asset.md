---
description: 'Remix is a Solidity IDE that''s used to write, compile and debug Solidity code.'
---

# Remix - Create an Asset

## Create an asset

### Introduction

In this guide, we will create a simple token and deploy this on Dusty. We will build a token with the following specifications:

**Token name:** DUSTY  
**Token symbol:** DST  
**Token decimals:** 18  
**Token supply:** 1000000000000000000000000

###  **Environment**

We will use two tools during this guide:

* [Remix IDE](http://remix.ethereum.org/)
* [MetaMask](https://metamask.io/)

This smart contract will create an asset on Dusty. We don't invent it ourselves. We take the ERC20 smart contract from OpenZeppelin and used example code from [Ethereum Blockchain Developer guide](https://ethereum-blockchain-developer.com/060-tokenization/02-erc20-installation/). If you want to create a more complex token, please do some research about OpenZeppelin. They make things a lot easier and faster for every developer.

{% embed url="https://github.com/OpenZeppelin/openzeppelin-contracts" %}

### Create smart contract

* Go to Remix: [http://remix.ethereum.org/](http://remix.ethereum.org/)
* Let's go to 'File explorer' and 'Create a new file'

![Remix IDE](../../../.gitbook/assets/01%20%282%29.png)

* Let's call this sample contract 'Dusty Token.sol

![](../../../.gitbook/assets/image%20%2830%29.png)

* Copy the following sample code in your smart contract and make your edits. Do not just copy but also read the explanation in the contract.

```sql
//We use this version of Solidity because the contract on OpenZeppelin is build for 0.8.0
pragma solidity ^0.8.0;

//This will import the ERC20 contract from OpenZeppelin to Dusty
import 'https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/ERC20.sol';

// This part will create the token
// To make it easy let's call our contract the same as the Solidity file
contract DustyToken is ERC20 {
  constructor(uint256 initialSupply) ERC20("DUSTY", "DST") { //Token name is DUSTY and token symbol is DST
    _mint(msg.sender, initialSupply); //We can set the initial supply before deploying the contract
  }
}
```

* We are now ready to compile this contract.
* Click on the 'Solidity compiler'
* Make sure that you choose the compiler '0.8.0+commit...', this needs to be the same of in your contract.
* Let's compile 'Dusty Token.sol'

![](../../../.gitbook/assets/02%20%281%29.png)

### Deploy smart contract

Compiled? Yes! Let's deploy our contract to Dusty.

![](../../../.gitbook/assets/03%20%281%29.png)

* Click on 'Deploy & Run transactions'.
* Make sure that you choose 'Injected Web3' as an environment.
* The moment you click on 'Injected Web3', MetaMask will pop up.

![](../../../.gitbook/assets/04%20%281%29.png)

* Make sure you are connected to our Dusty testnet and have some PLD in your wallet. If you don't know how to do this, please check the guide about deploying smart contracts on Dusty.

{% page-ref page="../ethereum-virtual-machine/ethereum-contract-on-dusty-network.md" %}

We are ready to 'Deploy' our contract. As you can see in the screenshot below you need to insert your 'initialSupply' before hitting 'Deploy'.

![](../../../.gitbook/assets/image%20%2828%29.png)

The moment you hit 'Deploy', MetaMask will again pop up to 'Confirm' the transaction. Click on 'Confirm' and wait for the contract to be deployed on Dusty. The contract will appear under 'Deployed Contracts' in Remix. 

![](../../../.gitbook/assets/image%20%2829%29.png)

![](../../../.gitbook/assets/image%20%2826%29.png)

Once the contract is deployed, you can interact with it. Clicking on 'name', 'symbol', and 'totalSupply' should return “DUSTY”, “DST”, and “100000000” respectively. 

If you copy the address from which you deployed the contract and paste it into the balanceOf field, you should see the entirety of the balance of the ERC20 as belonging to that user.

### Add token to MetaMask

Copy the contract address by clicking the button next to the contract name and address.

![](../../../.gitbook/assets/05%20%281%29.png)

You can now interact with a Substrate-based ERC-20 token. Open MetaMask to add the newly deployed asset. In MetaMask, click on “Add Token” and paste the contract address.

![](../../../.gitbook/assets/image%20%2827%29.png)

That's it! Great work.  
Now you can send your asset around and play around.

