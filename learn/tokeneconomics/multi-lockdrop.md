# ロックドロップ

{% hint style="info" %}
現在Plasm Networkのロックドロップは実施しておりません。第三回ロックドロップのアナウンスをお待ち下さい。開催時期はPolkadotの開発によるため、未定です。
{% endhint %}

![](../../.gitbook/assets/undraw_collecting_fjjl.png)

## はじめに

ロックドロップは、法定通貨や暗号資産ではなく機会費用を担保にした新しい低リスクの経済インセンティブメカニズムです。Plasm Networkでは、この仕組みを利用してトークンを発行しています。ここでは、Plasm Networkのトークン発行メカニズムについて説明します。Lockdropは [Edgeware](https://edgewa.re/)が最初に考案したもので、Plasm Networkでの実装はこれを拡張したものです。Plasm Networkで使用されているネイティブトークンは PLMと発音します。PLMは小数点以下15位までで計算し、それ以下の数字は切り捨てます。PLMの役割については、PLMトークンのトークンエコノミクスの項を参照してください。

**NOTE**: 通貨単位の変更後、小数点以下の桁数は15桁から18桁になります。

{% page-ref page="staking-liquidity-and-inflation-model.md" %}

## ロックドロップ概要

最初に発行されたロックドロップは、Ethereumの機会費用を使用しました。例では、ロックされたトークンがETHであることを前提とします。ロックドロップは、TimeLockに対応しているチェーンであれば、どのチェーンでも実装できるアルゴリズムです。下図は、Plasm Network上でロックドロップがどのように動作するかを示しています。

![Keep in mind that you have to pay the gas fee.](../../.gitbook/assets/screen-shot-2020-08-25-at-11.56.15.png)

ロックドロップの流れ：

1. EthereumのトークンホルダーがETHを送信し、Ethereumブロックチェーン上にあるLockContractにトランザクションとしてロックの期間を決定します。
2. `total locked ETH × Lock bonus per duration × α` で計算されたPLMの数が、参加者ごとにPlasm Networkのジェネシスブロックに記録される。
3. Plasmチームは、ジェネシスブロックから`total issued amount × 15%`のPlasmTokensをミントします。
4. トークンホルダーが指定したロック期間が経過すると、全てのETHが参加者に返却されます。

前提として、Ethereumトークン保有者の機会費用は、ロックされているトークンの数とロックされている期間に比例する。PLMはそれらの機会費用を担保に価値を生み出すことができる。最終的なトークンの供給量は決定されません。これにより、生成後のロックドロップから発行されたトークンの公平性が確保されます。最初のロックドロップからミントされたトークン全体の15%が手数料としてPlasmチームに行きます。健全なトークン供給を維持するために、複数回のロックドロップが行われます。

### Multi−Lockdropとは？

Multi-Lockdrop は前述した Lockdrop を複数回行うための仕組みです。Plasm Network では 3度の Lockdrop を行います。Plasm Network ではトークンの総発行量がジェネシスブロックで決まりません。3度の Lockdrop によりその都度トークンが発行され、後述する "Staking" の利回りとしてもトークンが発行され続けます。

{% page-ref page="../features/dapps-reward.md" %}

Lockdrop を複数回に分ける理由は2つあります。

1つ目は先行者利益が肥大化することを避けるためです。1度の Lockdrop で全てのトークンを分配すると、仮に最初の Lockdrop の参加者が少なかった場合にトークンの大半を保有するホルダーが現れるかもしれません。そして、そのようなことが発生した後にロールバックを行うことはチェーンの信頼性を損ないます。ブロックチェーンでは予め提示したルールに基づいてこのような問題を避ける施策を打つ必要があります。

2つ目は Plasm Network が安全にスケール/分権化するために序盤はある程度管理可能で実験的な振る舞いが出来るようにするためです。ブロックチェーンの強固なセキュリティシステムは大量のノード参加者と広く分散化されたトークンホルダーが存在することで成り立っています。起動直後からこのセキュリティを担保することは極めて難しいです。序盤は信頼できる機関がある程度管理可能な状態であるほうが好ましいでしょう。そこで 3 度の Lockdrop を設けることにより、全てのトークン発行前に不用意なトークン価値の高騰を抑えることで管理コストを下げます。私達は最終的に Plasm Network を完全なパブリックチェーンとすることを前提として安定して動作するまでの準備期間を設けるために複数回の Lockdrop を行います。

また、Plasm Network では3回のLockdrop についてそれぞれ以下のトークンで Lockdrop が可能になります。

* 1st: ETH 16,783 ETH locked
* 2nd: ETH 137,253 ETH locked
* 3rd: DOT or KSM（ネットワークのオークション仕様による）

### **Lockdropのアルゴリズム**

初めに最初の Lockdrop で配布される PLM の総量を以下のように定義します。

![](../../.gitbook/assets/sukurnshotto-2020-05-29-162825png.png)

これらを発行比率\(IssueRatio\)に応じて Lockdrop に参加したユーザに対して分配します。**IssueRatio** は

* **DollarRate\_token：**ロックしたトークンの総量をPLMトークン発行時のドルとロックしたトークンとの変換レート
* ロックした日数に 1.0005 を日数\(Days\)乗したものを掛けたものに近似されます。

> ここで 1.0005 は Polkadot の金利を参考にしました。Polkadot のデフォルト最大平均年利は 20%と定義されています。これを複利込みの日利に直した際の近似解が 0.05% となります。

ユーザ実際にはロックする期間を次の4種類（3回目のLockdropのみ5種類）から選ぶことができます。ロック期間に応じて ロックしたトークンの価値をドル換算した値に以下の**LockBonus**を掛けたものが **IssueRatio** となります。

![](../../.gitbook/assets/sukurnshotto-2020-05-29-163405png.png)

上記をもとに **IsseRatio** を以下のような式で定義されます.ここで

* **Locked\_token**： Lockdrop の対象の token を Lock した量
* **DollarRate{token}** ：1token のドル建て価格
* **LockBonus\_day**： days 日間ロックしたときの**LockBonus**を示します

![](../../.gitbook/assets/sukurnshotto-2020-05-29-163659png.png)

算出された **IssueRatio** を元に、配られるトークン数が決定します。トークン配布量の決定アルゴリズムは以下のようになります。

* **n** : Lockdrop を行ったユーザ数
* **IssueRatio\_i**：ユーザ iの IssueRatio

総発行トークンのうち15%\(17/20\)はPlasm Network運営チームに移譲されます。この時、ユーザ **i** の 得られる**PLM\_i**は以下になります。

![](../../.gitbook/assets/sukurnshotto-2020-05-29-163929png.png)

つまり、全体の **IssueRatio** のうち自分の **IssueRatio** が占める割合だけPLMが分配されます。ここで、IssueRation の総和である **TotalIssueRatio** を定義します。

![](../../.gitbook/assets/sukurnshotto-2020-05-29-164050png.png)

また、1回目の Lockdrop における単位 **IssueRatio**あたりのPLM発行量をここで **α\_1**とおきます。これは2回目以降の Lockdrop における PLM 発行量を決めるための重要な値となります。

![](../../.gitbook/assets/sukurnshotto-2020-05-29-164144png.png)

2回目、3回目のLockdropにおける単位 **issueRatio**あたりの PLM 発行数を α\_2, α\_3と以下の等式を満たすように定義します。

![](../../.gitbook/assets/sukurnshotto-2020-05-29-164258png.png)

上記から2回目、3回目のユーザ i に配られるPLMの量は以下になります。

![](../../.gitbook/assets/sukurnshotto-2020-05-29-164335png.png)

こうすることで、2回目以降の Lockdrop のおいてユーザは単に **IssueRatio** に比例した量のトークンを得ることができます。これにより、2回目以降に Lockdrop を行うユーザが非常に増えた場合、ユーザが取得できる PLM の量が全体の割合に対して過度に少なくなってしまう問題を解決します。

![](https://user-images.githubusercontent.com/6259384/75602454-ac7d9a00-5b08-11ea-80a1-d3e697f1c776.png)

質問があれば、[Tech Chat](https://discord.gg/Cyjnrxv)の日本語チャネルでご質問ください。

