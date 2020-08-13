---
description: >-
  Substrate is under the active development. If you have issues, feel free to
  ask us on Discord (Tech Chat).
---

# Install

To write smart contracts on Plasm Network, you need to set up the following things on your computer.

### Plasm Node

Currently, we have 2 ways to install ****the Plasm Node as follows.

**①Install from the latest release**

{% embed url="https://github.com/staketechnologies/Plasm/releases/tag/v1.4.0-dusty" %}

**②Build from source**

Make sure you have already installed Rust 

```text
> curl https://sh.rustup.rs -sSf | sh
# on Windows download and run rustup-init.exe
# from https://rustup.rs instead

> rustup update nightly
> rustup target add wasm32-unknown-unknown --toolchain nightly
```

You will also need to install the following dependencies:

* Linux: `sudo apt install cmake git clang libclang-dev build-essential`
* Mac: `brew install cmake git llvm`
* Windows: Download and install the Pre Build Windows binaries of LLVM from [http://releases.llvm.org/download.html](http://releases.llvm.org/download.html)

Install additional build tools:

```text
cargo install --git https://github.com/alexcrichton/wasm-gc
```

Install the Plasm node from git source:

```text
cargo install --force --locked  --git https://github.com/staketechnologies/Plasm --tag v1.4.0-dusty plasm-cli
```

> Alternatively, you can use the following commands to compile directly from the repo (unstable bleeding edge)
> 
> ```text
> git clone https://github.com/staketechnologies/Plasm.git
> cd Plasm
> rustup override set nightly
> cargo build --release
> ./target/release/plasm-node
> ```

Run node on the Plasm canary network  \(Dusty Network\)

```text
plasm-node
```

Or run on your local development network:

```text
plasm-node --dev
```

The final tool we will be installing is ink! utility. 

```text
cargo install cargo-contract --vers 0.6.1 --force
```

{% hint style="info" %}
You can  use  "cargo contract --help" to understand commands
{% endhint %}

Any questions? Feel free to ask [us](https://discord.gg/kH3Njpr).

