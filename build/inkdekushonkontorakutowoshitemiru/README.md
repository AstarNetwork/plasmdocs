---
description: >-
  このページでは、オークションコントラクトの開発を通して、ink!を利用した開発を個人で調べつつ行えるようになることを目標としています。手順ごとにいくつかのサブページに分かれています。
---

# ink!でオークションコントラクトを開発してみる

ここでは、実際にコントラクトを実装することでink!での開発を学んでいきます。

題材として、単純なオークションを行うコントラクトの開発をします。最終的に作るものは、オークションに参加する人に予め定額を割り当てておき、その中から賭け金を宣言していくような簡単なものです。オークションの終了時には、最高額を提示したアカウントから開催者に賭け金の移動が行われます。

早速開発に移りましょう。いくつかのサブページに分けて解説をしているので、順番に読んでみてください。

{% page-ref page="hajimeno.md" %}

{% page-ref page="wosuru.md" %}

{% page-ref page="kenowosuru.md" %}

{% page-ref page="akauntogotoniwosuru.md" %}

{% page-ref page="kushonwosaseru.md" %}

これらのページを読み終えたとき、最終的なink!のソースコードは以下のようになります。

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



