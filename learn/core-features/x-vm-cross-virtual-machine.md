# X-VM \(Cross Virtual Machine\)

In this section, we are going to introduce our core feature called the **X-VM \(Cross Virtual Machine\)**. Our vision for X-VM is to establish a layer of abstraction that allows smart contracts to execute calls and read storage data from different contract engines \(virtual machine\) and languages \(ex, interacting with Solidity dApps written in from ink! or vise versa\) within the same blockchain.

As Dr.Gavin Wood mentioned earlier, using WebAssembly as smart contracts is the future, but Ethereum Virtual Machine is important now.

{% embed url="https://www.coindesk.com/polkadot-gavin-wood-webassembly-smart-contracts-evm" %}

WebAssembly is undoubtedly superior for smart contract execution. WASM-based engines have a bright future as many great developers like [Patract Lab](https://patract.io/) are making WebAssembly easier for developers to use on Polkadot.

However, we still see value in EVM, as we are staying close with the latest developments of Ethereum’s layer2 solutions like Optimistic Rollups and ZK Rollups. We have already started implementing the Rollups in the Plasm Ecosystem, supported by Web3 Foundation Grant Program.

Adding on to this, most new developers will start from learning Ethereum. Established projects will want to maintain their current workflow on Ethereum, and the mainstream will be exposed to the world of blockchains through dApps on Ethereum. Considering the matured ecosystem of Ethereum and its accessibility for new people, the EVM as it is today will be obsolete in the future. But the ecosystem won’t be going away. Instead, it will be a _portal to the future_. Similar to how the Internet Explorer is a portal for downloading better browsers.

We believe that, in a heterogeneous blockchain world, ‘EVM’ won’t just refer to a specific architecture for smart contract engines but will be treated as an ‘Ethereum-like development environment.’

**We treat all dApps as equal. Therefore, we aim to support both WebAssembly and Ethereum Virtual Machine on Plasm & Shiden Network by making them interactive. We see a future where EVM can be looked at as another framework for making dApps alongside ink!, HyperLedger Fabric, EOSIO, and future virtual machines.**

As the number of blockchains supporting bridges, XCMP, or other swapping channels increase, blockchains are no longer a monolithic network. Developers will have to add layers and layers of abstraction to keep up with this change. We believe that for blockchain ecosystems to grow, adding support for cross virtual machine communication is required. This is where X-VM comes in.

In addition to that, since Ethereum compatibility is developed by Parity Technologies, we think supporting EVM and Solidify contracts won’t be a differentiator. Even today, all Parachains can support them easily.

## How X-VM Help Developers? <a id="8e64"></a>

Since Polkadot and Kusama natively support WebAssembly, more and more projects will use WebAssembly as the main smart contract engine of choice. It’s not hard to imagine many smart contracts working in their own [sandboxed environment](https://hacks.mozilla.org/2019/08/webassembly-interface-types/).

We expect the biggest issue to arise from the differences in the language used to write the contract and the different client-side libraries the developer needs to interact with.

For example, if ink! contracts are more popular in the Polkadot ecosystem, the ability to call ink! contracts from a contract written in Solidity will be crucial. Projects that wish to fully leverage the capabilities of Substrate’s native modules, XCMP, and features from other Parachains will have to switch from Solidity to ink!. Similar to the long transition from Ethereum 1.0 to Ethereum 2.0, we understand that migrating to a new environment while maintaining backward compatibility is not an easy process.

As Astar and Shiden aims to become the hub for dApps on the Polkadot ecosystem, we see the need to add syntactical and functional support for both WASM-based contracts and EVM-based contracts.

## Astar and Shiden ’s Architecture <a id="0669"></a>

Astar/Shiden is a scalable multi-chain smart contract hub on Polkadot/Kusama that is natively supporting both EVM and WASM. Even today, developers can deploy Solidity smart contracts and ink! smart contracts on Astar Network’s testnet, Dusty.

Many people are already familiar with EVM and its developments. So, in the next section, I will elaborate on why WASM as a smart contract engine is feasible.

## Why WASM? <a id="26a1"></a>

![](https://miro.medium.com/max/1312/1*VnCtIgtARVpHTx8i6B7lHg.png)

Why would developers use WASM for smart contracts:

* WASM’s performance is very high. The language is built to be as close to native machine code as possible while still being independent.
* WASM massively reduces processing times in browsers because of the use of small binaries. This offers great scalability to potentially slow internet connections that want to use blockchain technology.
* WASM was developed so that code can be deployed in any browser with the same result. Contrary to the EVM, it was not developed towards a very specific use case. This has the benefit of a lot of tooling being available and large companies putting a lot of resources into furthering WASM’s development.
* WASM expands the use of languages to smart contract developers to include Rust, C/C++, C\#, Typescript, Haxe, and Kotlin. This means developers can write smart contracts in whichever language they’re familiar with.

Because ink! is a Domain-Specific Language \(DSL\) for making smart contracts in Substrate, the development environment is the same as most projects made in Rust. It’s a perfect match for the Polkadot ecosystem as it’s written in the same language. So why did Polkadot choose Rust for everything? [Why Rust?Programming is hard. Not because our hardware is complex, but simply because we're all humans. Our attention span is…www.parity.io](https://www.parity.io/why-rust/)

This brings us to another question. Why would we use Rust in smart contracts?

* Rust ecosystem and community: [Rust documentation](https://doc.rust-lang.org/) is very extended with a very strong developers community. All is knowledge is shared on the internet. The language keeps developing, ink! will automatically keep following these developments. All those new features and functionality will improve how you can write smart contracts in the future.
* We believe Rust is an ideal smart contract language: it is **type safe**, **memory safe**, and **free of undefined behaviors**. Through compiler flags, Rust can automatically protect against integer overflow.
* Rust provides first-class support for WebAssembly.

[WebAssemblyPlays well with JavaScript The dream of WebAssembly is not to kill JavaScript but to work alongside of it, to help…www.rust-lang.org](https://www.rust-lang.org/what/wasm)

* ink! follows Rust standards, tools like rustfmt, clippy, and rust-analyzer already work out of the box. The same goes for code formatting and syntax highlighting in most modern text editors. Also, Rust has an integrated test and benchmark runner.
* **Small code size** means faster page loads. Rust-generated `.wasm` doesn’t include extra bloat, like a garbage collector. Advanced optimizations and tree shaking remove dead code. In the space-constrained blockchain world, size is important. The Rust compiler is a great help since it reorders struct fields to make each type as small as possible.

## Our Starting Point <a id="712a"></a>

We see X-VM as a long-term project that can ease development in the vastly fragmented smart contract development environment we have today.

As a start, we plan to implement a Proof-of-concept version of the Substrate contract module call as an EVM [precompiled contract](https://blog.qtum.org/precompiled-contracts-and-confidential-assets-55f2b47b231d) for the [Frontier library](https://github.com/paritytech/frontier#evm-pallet-precompiles) in Substrate. This will enable a one-directional contract call from EVM to ink!. At the moment, calling the Substrate contract pallet as a precompiled contract on EVM will be limited in functionality. Still, we hope to use this PoC implementation as the beginning for developing X-VM as a native module that can unify the various contract engines, like how the OVM unifies the layer 2 protocols.

In the future, we plan to make a standard contract development environment tool like Truffle or Hardhat for developing on Astar Network.

