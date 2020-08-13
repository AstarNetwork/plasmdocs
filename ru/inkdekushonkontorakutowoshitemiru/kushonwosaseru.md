---
description: このページでは関数を呼び出したアカウントを利用した処理を行うことを目標としています。最終的なコードはページ下部に記載しています。
---

# オークションを終了させる

オークションを終わらせて賭け金を移動させることができるようにしましょう。そのためにまず、賭け金を受け取るアカウントとオークションが開かれているかどうかを保持するストレージアイテムを追加します。

```text
#[ink(storage)]
struct Auction {
    highest_bid: storage::Value<Balance>,
    highest_bidder: storage::Value<AccountId>,
    balances: storage::HashMap<AccountId, Balance>,
    default_balance: storage::Value<Balance>,
    owner: storage::Value<AccountId>,
    is_open: storage::Value<bool>,
}
```

次に、今までと同様constructorで初期値を設定します。

```text
#[ink(constructor)]
fn new(&mut self, default_balance: Balance) {
    let owner = self.env().caller();
    self.highest_bid.set(0);
    self.highest_bidder.set(AccountId::from([0x0; 32]));
    self.default_balance.set(default_balance);
    self.owner.set(owner);
    self.is_open.set(true);
}
```

引数に直接アカウントをとるのではなく、`caller`関数を呼び出すことでアカウントを取得している点がこれまでと異なります。`self.env()`はEnvAccessという型の値を返しており、コントラクトで扱ういくつかの値にアクセスすることができます。詳細は以下のページのコードで定義されています。

{% embed url="https://github.com/paritytech/ink/blob/master/lang/src/env\_access.rs" %}

最後に、オークションを終了して賭け金を受け渡す`finish`関数を定義します。

```text
#[ink(message)]
fn finish(&mut self) -> bool {
    if !*self.is_open {
        return false;
    }

    self.is_open.set(false);

    let owner = self.get_owner();
    let highest_bid = self.get_highest_bid();
    let highest_bidder = self.get_highest_bidder();
    let owner_balance = self.balance_of(owner);
    let highest_bidder_balance = self.balance_of(highest_bidder);

    self.set_balance(owner, owner_balance + highest_bid);
    self.set_balance(highest_bidder, highest_bidder_balance - highest_bid);
    true
}
```

`is_open`をfalseに変更し、現在の最高額に応じて`balances`を更新しています。また、既に終了している場合にはこの処理は行いません。

`bid`関数にも同様に小さな修正を加えます。オークションが終了している場合には、これ以上最高額を上書きすることはできません。

```text
#[ink(message)]
fn bid(&mut self, who: AccountId, value: Balance) -> bool {
    if !*self.is_open {
        return false;
    }

    if self.balance_of(who) < value {
        return false;
    }

    if self.get_highest_bid() < value {
        self.set_highest_bid(value);
        self.set_highest_bidder(who);
        true
    } else {
        false
    }
}
```

最後にテストを追加したコードが以下になります。テストが通ることを確認してみてください。

```text
#![cfg_attr(not(feature = "std"), no_std)]

use ink_lang as ink;

#[ink::contract(version = "0.1.0")]
mod auction {
    use ink_core::storage;

    #[ink(storage)]
    struct Auction {
        highest_bid: storage::Value<Balance>,
        highest_bidder: storage::Value<AccountId>,
        balances: storage::HashMap<AccountId, Balance>,
        default_balance: storage::Value<Balance>,
        owner: storage::Value<AccountId>,
        is_open: storage::Value<bool>,
    }

    impl Auction {
        #[ink(constructor)]
        fn new(&mut self, default_balance: Balance) {
            let owner = self.env().caller();
            self.highest_bid.set(0);
            self.highest_bidder.set(AccountId::from([0x0; 32]));
            self.default_balance.set(default_balance);
            self.owner.set(owner);
            self.is_open.set(true);
        }

        #[ink(message)]
        fn get_highest_bid(&self) -> Balance {
            *self.highest_bid
        }

        #[ink(message)]
        fn get_highest_bidder(&self) -> AccountId {
            *self.highest_bidder
        }

        #[ink(message)]
        fn get_owner(&self) -> AccountId {
            *self.owner
        }

        fn set_highest_bid(&mut self, new_bid: Balance) {
            self.highest_bid.set(new_bid)
        }

        fn set_highest_bidder(&mut self, new_bidder: AccountId) {
            self.highest_bidder.set(new_bidder)
        }

        fn set_balance(&mut self, who: AccountId, value: Balance) {
            self.balances.insert(who, value);
        }

        #[ink(message)]
        fn balance_of(&mut self, who: AccountId) -> Balance {
            match self.balances.get(&who) {
                Some(value) => *value,
                None => {
                    self.set_balance(who, *self.default_balance);
                    *self.balances.get(&who).unwrap()
                }
            }
        }

        #[ink(message)]
        fn bid(&mut self, who: AccountId, value: Balance) -> bool {
            if !*self.is_open {
                return false;
            }

            if self.balance_of(who) < value {
                return false;
            }

            if self.get_highest_bid() < value {
                self.set_highest_bid(value);
                self.set_highest_bidder(who);
                true
            } else {
                false
            }
        }

        #[ink(message)]
        fn finish(&mut self) -> bool {
            if !*self.is_open {
                return false;
            }

            self.is_open.set(false);

            let owner = self.get_owner();
            let highest_bid = self.get_highest_bid();
            let highest_bidder = self.get_highest_bidder();
            let owner_balance = self.balance_of(owner);
            let highest_bidder_balance = self.balance_of(highest_bidder);

            self.set_balance(owner, owner_balance + highest_bid);
            self.set_balance(highest_bidder, highest_bidder_balance - highest_bid);
            true
        }
    }

    #[cfg(test)]
    mod tests {
        use super::*;
        use ink_core::env;

        #[test]
        fn initialize_auction() {
            let default_balance = 100;
            let auction = Auction::new(default_balance);
            assert_eq!(auction.get_highest_bid(), 0);
            assert_eq!(auction.get_highest_bidder(), AccountId::from([0x0; 32]));
        }

        #[test]
        fn bid_test() {
            let default_balance = 100;
            let mut auction = Auction::new(default_balance);

            let accounts =
                env::test::default_accounts::<env::DefaultEnvTypes>().expect("Cannot get accounts");

            assert_eq!(auction.bid(accounts.alice, 100), true);
            assert_eq!(auction.get_highest_bid(), 100);
            assert_eq!(auction.get_highest_bidder(), accounts.alice);

            assert_eq!(auction.bid(accounts.bob, 50), false);
            assert_eq!(auction.get_highest_bid(), 100);
            assert_eq!(auction.get_highest_bidder(), accounts.alice);

            assert_eq!(auction.bid(accounts.bob, 200), false);
            assert_eq!(auction.get_highest_bid(), 100);
            assert_eq!(auction.get_highest_bidder(), accounts.alice);
        }

        #[test]
        fn finish_test() {
            let default_balance = 100;
            let mut auction = Auction::new(default_balance);

            let accounts =
                env::test::default_accounts::<env::DefaultEnvTypes>().expect("Cannot get accounts");

            assert_eq!(auction.get_owner(), accounts.alice);
            assert_eq!(auction.bid(accounts.bob, 50), true);
            assert_eq!(auction.finish(), true);
            assert_eq!(auction.balance_of(accounts.alice), 150);
            assert_eq!(auction.balance_of(accounts.bob), 50);
            assert_eq!(auction.bid(accounts.charlie, 100), false);
            assert_eq!(auction.finish(), false);
        }
    }
}

```

