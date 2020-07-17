# テスト

コントラクトコードを更新したら、以下のコマンドでテストを実行することができます。

```text
cargo +nightly test
```

試しに、flipperでテストを実行してみましょう。変更を加えていなければ、以下のような結果が返ってきます。

```text
...

running 2 tests
test flipper::tests::it_works ... ok
test flipper::tests::default_works ... ok

test result: ok. 2 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out
```

ここでは2つのテスト\(it\_worksとdefault\_works\)が実行されていますが、これらのテストは`lib.rs`の下部に記述されています。

```text
/// Unit tests in Rust are normally defined within such a `#[cfg(test)]`
/// module and test functions are marked with a `#[test]` attribute.
/// The below code is technically just normal Rust code.
#[cfg(test)]
mod tests {
    /// Imports all the definitions from the outer scope so we can use them here.
        use super::*;

    /// We test if the default constructor does its job.
    #[test]
    fn default_works() {
        // Note that even though we defined our `#[ink(constructor)]`
        // above as `&mut self` functions that return nothing we can call
        // them in test code as if they were normal Rust constructors
        // that take no `self` argument but return `Self`.
        let flipper = Flipper::default();
        assert_eq!(flipper.get(), false);
    }

    /// We test a simple use case of our contract.
    #[test]
    fn it_works() {
        let mut flipper = Flipper::new(false);
        assert_eq!(flipper.get(), false);
        flipper.flip();
        assert_eq!(flipper.get(), true);
    }
}
```

開発時には、ここにテストコードの追加・変更を行うことで「コード変更」→「テスト」を繰り返していきます。

