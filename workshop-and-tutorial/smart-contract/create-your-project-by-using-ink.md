# Create Your Project by Using ink!

Let's make a folder we need for your project. We are going to use the ink! CLI.

```text
cargo contract new myproj
```

This command creates a new folder named `myproj`

```text
cd myproj
```

Now you could install the simplest ink! smart contract! When you are making your own smart contract, feel free to edit files, and make your own smart contract.

## Test

Off-chain test environment is provided by ink!. We can quickly test your codes.

```text
cargo +nightly build
```

Then,

```text
cargo +nightly test
```

You could see a successful test completion.

Any questions? Feel free to ask [us](https://discord.gg/kH3Njpr).

