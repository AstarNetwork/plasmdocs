---
description: >-
  このページではink!でKey-Valueストレージを扱うこと、test
  apiで定義された関数を使用することができるようになることを目標としています。最終的なコードはページ下部に記載しています。
---

# アカウントごとに残高を記録する

さて、この`bid`関数は現状では残高が一切考慮されていません。そこで、独自の残高を管理する`balances`とその初期値`default_balance`を追加することにします。今回は全員一律に`default_balance`を保有していることにしましょう。

```text
#[ink(storage)]
struct Auction {
    highest_bid: storage::Value<Balance>,
    highest_bidder: storage::Value<AccountId>,
    balances: storage::HashMap<AccountId, Balance>,
    default_balance: storage::Value<Balance>,
}
```

ink!ではKey-Valueなストレージとして、HashMapを利用することができます。型パラメータの1つ目がkeyの型で2つ目がvalueの型になります。ここでは、各アカウントに対して残高を定義したいのでValueではなくHashMapを利用するのが適していそうです。

HashMapは`insert`関数で値をセットすることができます。balancesの各要素のsetterを定義してみましょう。

```text
fn set_balance(&mut self, who: AccountId, value: Balance) {
    self.balances.insert(who, value);
}
```

`default_balance`は以下のようにしてconstructorの引数として受け取り、セットすることにします。

```text
#[ink(constructor)]
fn new(&mut self, default_balance: Balance) {
    self.highest_bid.set(0);
    self.highest_bidder.set(AccountId::from([0x0; 32]));
    self.default_balance.set(default_balance);
}
```

次に指定したアカウントの残高を返す関数を定義しましょう。

```text
fn balance_of(&mut self, who: AccountId) -> Balance {
    match self.balances.get(&who) {
        Some(value) => *value,
        None => {
            self.set_balance(who, *self.default_balance);
            *self.balances.get(&who).unwrap()
        }
    }
}
```

ここでは、HashMapの`get`関数はOption型を返すのでパターンマッチで値を取り出し、未定義の場合は`default_balance`をセットするようにしています。

`bid`関数も修正しましょう。残高よりも高い値を賭けることはできないようにします。

```text
#[ink(message)]
fn bid(&mut self, who: AccountId, value: Balance) -> bool {
    if self.balance_of(who) < value {
        return false
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

ロジックを変更したので、テストコードにも変更を加えましょう。`bid_test`関数を以下のように変更してみました。

```text
#[cfg(test)]
mod tests {
    use super::*;
    use ink_core::env;

    ...

    #[test]
    fn bid_test() {
        let default_balance = 100;
        let mut auction = Auction::new(default_balance);

        let accounts = env::test::default_accounts::<env::DefaultEnvTypes>()
            .expect("Cannot get accounts");

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
}
```

指定した`default_balance`よりも大きな値を賭けた場合に、最高額が更新されないことを追加で確認しています。また、新たにテストコード内で`ink_core::env::test::default_accounts`を利用しています。ink!がテスト用に予め定義してくれているアカウントを利用することができます。

default\_accountsを含むテストAPIが以下のページのコードに記述されているので、詳細やその他の関数はこちらを確認してみてください。

{% embed url="https://github.com/paritytech/ink/blob/master/core/src/env/engine/off\_chain/test\_api.rs" %}

ここまでのコードは以下のようになっています。

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
    }

    impl Auction {
        #[ink(constructor)]
        fn new(&mut self, default_balance: Balance) {
            self.highest_bid.set(0);
            self.highest_bidder.set(AccountId::from([0x0; 32]));
            self.default_balance.set(default_balance);
        }

        #[ink(message)]
        fn get_highest_bid(&self) -> Balance {
            *self.highest_bid
        }

        #[ink(message)]
        fn get_highest_bidder(&self) -> AccountId {
            *self.highest_bidder
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
            if self.balance_of(who) < value {
                return false
            }

            if self.get_highest_bid() < value {
                self.set_highest_bid(value);
                self.set_highest_bidder(who);
                true
            } else {
                false
            }
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

            let accounts = env::test::default_accounts::<env::DefaultEnvTypes>()
                .expect("Cannot get accounts");

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
    }
}
```

