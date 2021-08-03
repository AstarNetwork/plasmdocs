# DApps報酬

Dapps Rewardsに関しての説明はこちらをご覧ください。

{% page-ref page="../learn/features/dapps-reward.md" %}

## 準備

{% page-ref page="operator-trading-tutrial.md" %}

に従って、コントラクトをデプロイするところまでやってみましょう。サイドバーから _**Staking**_ を選択して以下のような状態であれば準備完了です。

![dAppsStaking Board](../.gitbook/assets/screen-shot-2020-06-11-at-16.26.00.png)

## dApps Rewards を体験する <a id="a574"></a>

dApps Rewards の大まかな流れはざっくりと以下のようになっています。

1. スマートコントラクトを選んで Staking する。\(これを Nominate といいます。\)
2. Staking 量に応じて Nominate した人\(以下、ノミネータ\)と Nominate されたスマートコントラクトのオペレータは報酬が与えられます。

![](../.gitbook/assets/sukurnshotto-2020-05-30-160230png%20%281%29%20%281%29.png)

では、実際にやってみてましょう。

### ① スマートコントラクトに Nomiante する <a id="082b"></a>

_**DappsStaking -&gt; Account actions**_ を選択します。まだ Stake していない場合、下のような画面が表示されます。ここで右上の _**+ New stake**_ と書かれたボタンを押します。

![](../.gitbook/assets/sukurnshotto-2020-05-30-160422png.png)

すると以下のような画面が現れるため、以下の4つの項目を埋めます。

* **Stash account**：誰の持っているトークンを扱うかを指定します。”**口座”**のようなものです。
* **Controller account**：どのアカウントの権限で操作するかを指定します。セキュリティ的には Stash account と Controller account は別のアカウントを使うことが好ましいです。今回はデモなので同一のアカウント\(BOB\)を使います。
* **Value bonded**：Stake に利用するトークン量を指定します。
* **Payment destination**：Rewards の振込先を指定します。

![](../.gitbook/assets/sukurnshotto-2020-05-30-160554png.png)

入力を終えたら、_**Bonding -&gt; Sign and Submit**_ を押してトランザクションを発行します。すると下のように先程指定した項目が反映された内容のカードが表示されます。

![](../.gitbook/assets/screen-shot-2020-06-11-at-16.33.28.png)

これで、トークンをロックすることに成功しました。しかし、これだけでは Nominate したことになりません。続いてカードの右側の _**Nominate**_ ボタンをクリックします。

![](../.gitbook/assets/screen-shot-2020-06-11-at-16.35.14.png)

すると、以下のようなポータルが現れます。ここでは Nominate する対象のスマートコントラクトを選ぶことができます。[前回](https://medium.com/stake-technologies/%E9%81%8A%E3%81%BC%E3%81%86-plasm-testnet-v3-%E2%91%A0-operator-trading-64323fa2d4fd)のデモでアップロードした “SAMPLE.WASM” を選びましょう。この時、コントラクトの _**canBeNominate**_ のパラメータを Yes にしているコントラクトしか選ぶことができないことに注意しましょう。

![](../.gitbook/assets/screen-shot-2020-06-11-at-22.54.43.png)

_**Nominate -&gt; Sign and Submit**_ でトランザクションを発行します。しばらくすると以下のようにカードに _**Nominating**_ という項目が現れ、先程 Nominate したスマートコントラクトが表示されます。

![](../.gitbook/assets/screen-shot-2020-06-11-at-16.38.25.png)

これで、スマートコントラクトへの Nominate が完了しました。

### ② Dapps Rewards を受け取る <a id="58bd"></a>

これはとても簡単です。待ちましょう！Dapps Rewards は **Era** と呼ばれる特定の周期おきに発行されます。NominateをEra \(E\)で行ったならば、Era \(E+1\)が終了した時点で報酬を受け取ることが可能になります。

Dustyでは、

* 1 Era = 1日
* 1 Session = 10分

となっています。

Local Node を使った場合、この Era を強制的に動かすことで待たずに報酬を貰う過程までをスキップできます！以下ではそのやり方を説明します。

サイドバーから _**Extrinsics**_ を選び、ルートユーザである ALICE から以下のトランザクションを発行します。**Sudo\(forceNewEra\(\)\)。**

![](../.gitbook/assets/screen-shot-2020-06-11-at-21.23.53.png)

このトランザクションを発行することで、一度だけ Era を強制的にすすめる事ができます。Era が更新されたかどうかは _**Chain state**_ から確認することができます。_plasmStaking_ の _forceEra\(\)_ を参照して _**ForceNew**_ であれば Era が更新されておらず、_**NotForcing**_ であれば Era が更新されています。

これで、**Claim for Nominator**タブと**Claim for Operator**タブで報酬を請求できます。**Staking**ページの**Claim for Nominator**タブから、**Claim**ボタンをクリックします。

![](../.gitbook/assets/screen-shot-2020-06-11-at-23.07.30.png)

すると、以下のモーダルが表示されます。Nominatorのアドレスと最新のEraを選択して**Claim**ボタンを押すことで報酬を受け取ることができます。

![](../.gitbook/assets/screen-shot-2020-06-11-at-22.58.13%20%281%29%20%282%29%20%282%29.png)

また、Operatorの場合も同様の操作で報酬を受け取ることができます。

以上で今回のデモを終わります！お疲れさまでした！

質問があれば、[Tech Chat](https://discord.gg/Cyjnrxv)の日本語チャネルでご質問ください。

