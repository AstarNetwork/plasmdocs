---
description: >-
  Substrate is under the active development. If you have issues, feel free to
  ask us on Discord (Tech Chat).
---

# Install

To write smart contracts on Plasm Network, you need to set up the following things on your computer.

## Plasm Node

### Install a Plasm Node

To use a  local development environment, a Plasm node is necessary. Please install the latest Plasm node from here: [https://github.com/staketechnologies/Plasm/tree/dusty](https://github.com/staketechnologies/Plasm/tree/dusty) \([build instruction](https://github.com/staketechnologies/Plasm/tree/dusty#building-from-source)\).

The next step is to launch a node in the development environment.

```text
plasm-node --dev -l evm=debug
Oct 14 15:07:56.998  WARN Running in --dev mode, RPC CORS has been disabled.    
Oct 14 15:07:56.998  INFO Plasm Node                                                                                           
Oct 14 15:07:56.998  INFO ✌️  version 1.6.0-1dc78cce-x86_64-linux-gnu    
Oct 14 15:07:56.998  INFO ❤️  by Stake Technologies <devops@stake.co.jp>, 2019-2020    
Oct 14 15:07:56.998  INFO 📋 Chain specification: Development     
Oct 14 15:07:56.998  INFO 🏷  Node name: skillful-war-1171    
Oct 14 15:07:56.998  INFO 👤 Role: AUTHORITY
```

### **Build from source**

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

Run node on the Plasm canary network \(Dusty Network\)

```text
plasm
```

Or run on your local development network:

```text
plasm --dev
```

The final tool we will be installing is ink! utility.

```text
cargo install cargo-contract --vers ^0.11 --force --locked
```

{% hint style="info" %}
You can use "cargo contract --help" to understand commands
{% endhint %}

Any questions? Feel free to ask [us](https://discord.gg/kH3Njpr).

