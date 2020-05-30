# トークンエコノミクス

Plasm NetworkのトークンエコノミクスはPolkadotを参照にしています。従って、このセクションにはPolkadotのトークンエコノミクスも含まれます。

Plasm Networkにおけるトークンの名前はPLMといい、"PLUM（プラム）"と発音します。

 PLMには主に4つの役割が存在しています。

1. コンセンサスのためのステーキング、ValidatorとNominatorへの報酬
2. 悪意ある攻撃を防ぐためのトランザクション手数料
3. DApps開発者へのブロック報酬
4. ガバナンス

PLMにおいて意図されているステーキングに使われるPLMと流動性に使用されるPLMの割合は1:1となるように設計しています。

$$
Staking ： Liquidity＝ 1:1
$$

### インフレーションモデル

Plasm Networkの新規トークンを発行する際の発行額や配布方法を決定するアルゴリズムを定義します。Plasm Networkは、新規トークン発行額をDapps Rewardsと共有し、ブロックチェーン上の価値を高める行為に対してリワードを付与するという構造になっています。ブロックチェーンのコンセンサス・アルゴリズムは最終的にNPoSになります。これにより、Stakingのアクションには2種類のタイプがあります。ValidatorのためのStaking \(NPoS\)と、スマートコントラクトのためのStaking \(Dapps Rewards\)です。それぞれのStakingによる報酬は、どちらもStakingの量に等しく比例します。

{% page-ref page="dapps-reward.md" %}

Validatorやスマートコントラクトにステークをするユーザーを総称してノミネーターと呼びます。ValidatorのStakingとスマートコントラクトのStakingの理想的な比率は以下の通りです。

$$
5:1 = Staking_{validator}: Staking_{contrracts}
$$

また、ここで Dapps Rewards における Operator に支払う報酬について考えます。Operator 報酬は Staking によるインフレ率に比例して増加します。Dapps Rewards の章より理想的な $$q$$ を満たすときに報酬全体の50%が Dapps Rewards の報酬に当てられます。

{% page-ref page="dapps-reward.md" %}

またそのときにに Operator の得られる報酬は最大化します。具体的な報酬の配分を示すために、以下の変数を導入します。



