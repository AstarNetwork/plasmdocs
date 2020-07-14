# コンセンサス

![](../.gitbook/assets/sukurnshotto-2020-06-29-175510png.png)

Plasm Network はセキュリティの維持のために段階的に合意形成アルゴリズムと報酬設計を変更します。具体的には最初はコミュニティによって選定された Validator のみで運営する Proof of Authority の形式をとります。最終的に Polkadot の リレーチェーン でも採用されている NPoS に移行します。

### Proof Of Authority

Proof of Authority はコミュニティによって選定された Validator のみで運営する合意形成アルゴリズムです。パブリックブロックチェーンはローンチ直後に信頼できるバリデータを十分用意できず脆弱性を持つ可能性があります。そのため、十分なトークンホルダーの分布と潜在的バリデータの存在が確認できるまでは PoA による運営を行います。この時のバリデータにも PoS の時と同様に指定されたパラメータに従って報酬が支払われます。

### Nominated Proof of Staking

Plasm Network は最終的に Polkadot の RelayChain で採用されているコンセンサスアルゴリズムを使います。このアルゴリズムは大きく3ステップに分かれています。

1. Nominator は Validator を選出する。 
2. Validator はトランザクションを検証しブロックを生成する。
3. 配布されたブロックをファイナライズする。

また、初期の Validator ノードを限定することで十分な Validator がいない状態において悪意のある Validator が闊歩するリスクを減らすことができます。ブロックの生成報酬は Validator とその支援者である Nominator に分配されます。また、Plasm Network の価値向上の貢献者にもこの報酬は支払われます。

質問があれば、[Tech Chat](https://discord.gg/Cyjnrxv)の日本語チャネルでご質問ください。

**参照リンク**

{% embed url="https://wiki.polkadot.network/docs/en/learn-staking" %}

