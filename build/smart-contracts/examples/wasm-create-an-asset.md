# WASM - Create an Asset

This guide is a step-by-step guide to deploy a WebAssembly \(WASM\) smart contract. As a result, the output is highly optimized, which saves you gas costs.

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

```text
cargo contract new erc20
```

This command will create a new project folder named `erc20` which we will explore:

```text
cd erc20
```

**ink! Contract Project**

```text
erc20
|
+-- lib.rs                <-- Contract Source Code
|
+-- Cargo.toml            <-- Rust Dependencies and ink! Configuration
```

### Contract Source Code <a id="contract-source-code"></a>

The ink CLI automatically generates the source code for an ERC20 contract. You can take a sneak peek to have a look at some code. This is a very basic ERC20 contract.

Now, let's add some code. In this guide, we will use [Visual Studio Code](https://code.visualstudio.com/).

```text
code .
```

![ERC20 WASM code in Visual Studio Code](../../../.gitbook/assets/image%20%2834%29.png)

## Testing your contract

![](../../../.gitbook/assets/image%20%2833%29.png)

You will see at the bottom of the source code there is a simple test that verifies the contract functionality. We can quickly test that this code is functioning as expected using the **off-chain test environment** that ink! provides.

In your project folder, run:

```text
cargo +nightly test
```

To which you should see a successful test completion:

![](../../../.gitbook/assets/image%20%2832%29.png)

When we are making the ERC20 contract more complex, you can add more tests. 

![](../../../.gitbook/assets/image%20%2839%29.png)

This is how my test contract looks like:

```sql
#![cfg_attr(not(feature = "std"), no_std)]

use ink_lang as ink;

#[ink::contract]
mod erc20 {
    #[cfg(not(feature = "ink-as-dependency"))]
    #[ink(storage)]
    pub struct Erc20 {
        /// The total supply.
        total_supply: Balance,
        /// The balance of each user.
        balances: ink_storage::collections::HashMap<AccountId, Balance>,
        /// Approval spender on behalf of the message's sender.
        allowances: ink_storage::collections::HashMap<(AccountId, AccountId), Balance>,
    }

    #[ink(event)]
    pub struct Transfer {
        #[ink(topic)]
        from: Option<AccountId>,
        #[ink(topic)]
        to: Option<AccountId>,
        #[ink(topic)]
        value: Balance,
    }

    #[ink(event)]
    pub struct Approval {
        #[ink(topic)]
        owner: AccountId,
        #[ink(topic)]
        spender: AccountId,
        #[ink(topic)]
        value: Balance,
    }

    impl Erc20 {
        #[ink(constructor)]
        pub fn new(initial_supply: Balance) -> Self {
            let caller = Self::env().caller();
            let mut balances = ink_storage::collections::HashMap::new();
            balances.insert(caller, initial_supply);

            Self::env().emit_event(Transfer {
                from: None,
                to: Some(caller),
                value: initial_supply,
            });

            Self {
                total_supply: initial_supply,
                balances,
                allowances: ink_storage::collections::HashMap::new(),
            }
        }

        #[ink(message)]
        pub fn total_supply(&self) -> Balance {
            self.total_supply
        }

        #[ink(message)]
        pub fn balance_of(&self, owner: AccountId) -> Balance {
            self.balance_of_or_zero(&owner)
        }

        #[ink(message)]
        pub fn approve(&mut self, spender: AccountId, value: Balance) -> bool {
            // Record the new allowance.
            let owner = self.env().caller();
            self.allowances.insert((owner, spender), value);

            // Notify offchain users of the approval and report success.
            self.env().emit_event(Approval {
                owner,
                spender,
                value,
            });
            true
        }

        #[ink(message)]
        pub fn allowance(&self, owner: AccountId, spender: AccountId) -> Balance {
            self.allowance_of_or_zero(&owner, &spender)
        }

        #[ink(message)]
        pub fn transfer_from(&mut self, from: AccountId, to: AccountId, value: Balance) -> bool {
            // Ensure that a sufficient allowance exists.
            let caller = self.env().caller();
            let allowance = self.allowance_of_or_zero(&from, &caller);
            if allowance < value {
                return false;
            }

            let transfer_result = self.transfer_from_to(from, to, value);
            if !transfer_result {
                return false
            }

            // Decrease the value of the allowance and transfer the tokens.
            self.allowances.insert((from, caller), allowance - value);
            true
        }

        #[ink(message)]
        pub fn transfer(&mut self, to: AccountId, value: Balance) -> bool {
            self.transfer_from_to(self.env().caller(), to, value)
        }

        fn transfer_from_to(&mut self, from: AccountId, to: AccountId, value: Balance) -> bool {
            let from_balance = self.balance_of_or_zero(&from);
            if from_balance < value {
                return false
            }

            // Update the sender's balance.
            self.balances.insert(from, from_balance - value);

            // Update the receiver's balance.
            let to_balance = self.balance_of_or_zero(&to);
            self.balances.insert(to, to_balance + value);

            self.env().emit_event(Transfer {
                from: Some(from),
                to: Some(to),
                value,
            });

            true
        }

        fn balance_of_or_zero(&self, owner: &AccountId) -> Balance {
            *self.balances.get(owner).unwrap_or(&0)
        }

        fn allowance_of_or_zero(&self, owner: &AccountId, spender: &AccountId) -> Balance {
            *self.allowances.get(&(*owner, *spender)).unwrap_or(&0)
        }
    }

    #[cfg(test)]
    mod tests {
        use super::*;

        use ink_lang as ink;

        #[ink::test]
        fn new_works() {
            let contract = Erc20::new(777);
            assert_eq!(contract.total_supply(), 777);
        }

        #[ink::test]
        fn balance_works() {
            let contract = Erc20::new(100);
            assert_eq!(contract.total_supply(), 100);
            assert_eq!(contract.balance_of(AccountId::from([0x1; 32])), 100);
            assert_eq!(contract.balance_of(AccountId::from([0x0; 32])), 0);
        }

        #[ink::test]
        fn transfer_works() {
            let mut contract = Erc20::new(100);
            assert_eq!(contract.balance_of(AccountId::from([0x1; 32])), 100);
            assert!(contract.transfer(AccountId::from([0x0; 32]), 10));
            assert_eq!(contract.balance_of(AccountId::from([0x0; 32])), 10);
            assert!(!contract.transfer(AccountId::from([0x0; 32]), 100));
        }

        #[ink::test]
        fn transfer_from_works() {
            let mut contract = Erc20::new(100);
            assert_eq!(contract.balance_of(AccountId::from([0x1; 32])), 100);
            contract.approve(AccountId::from([0x1; 32]), 20);
            contract.transfer_from(AccountId::from([0x1; 32]), AccountId::from([0x0; 32]), 10);
            assert_eq!(contract.balance_of(AccountId::from([0x0; 32])), 10);
        }

        #[ink::test]
        fn allowances_works() {
            let mut contract = Erc20::new(100);
            assert_eq!(contract.balance_of(AccountId::from([0x1; 32])), 100);
            contract.approve(AccountId::from([0x1; 32]), 200);
            assert_eq!(contract.allowance(AccountId::from([0x1; 32]), AccountId::from([0x1; 32])), 200);

            assert!(contract.transfer_from(AccountId::from([0x1; 32]), AccountId::from([0x0; 32]), 50));
            assert_eq!(contract.balance_of(AccountId::from([0x0; 32])), 50);
            assert_eq!(contract.allowance(AccountId::from([0x1; 32]), AccountId::from([0x1; 32])), 150);

            assert!(!contract.transfer_from(AccountId::from([0x1; 32]), AccountId::from([0x0; 32]), 100));
            assert_eq!(contract.balance_of(AccountId::from([0x0; 32])), 50);
            assert_eq!(contract.allowance(AccountId::from([0x1; 32]), AccountId::from([0x1; 32])), 150);
        }
    }
}

```

Now that we are feeling confident things are working, we can actually compile this contract to Wasm.

### Build your contract

Run the following command to compile your smart contract:

```text
cargo +nightly contract build
```

![](../../../.gitbook/assets/image%20%2838%29.png)

This special command will turn your ink! project into a Wasm binary, a metadata file \(which contains the contract's ABI\), and a `.contract` file that bundles both. This `.contract` file can be used for deploying your contract to Plasm/Shiden chain. If all goes well, you should see a `target` folder that contains these files:

```text
target
└── erc20.wasm
└── metadata.json
└── erc20.contract
```

Let's take a look at the structure of the `metadata.json`:

```text
{
  "registry": {
    "strings": [...],
    "types": [...]
  },
  "storage": {...},
  "contract": {
    "name": ...,
    "constructors": [...],
    "messages": [...],
    "events": [],
    "docs": []
  }
}Copy to clipboardErrorCopied
```

You can see that this file describes all the interfaces that can be used to interact with your contract.

* The registry provides the **strings** and custom **types** used throughout the rest of the JSON.
* Storage defines all the **storage** items managed by your contract and how to ultimately access them.
* Contract stores information about the callable functions like **constructors** and **messages** a user can call to interact with your contract. It also has helpful information like the **events** that are emitted by the contract or any **docs**.

If you look closely at the constructors and messages, you will also notice a `selector` which is a 4-byte hash of the function name and is used to route your contract calls to the correct functions.

The Canvas UI uses this file to generate a friendly interface for deploying and interacting with your contract. :\)

## Deploy your contract 

Let's deploy the contract now on Plasm/Shiden or Dusty, our testnet.  
In this guide, I will use our testnet, 'Dusty'. To deploy your contract go to '**Developer - Contracts**'. Click on '**Upload and deploy code**'.

![](../../../.gitbook/assets/01%20%283%29.png)

Load your `contract`file and give your bundle a name. I used 'DustyToken'

![](../../../.gitbook/assets/image%20%2836%29.png)

In my case, I had to enter my total supply and that's it. Deploy and contract is in place!

![](../../../.gitbook/assets/image%20%2835%29.png)

That's it! Great work.  
Now you can send your asset around and play around.

## Support

Come join our developers community for all kinds of support.

{% embed url="https://discord.gg/Z3nC9U4" %}



