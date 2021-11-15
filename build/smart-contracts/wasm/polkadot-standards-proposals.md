# Polkadot Standards Proposals

## PSPs - Polkadot Standards Proposals

Polkadot ecosystem needs its own set of standards to fit ecosystem needs. Please visit [Polkadot Standards Proposals (PSPs) Github](https://github.com/w3f/PSPs).

These standards go through several acceptance phases, and the engagement of the whole community is needed to build valuable and future-proof standards. All the teams who will benefit from a standard needs to agree on its content

### PSP22 - Fungible Token Standard

The [PSP22 Fungible Token standard](https://github.com/w3f/PSPs/blob/master/PSPs/psp-22.md) is inspired by the ERC20 from Ethereum. It targets every parachain that integrates pallet-contract to enable WASM smart contracts. It is defined at ABI level, so it should be used for any language that compiles to WASM (and is not restricted to ink! specifically).

PSP22 will have a double impact:

* On Parachain level, it will ensure the PSP22 is used to enable true interoperability.
* In the multi-chain future, it will secure interoperability of all token standards (PSP22 and the next coming) between differents parachains or other substrate base chains.

It also helps to have a predefined interface for specific token standards to ensure exhaustive logic is implemented. It will also encourage to share the most performant & secure implementation. For reference implementation please refer to [PSP22 - OpenBrush](https://github.com/Supercolony-net/openbrush-contracts/blob/main/contracts/token/psp22/src/traits.rs)

This standard was the first to be accepted by the community. Please refer to the official [PSPs repo](https://github.com/w3f/PSPs) to be aware of latest standards.
