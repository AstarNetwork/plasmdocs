# Mainnet collator guide

Astar ecosystem has two main networks. We have permissionless onboarding for collators if you meet our [requirements](learn-about-collators.md). We also have a program to become a whitelisted collator! We are finalizing this in Q1 2022.

#### Astar ecosystem:

* **Shiden Network**: Kusama parachain
* **Astar Network**: Polkadot parachain

## Overview

Before building your collator, make sure you understand the role of collators and you have experience with running a node. If you don't have the experience you can learn by launching a node in our testnet [Shibuya](shibuya-network/).&#x20;

{% content-ref url="learn-about-collators.md" %}
[learn-about-collators.md](learn-about-collators.md)
{% endcontent-ref %}

{% content-ref url="shibuya-network/" %}
[shibuya-network](shibuya-network/)
{% endcontent-ref %}

### Building collator from source

Make sure your server is ready to build a collator:

```
## Install Rust
##
curl https://sh.rustup.rs -sSf | sh
source $HOME/.cargo/env
rustup update nightly
rustup target add wasm32-unknown-unknown --toolchain nightly

## Compile needed software
##
bash -c "$(wget -O - https://apt.llvm.org/llvm.sh)"
sudo apt install cmake 
sudo apt install git 
sudo apt install build-essential
sudo apt update
sudo apt install clang
```

Download everything from our Github:

```shell-session
git clone https://github.com/AstarNetwork/Astar.git
cd Astar
```

Make sure you have the latest commits in place:

```
git checkout
git pull
```

Build your node from source:

```
cargo build --release
```

Start Collator using `screen` or `nohup`:&#x20;

{% tabs %}
{% tab title="Astar" %}
```
cd /target/release/
./astar-collator --validator --name NODENAME --chain astar --parachain-id 2006 --rpc-cors all --telemetry-url 'wss://telemetry.polkadot.io/submit/ 0' --execution wasm --state-cache-size 1
```
{% endtab %}

{% tab title="Shiden" %}
```
cd /target/release/
./astar-collator --validator --name NODENAME --rpc-cors all --telemetry-url 'wss://telemetry.polkadot.io/submit/ 0' --execution wasm --state-cache-size 1
```
{% endtab %}
{% endtabs %}

Get your session key:

```
curl -H "Content-Type: application/json" -d '{"id":1, "jsonrpc":"2.0", "method": "author_rotateKeys", "params":[]}' http://localhost:9933
```

**Make sure you set your session key before registering to become a collator!**

## Build with Docker or use Binaries

### Docker

You can download the docker [here](https://hub.docker.com/layers/staketechnologies/astar-collator/shiden/images/sha256-0a816762ae34767aff8dea62c905b5ca89e8f7a9c0d6f046c20514fa8474c329?context=explore).

### Binaries

You can download the latest binary from [here](https://github.com/AstarNetwork/Astar/releases).

## Relay Chain snapshot

If you run your collator it not only needs to sync the mainnet chain but also the complete relay chain from Kusama/Polkadot. This can take up to 3-4 days. You can also use a snapshot of Kusama/Polkadot. You can download this [here](https://polkashots.io) and will save a lot of time.

**NOTE**: know what you are doing!
