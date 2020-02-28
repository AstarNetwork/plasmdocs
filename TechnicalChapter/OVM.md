# OVM

OVM(Optimistic Virtual Machine) is a powerful concept to develop Layer 2. We can express complex dispute logic by simple OVM language, and that language consists of [Optimistic Game Semantics](https://plasma.group/optimistic-game-semantics.pdf). For example, we can express Plasma checkpoint and exit claims with 2 simple definitions (we call these "property") by OGS. Plasm Network separates the OVM from the smart contract and prepares it as a module so that OVM can be used more simply and conveniently.

## OVM in Plasm Network

The OVM and its surrounding architecture are as shown in the below figure.

![ovmodule](https://user-images.githubusercontent.com/6259384/75546609-404d5880-5a6c-11ea-84d0-f063e0bc252c.png)

Plasma applications (Plapps) can be created and run properly through the dedicated client application L1 adapter. Plapps are composed of OVM, Plasma and Contracts modules in Plasm Network. In Plasma development at Ethereum, everything provided in these modules was managed by smart contracts. However, in that case, there is a problem that it is difficult to predict the gas cost when running a plasma application containing complicated logic. Also, building applications that combine multiple contracts can be confusing to developers. For this reason, Plasma Network has considered a superficially concise and easy-to-understand configuration by separating the roles into three modules. The OVM Module implements a function called Universal Adjudication to cause a dispute when the user finds a mistake in the information on Layer1. The Plasma Module supports a common implementation of some of the essential smart contracts for Plasma. Only the implementations that require different logic for each application are managed by the Contracts Module.

These Plasm Network logics can be combined with the implementation provided by the Plasma L2 Implementation described above to build an application.