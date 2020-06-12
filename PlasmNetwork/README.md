# Plasm Network
 Plasm Network is a Substrate blockchain project that provides the methods for developing scalable dApps. The general architecture can be visible from the following figure. 

Plasm Network is a Layer1 permissionless public blockchain where everyone can join. Since it is built with the Substrate framework, Plasm Network is capable of becoming a Polkadot Parachain and it is expected to be the first scalable Parachain in the Polkadot ecosystem.  Plasm Network consists of the Plasm main chain and multiple Plasm child chains. In general, Plasm Network is the default root chain for developers to connect their applications. Plasm Network provides various modules that allow the developers to utilize Layer2 solutions with ease, such as the OVM module and dAppsStaking module. In addition, it has an innovative token issuance mechanism. The issue with the traditional dApps platform is that despite the fact that creators of applications are contributing to the ecosystem, they have to pay the price for doing so in the form of Gas. To solve this issue, we divide the block reward to two. 50% of the block rewards on the Plasm root chain are distributed to dApps developers who increase the value of the network and the other 50% of rewards are distributed to the validators of the block. By doing this, half of the block rewards can act as a basic income for dApps developers, which not only incentivizes the validators but also incentivizes the developers for the platform. 

![plasm_network_001](https://user-images.githubusercontent.com/6259384/77140423-e402b500-6abc-11ea-8f17-30b44cf2de58.png)

In addition to implementing Layer2 solutions that are not possible in Plasma, we have the **Plasma as a Service** for supporting dApps developers. Plasma as a Service is a form of Platform as a Service that allows developers to easily deploy Plasma applications. It is capable of allowing developers to choose a parent chain *that* they want to deploy their application to and deploy a custom child chain onto it. This fully managed via an intuitive GUI that does not require the developers to go through the pain of learning everything from scratch. We plan on implementing this via the [Plasma Rust Frameworks](https://github.com/cryptoeconomicslab/plasma-rust-framework) provided by [Cryptoecnomics Lab](https://www.cryptoeconomicslab.com/).

This chapter discusses about Plasm Network.

## [Plasm Network Lockdrop](./Lockdrop.md)
This item explains the overview of the lockdrop design(token distributed algorithm).

## [Consensus Algorithm](./ConsensusAlgorithm.md)
This item explains the overview of consensus algorithm.

## [dApps Rewards](./dAppsRewards.md)
This item explains about the dApps Rewards.

## [Token Ecosystem](./TokenEcosystem.md)
This item explains about the Token Ecosystem.

## [Operator Trading](./OperatorTrading.md)
This item explains about the operator trading.

## [Real-time Lockdrop](./RealtimeLockdrop.md)
This item explains about the Real-time Lockdrop module.
