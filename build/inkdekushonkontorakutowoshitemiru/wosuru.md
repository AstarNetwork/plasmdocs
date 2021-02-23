---
description: このページではink!で状態を保持できるようになること、雛形を変更してテスト実行できることを目標としています。最終的なコードはページ下部に記載しています。
---

# 最高額を保持する

`#[ink(storage)]`を利用してコントラクト内で扱う状態を宣言することができます。生成された雛形は以下のようになっているはずです。

```text
#[ink(storage)]
struct Auction {
    /// Stores a single `bool` value on the storage.
    value: storage::Value<bool>,
}
```

Auction構造体内の`value`のような、コントラクト上で扱う各状態を以降ではストレージアイテムと呼ぶことにします。

`value`のように、ジェネリック型であるValueでラップすることで、bool、u32といったRustのプリミティブ型を扱うことができます。また、プリミティブ型の他にもAccountId、BalanceといったSubstrate特有の型を使用することも可能です。サポートされている型は次のページのコードから確認することができます。

{% embed url="https://github.com/paritytech/ink/blob/master/core/src/env/types.rs" %}

オークションコントラクトでは、現在の最も高い賭け金と、その賭け金を賭けた人物\(AccountId\)を保持しておく必要があります。そこで、雛形を以下のように変更してみましょう。

```text
#[ink(storage)]
struct Auction {
    highest_bid: storage::Value<Balance>,
    highest_bidder: storage::Value<AccountId>,
}
```

ここでは、最も高い賭け金を保持する`highest_bid`とそれを賭けたアカウントを保持する`highest_bidder`を宣言しています。

「他の部分を一旦コメントアウトしてコンパイル！」としてみたくなるところですが、ちょっと待ってください。

* ink!コントラクトは1つ以上の`#[ink(constructor)]`と1つ以上の`#[ink(message)]`を含む必要があります！

そのため、コンパイル・テストを行うためにはこれらを記述しなければなりません。

雛形で生成されたコードの`#[ink(constructor)]`が現れる部分を見ていきましょう。ここでは、`set`関数を用いてstorageで宣言された`value`に初期値を与えています。

```text
impl Auction {
    /// Constructor that initializes the `bool` value to the given `init_value`.
    #[ink(constructor)]
    fn new(&mut self, init_value: bool) {
        self.value.set(init_value);
    }

    ...
}
```

この部分を今回の目的に沿うように変更したいわけですが、ここで、覚えておくべき注意点があります。

* Valueは必ず初期化をしなければいけません！

もし初期化をしなかった場合でも、コンパイルは正常に通りますが、ストレージにアクセスしようとすると失敗します。なので、テストコードにストレージアイテムの初期化のチェックを含めるのを忘れないようにしましょう。

通常は、初期化処理は`#[ink(constructor)]`が付与された関数\(以降constructor\)内で行います。このconstructorはコントラクトの作成時に一度だけ実行されます。

宣言済みの2つのストレージアイテムを初期化してみましょう。`set`関数で初期値を与えることができます。

```text
#[ink(constructor)]
fn new(&mut self) {
    self.highest_bid.set(0);
    self.highest_bidder.set(AccountId::from([0x0; 32]));
}
```

次に、`#[ink(message)]`の部分を変更していきます。`#[ink(message)]`を用いることで、コントラクト作成後に呼び出し可能な関数を定義することができます。あくまでRustコードなので、`#[ink(message)]`を付与しない通常の関数も定義することができますが、それらの関数を外部から呼び出すことはできません。

ストレージアイテムの値を取得する関数を定義してみましょう。例えば、以下のような関数が定義できます。

```text
#[ink(message)]
fn get_highest_bid(&self) -> Balance {
    *self.highest_bid
}

#[ink(message)]
fn get_highest_bidder(&self) -> AccountId {
    *self.highest_bidder
}
```

ここまでの実装で、

* 2つのストレージアイテム`highest_bid`と`highest_bidder`の初期化
* `highest_bid`と`highest_bidder`の現在の値の取得

が可能になりました。コードに変更を加えたので、テストコードを記述して実際にテストをしてみましょう。Auctionの初期化が正しく行われているかを確認するために、以下のコードを記述してください。

```text
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn initialize_auction() {
        let auction = Auction::new();
        assert_eq!(auction.get_highest_bid(), 0);
        assert_eq!(
            auction.get_highest_bidder(),
            AccountId::from([0x0; 32])
        );
    }
}
```

`initialize_auction` では、`assert_eq!` を用いて各関数の返り値が正しいことを検査しています。

雛形のコードに含まれていた不要な部分を削除すると、ソースコードは最終的に以下のようになります。

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
    }

    #[cfg(test)]
    mod tests {
        use super::*;
        #[test]
        fn initialize_auction() {
            let auction = Auction::new();
            assert_eq!(auction.get_highest_bid(), 0);
            assert_eq!(
                auction.get_highest_bidder(),
                AccountId::from([0x0; 32])
            );
        }
    }
}
```

最後に、正しくテストをパスできることを以下のコマンドで確認しましょう。

```text
cargo +nightly test
```

