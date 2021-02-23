---
description: このページではink!で定義したストレージを更新できるようになることを目標としています。最終的なコードはページ下部に記載しています。
---

# 「賭け」の処理を追加する

このままでは、オークションの賭け金を変更できないので、賭けを行う関数を定義していきます。

まずはじめに、\(冗長かもしれませんが\)setterを定義しましょう。これらの関数は外部から叩けないように`#[ink(message)]`を付与していないこと、値を変更するために引数の型が`&mut self`になっていることを確認してください。

```text
impl Auction {
    ...
    fn set_highest_bid(&mut self, new_bid: Balance) {
        self.highest_bid.set(new_bid)
    }

    fn set_highest_bidder(&mut self, new_bidder: AccountId) {
        self.highest_bidder.set(new_bidder)
    }
    ...
}
```

コンパイル時に以下のようなエラーが出力される場合は、`&mut self`が`&self`になっていないか確認をしてください。

```text
error[E0596]: cannot borrow `self.highest_bid` as mutable, as it is behind a `&` reference
```

これらのsetterを使用して、賭けの処理を行う`bid`関数を作成しましょう。ここでは、賭けた人物と賭けた値を引数にとり、現在最も高い金額よりも高い場合にストレージアイテムを更新することにします。また、値が更新された場合にはtrue、そうでない場合にはfalseを返すようにしてみましょう。例えば、以下のようなコードが記述できます。

```text
#[ink(message)]
fn bid(&mut self, who: AccountId, value: Balance) -> bool {
    if self.get_highest_bid() < value {
        self.set_highest_bid(value);
        self.set_highest_bidder(who);
        true
    } else {
        false
    }
}
```

messageを追加したので、テストコードも追加しましょう。

```text
#[test]
fn bid_test() {
    let mut auction = Auction::new();
    let alice = AccountId::from([0x1; 32]);
    let bob = AccountId::from([0x2; 32]);

    assert_eq!(auction.bid(alice, 100), true);
    assert_eq!(auction.get_highest_bid(), 100);
    assert_eq!(auction.get_highest_bidder(), alice);

    assert_eq!(auction.bid(bob, 50), false);
    assert_eq!(auction.get_highest_bid(), 100);
    assert_eq!(auction.get_highest_bidder(), alice);
}
```

ここまでのコードは以下のようになります。手元でテストを実行してみてください。

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
    }

    impl Auction {
        #[ink(constructor)]
        fn new(&mut self) {
            self.highest_bid.set(0);
            self.highest_bidder.set(AccountId::from([0x0; 32]));
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

        #[ink(message)]
        fn bid(&mut self, who: AccountId, value: Balance) -> bool {
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
        #[test]
        fn initialize_auction() {
            let auction = Auction::new();
            assert_eq!(auction.get_highest_bid(), 0);
            assert_eq!(auction.get_highest_bidder(), AccountId::from([0x0; 32]));
        }

        #[test]
        fn bid_test() {
            let mut auction = Auction::new();
            let alice = AccountId::from([0x1; 32]);
            let bob = AccountId::from([0x2; 32]);

            assert_eq!(auction.bid(alice, 100), true);
            assert_eq!(auction.get_highest_bid(), 100);
            assert_eq!(auction.get_highest_bidder(), alice);

            assert_eq!(auction.bid(bob, 50), false);
            assert_eq!(auction.get_highest_bid(), 100);
            assert_eq!(auction.get_highest_bidder(), alice);
        }
    }
}
```

