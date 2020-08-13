---
description: このページでは開発を行うためのプロジェクトの作成を行います。
---

# はじめの一歩

まずはじめに、オークションコントラクトを開発するためのプロジェクトディレクトリを作成します。以下のコマンドを実行してください。

```text
cargo contract new auction
cd auction
```

ここで作成された雛形\(とくにlib.rs\)に変更を加えていくことでコントラクトを開発します。lib.rsを開くと以下のようなコードが記述されています。

```text
#[ink::contract(version = "0.1.0")]
mod auction {

    ...
    
    #[ink(storage)]
    struct Auction {
        ...
    }
    
    ...
    
    impl Auction {
        #[ink(constructor)]
        fn new(&mut self, init_value: bool) {
            self.value.set(init_value);
        }
        
        ...
        
        #[ink(message)]
        fn flip(&mut self) {
            *self.value = !self.get();
        }
    } 
       
    ...
}
```

この`[ink::contract(version = "0.1.0")]`というattributeが付与されたモジュールがコントラクトの定義となります。

