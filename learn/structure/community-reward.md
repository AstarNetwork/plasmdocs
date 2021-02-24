# コミュニティ報酬

コミュニティ報酬はPlasm Networkに貢献してくれたコミュニティメンバーにインセンティブを与えるためのものです。ステークスの仕組みを利用し、一定のメカニズムを通して、貢献者は報酬を得ることができます。

![\*&#x8A73;&#x7D30;&#x306A;&#x6570;&#x5024;&#x3001;&#x6BD4;&#x7387;&#x306F;&#x672A;&#x5B9A;&#x3067;&#x3059;](https://gblobscdn.gitbook.com/assets%2F-M8GVK5H7hOsGnYqg-7q%2F-MEVhuEXH_ob7auotAQh%2F-MEWBq6RtHGYzqoV77n0%2FScreen%20Shot%202020-08-11%20at%2018.33.49.png?alt=media&token=f9e667a5-ccc3-45a7-aada-ab158f91b67e)

### 概要 <a id="overview"></a>

コミュニティ報酬の構造はとてもシンプルです。

1. 開発者がスマートコントラクト\(アプリケーション\)を作成し、Plasm Network上にデプロイする
2. PLM（テストネットでは PLD）ホルダーは、Plasm Networkに貢献していると思うスマートコントラクトにトークンをステーキングする
3. どちらもスマートコントラクトのパフォーマンスに応じて報酬を得る。

さらに詳しく見てみましょう。

### コントラクトのデプロイ方法 <a id="how-to-deploy-your-contract"></a>

開発者はスマートコントラクトをデプロイする必要があります。デプロイ方法は以下のページをご覧ください。

{% page-ref page="../../build/operator-trading-tutrial.md" %}

デプロイ完了後、コミュニティ報酬のページにて、状況を確認できます。

### ステーキング方法 <a id="how-to-nominate-your-contract"></a>

次はステーキングです。詳細は以下をご覧ください。

{% page-ref page="../../build/dapps-rewards-tutrial.md" %}

そのほかにも、ステーキングのコミュニティ報酬ページでは、ステークスボリュームの状況やランキングを確認することができます

​[https://dusty.plasmnet.io](https://dusty.plasmnet.io/#/accounts)​

![](https://gblobscdn.gitbook.com/assets%2F-M8GVK5H7hOsGnYqg-7q%2F-MEQ7wEnMGsqh5gDfY0r%2F-MEQ83B6c9XW4j5kBGqF%2FScreen%20Shot%202020-08-11%20at%2010.29.40.png?alt=media&token=7420eba9-d25b-40d5-8f18-022fc57d0029)

### 報酬の獲得方法 <a id="how-to-get-rewards"></a>

PLMホルダーは、Plasm Networkの価値向上に貢献していると思うアプリ\(スマートコントラクト\)にトークンをステーキングします。それにより、ステーキングした人と、開発者（スマートコントラクト作成者）は報酬を得ることができます。

詳細は以下をご覧ください。

{% page-ref page="../../build/dapps-rewards-tutrial.md" %}

次に、報酬の計算方法を見ていきましょう。発展的な内容を含んでいるため、飛ばしていただいても構いません。

### 計算方法 <a id="rewards-calculation"></a>

{% hint style="info" %}
複雑な内容および計算を含んでいます。関心がある方のみご覧ください。
{% endhint %}

The target inflation rate of the maximum token supply is $$I ≤ I_0 = 2.5$$per a year.I\_0I0​ is the minimum token supply that should be paid to the block validators to ensure a sufficient number of validators \(We assume the sufficient number of validators is 100\). Validator compensation per each Era is strictly defined as the following.

First, we define the meaning of each variable.

* $$​TotalForValidatorRewards$$ is the total amount of compensation paid for the validator.
* ​ $$TotalForCommunityRewards$$ is the total amount of compensation paid for the community contributors.
* $$​TotalAmountOfIssue$$ is the total number of PLM tokens issued by Plasm Network.
* $$​I_0$$ ​ is the minimum token supply that should be paid to the validators to ensure a sufficient number of nodes.
* ​ $$EraDuration$$ is the length of the duration of each Era.
* $$​NumberOfValidators$$ is the actual number of validators in the network.
* $$TargetNumber$$ is 100 that is the sufficient number of validators on Plasm Network.

If $$TargetNumber$$ &lt; $$NumberOfValidators$$ :

$$
TotalForValidatorRewards = TotalAmoutOfIssue \times I_0\% \times \frac{EraDuration}{1 year}
$$

Otherwise:

$$
TotalForValidatorRewards = TotalAmoutOfIssue \times I_0\% \times \frac{EraDuration}{1 year}
$$

The amount of tokens allocated to the community members \(project owners\) is equal to the total amount of tokens allocated to the validator.

$$
TotalForCommunityRewards = TotalForValidatorRewards
$$

And the $$TotalForCommunityRewards$$ is distributed equally to operators \(project owners\) and nominators. $$RewardsForOperators$$ is the total amount of rewards assigned for operators \(project owners\). $$RewardsForNominators$$ is the total amount of rewards assigned for nominators.

$$
RewardsForOperators = RewardsForNominators = \frac{TotalForCommunityRewards}{2}
$$

The reward for each operator is given by the following formula, where $$RewardForOperators_{i}$$ ​ is the reward for the $$i$$ -th operator and $$C_{operator_i}$$ is the set of contracts deployed by the $$i$$ -th operator. $$TotalStake$$ represents the total amount of stake and $$Stake_{contract_j}$$ ​​ represents the amount of stake in $$contract_j$$ .

$$
RewardForOperators_{i} = \sum_{contract_j\ \in \ C_{operator_i}} \frac{Stake_{contract_j}}{TotalStake} \times RewardsForOperators
$$

Calculating compensation for a nominator is a bit more complicated: a nominator can only stake on contracts that are staked 3% or more of the $$TotalStake$$ .

This is to prevent participants from nominating themselves. In the following equation, let $$WeightedStake_i$$ ​ be the sum of $$i$$ -th nominator's stake amount that is weighted specifically for Community Rewards, and $$C_{nominator_i}$$ ​​ be the set of contracts nominated by the $$nominator_i$$ ​. $$RewardForNominators_i$$ ​ is the reward for the $$i$$ -th nominator. We'll get into the details of function $$f$$ in a moment.

$$
Threshold = TotalStake \times \frac{3}{100}
$$

$$
WeightedStake_{i} = \sum_{contract_j\ \in \ C_{nominator_i}} \left\{ \array{f(contract_j) & Threshold \leq Stake_{contract_j} \cr 0 & otherwize} \right.
$$

$$
RewardForNominators_i = \frac{WeightedStake_i}{TotalStake} \times RewardsForNominators
$$

The formula for the compensation received is expressed as $$f$$. This means that the more you nominate a contract with a small amount of stake, the more reward you get. This is expected to disperse the contract to be nominated.

$$
f(contract_j) = 0.197 \times -log_{2}(\frac{Stake_{contract_j}}{TotalStake})  \times Stake_{nominator_i}
$$

The magic number, 0.197, is used to make the coefficient close to 1 when $$\frac{Stake_{contract_j}}{TotalStake}$$ is 3% \(the smallest allowable fraction\).

$$
0.197 \times -log_{2}(\frac{3}{100}) = 0.996602... \simeq 1
$$

