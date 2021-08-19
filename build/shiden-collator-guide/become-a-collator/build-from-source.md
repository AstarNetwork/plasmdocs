# Build from source

## Overview

Before building your collator, make sure you understand the role of collators in the Shiden Network and you have experience with running a node. If you don't have the experience you can learn by launching a node for our testnet Dusty.

{% page-ref page="../learn-about-collators.md" %}

{% page-ref page="../../validator-guide/" %}

## Building Shiden collator

Make sure your server is ready to build a Shiden collator:

```text
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

Download everything from our Github and use the Shiden branch:

```text
git clone https://github.com/PlasmNetwork/Astar.git
cd Astar
git checkout production/shiden
```

Make sure you have the latest commits in place:

```text
git checkout
git pull
```

Build your node from source:

```text
cargo build --release
```

Start Collator using `screen` or `nohup`:

```text
cd /target/release/
./astar-collator --validator --name NODENAME --rpc-cors all
```

Get session key:

```text
curl -H "Content-Type: application/json" -d '{"id":1, "jsonrpc":"2.0", "method": "author_rotateKeys", "params":[]}' <http://localhost:9933>
```

**Make sure you set your session key before register to become a collator!**

