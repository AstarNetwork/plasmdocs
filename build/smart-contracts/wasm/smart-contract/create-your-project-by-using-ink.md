# Create Your Project by Using ink!

Let's make a folder for your project. We are going to use the ink! CLI to help us with this.

```text
cargo contract new my_contract
```

 This command creates a new folder named `my_contract` . 

```text
cd my_contract
```

This folder contains a `Cargo.toml` file and a `lib.rs` file. The `lib.rs` file is an example of a very simple ink! smart contract. When writing your own smart contracts, feel free to edit the files accordingly.

### Test

An off-chain test environment is provided by ink! to quickly test our code. First, let's build the files.

```text
cargo +nightly build
```

Then to run the test,

```text
cargo +nightly test
```

You should see the output of 2 successful tests in your command line.

Any questions? Feel free to ask [us](https://discord.gg/kH3Njpr).

