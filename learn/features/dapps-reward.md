# Dapps報酬

{% embed url="https://medium.com/stake-technologies/dapps-%E9%96%8B%E7%99%BA%E8%80%85%E3%81%8C%E3%83%9E%E3%83%8D%E3%82%BF%E3%82%A4%E3%82%BA%E3%81%99%E3%82%8B%E3%81%9F%E3%82%81%E3%81%AE%E3%83%96%E3%83%AD%E3%83%83%E3%82%AF%E7%94%9F%E6%88%90%E5%A0%B1%E9%85%AC%E3%81%A8%E3%81%AF-1062a0925909" %}

Dapps Reward はスマートコントラクトの開発者または管理者に継続的な報酬を与える仕組みです。[Plasm Network](https://www.plasmnet.io/) の Staking 報酬の50% は [Plasm Network](https://www.plasmnet.io/) の価値を向上させたアプリケーション作成者に当てられます。[Plasm Network](https://www.plasmnet.io/) ではスマートコントラクトに対してスマートコントラクトの管理者を割り当てることができ、この管理者のことを "Operator" と呼びます。ユーザはスマートコントラクトに対しても Staking をすることができます。この行為を Nominate と呼び、それを行う人を Dapps Nominator と呼びます。下図のように、多くの Nominate を受けたスマートコントラクトの Operator は新たに発行されたPLMトークンをチェーンから受け取ることができます。

![](../../.gitbook/assets/sukurnshotto-2020-05-30-122939png.png)

この報酬を Operator と Nominator にそれぞれどのように分配するかを定義していきます。次の変数を定義します。

*  $$Rewards_{nominate}$$ : Nominator に割り振られた報酬の合計
*  $$Rewards_{contract}$$ : スマートコントラクトに割り振られた報酬の合計
* $$Rewards_{nominate_{i,j}}$$ : i 番目のスマートコントラクトに対する j 番目の Nominate で得られる報酬
* $$Rewards_{contract_i}$$ : i 番目のスマートコントラクトの Operator が得られる報酬
* $$n$$ : スマートコントラクトの数
* $$m_i$$ : i 番目のに対する Nominate の数
* $$stake_{i,j}$$ : i 番目のスマートコントラクトに対する j 番目の Nominate により Stake したトークンの量

この時、この Stake について $$Nominate_{i,j}$$ により以下の報酬が得られます。

$$
Rewards_{nominate_{i,j}}=Rewards_{nominate}\times\frac{stake_{i,j}}{\sum_i^n\sum_j^{m_i}stake_{i,j}}
$$

Nominator は選んだスマートコントラクトに関わらずスマートコントラクトに対するStake総量のうち自信のStake量が占める割合に比例した報酬を得ることができます。Stake を受けた contract\_i の Operator は以下の報酬が得られます。

$$
Rewards_{contract_i}=Rewards_{contract} \times \frac{\sum_{j}^{m_i}stake_{i,j}}{\sum_i^n\sum_j^{m_i}stake_{i,j}}
$$

一方、Operator はスマートコントラクトに対するStake総量のうち自身が所有するスマートコントラクトのStake量が占める割合に比例した報酬を得ることができます。これにより、Nominator は単純にトークンの価値を向上させると思われるスマートコントラクトに対して Stake するインセンティブが発生します。また、Operator は自信が管理するスマートコントラクトに Stake を受けることで半永続的に報酬を受取ることができます。これはチェーン上のアプリケーション開発者\(管理者\)のマネタイズが難しい問題に対する革新的な解決策となることを期待しています。

{% hint style="info" %}
Operator/Nominator が報酬を実際に受取るには一定の期間を待つ必要があります。
{% endhint %}

質問があれば、[Tech Chat](https://discord.gg/Cyjnrxv)の日本語チャネルでご質問ください。

