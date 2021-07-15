# WASM - Create an NFT

This guide is a step-by-step guide to deploy a WebAssembly \(WASM\) smart contract. As a result, the output is highly optimized, which saves you gas costs.

In this tutorial, we will create a non-fungible token \(NFT\) and deploy it to our public testnet Dusty.

ERC721 is a standard for representing ownership of _non-fungible_ tokens, that is, where each token is unique such as in real estate or collectibles.

## Setup

### Substrate Prerequisites <a id="substrate-prerequisites"></a>

During this part, we will set up a Rust environment with the latest `nightly`release

```text
rustup component add rust-src --toolchain nightly
rustup target add wasm32-unknown-unknown --toolchain stable
```

### ink! CLI <a id="ink-cli"></a>

As a pre-requisite for the tool, you need to install the [binaryen](https://github.com/WebAssembly/binaryen) package, which is used to optimize the WebAssembly bytecode of the contract. Many package managers have it available nowadays ‒ e.g., it's a package for [Debian/Ubuntu](https://tracker.debian.org/pkg/binaryen), [Homebrew](https://formulae.brew.sh/formula/binaryen), and [Arch Linux](https://archlinux.org/packages/community/x86_64/binaryen/).

After you've installed the package, execute:

```text
cargo install cargo-contract --vers ^0.11 --force --lockedCopy to clipboardErrorCopied
```

You can then use `cargo contract --help` to start exploring the commands made available to you.

![Installation of cargo-contract](../../../.gitbook/assets/image%20%2837%29.png)

## Create an ink! contract

We are going to use ink! CLI to generate the files we need for a WASM smart contract project. Make sure you are in your working directory and then run:

re in your working directory and then run:

```text
cargo contract new erc721
```

This command will create a new project folder named `erc20` which we will explore:

```text
cd erc721
```

**ink! Contract Project**

```text
NFToken
|
+-- lib.rs                <-- Contract Source Code
|
+-- Cargo.toml            <-- Rust Dependencies and ink! Configuration
```

### Contract Source Code <a id="contract-source-code"></a>

The ink CLI automatically generates the source code for a standard ink! contract. You can take a sneak peek to have a look at some code. Now, let's add some code. In this guide, we will use [Visual Studio Code](https://code.visualstudio.com/).

```text
code .
```

![Template ERC721 contract](../../../.gitbook/assets/image%20%2854%29.png)

You can find our example contract here:

{% embed url="https://github.com/PlasmNetwork/plasmdocs/tree/master/example/wasm/erc721" %}

Just replace the code in your `lib.rs` file with the complete code from our template.

## Testing the contract

You will see at the bottom of the source code there is a simple test that verifies the contract functionality. We can test this code is functioning as expected using the **off-chain test environment** that ink! provides.

In your project folder, run:

```text
cargo +nightly test
```

To which you should see a successful test completion:

![](../../../.gitbook/assets/image%20%2850%29.png)

Now that we are feeling confident things are working, we can actually compile this contract to WASM.

## Build your contract

Run the following command to compile your smart contract:

```text
cargo +nightly contract build
```

![Building contract](../../../.gitbook/assets/image%20%2853%29.png)

## Deploy your contract 

Let's deploy the contract now on Plasm/Shiden or Dusty, our testnet.  
In this guide, I will use our testnet, 'Dusty'. To deploy your contract go to '**Developer - Contracts**'. Click on '**Upload and deploy code**'.

![](../../../.gitbook/assets/01%20%283%29.png)

Load your `contract`file and give your bundle a name. I used 'My NFT'

![Upload .contract file](../../../.gitbook/assets/image.png)

![Add PLD to keep your contract alive.](../../../.gitbook/assets/image%20%2852%29.png)

After being deployed you can start mint your NFT. Those are the availble command:

![Contract calls.](../../../.gitbook/assets/image%20%2851%29.png)

That's it! Great work.  
Now you can send mint and send your NFT around.

