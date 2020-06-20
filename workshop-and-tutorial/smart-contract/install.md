---
description: >-
  Substrate is  under the active development. If you have issues, feel free to
  ask us on Discord (Tech Chat).
---

# Install

To write smart contracts on Plasm Network, you need to set up following things on your computer.

### Substrate

If you don't install Substrate yet, please set up to build Substrate as a first step.

**OSX or Linux** 

```text
curl https://getsubstrate.io -sSf | bash -s -- --fast

rustup target add wasm32-unknown-unknown --toolchain stable
rustup component add rust-src --toolchain nightly
```

**Windows**

if you are using Windows, please refer to [Substrate Developer Hub](https://substrate.dev/docs/en/knowledgebase/getting-started/windows-users) maintained by Parity Technologies.

Then, let's install a Substrate node that contains the Contracts module.

```text
cargo install node-cli --git https://github.com/paritytech/substrate.git --force
```

The final tool we will be installing is ink! utility. 

```text
cargo install cargo-contract --vers 0.6.1 --force
```

{% hint style="info" %}
You can  use  "cargo contract --help" to understand commands
{% endhint %}

