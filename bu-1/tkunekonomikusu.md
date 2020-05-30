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

* $$Rewards_{operators}$$ ： Operator が得る報酬の総量
* $$Rewards_{stakers_{validators}}$$ ：バリデータに対する Staking によって得る報酬の総量
* $$Reards_{stakers_{contracts}}$$ ：スマートコントラクトに対する Staking によって得る報酬の総量
* $$t$$ ： Operator が得る報酬の総量がスマートコントラクトに対する Staking によって得る報酬の何倍かを表す係数

Dapps Rewards の章より t=4であり、理想的な $$q$$ を満たすときの報酬全体の50%が Dapps Rewards の報酬に当てられます。そのため、理想的な報酬の配分比率を以下のように定めます。

{% page-ref page="dapps-reward.md" %}

$$
Rewards_{stakers_{validators}}:Rewards_{stakers_{contracts}}:Rewards_{operators}=5:1:4\\t=4
$$

また、Staking の割合と報酬の割合は以下のように等しくなります。

$$
Staking_{validators}:Staking_{contracts}=Rewards_{stakers_{validators}}:Rewards_{stakers_{contracts}}
$$

PLM トークンは Polkadot と同じ NPoS を起用します。このノミネータとバリデータは Staking に対してある年利でトークン運用を行うことができます。また、PLM Dapps operator のノミネータとOperatorにも同様にトークン報酬が支払われます。Plasm Network のインフレーションモデルは下記のように定義されます。まず、Polkadot のインフレーションモデルを踏襲して以下のような変数を定義します。

* $$x$$ ：全体の Staking 量をトークンの総発行量で割ったもの
* $$X_{ideal}$$ ：$$x$$ の理想的な値です. $$Staking : Liquidity = 1 : 1$$ なので $$X_ideal=0.5$$ 
* $$q$$ ：バリデータへの Staking 量を全体の Staking 量で割った値

$$
q=\frac{Staking_{validators}}{Staking_{validators}+Staking_{contracts}}
$$

* $$Q_{ideal}$$ ： $$q$$ の理想的な値。上記の式より、 $$q$$ の理想値は $$Q_{ideal} = 5/6$$ になります。 
* $$i(x,q)$$ ：Staker が得られる平均的な年利。 $$x$$ , $$q$$ を共に理想値に近づけるために、 $$x$$ , $$|Q_{ideal}-q|$$ \(理想的な比率との差分\)について単調減少関数です。 $$x$$ , $$|Q_{ideal}-q|$$ が低い時は Stake 量を増やすインセンティブとして金利を上げます。 $$x$$ ,  $$|Q_{ideal}-q|$$ が高い時は Stake 量を減らすインセンティブとして金利を下げます。 
* $$i_{ideal}$$ ： $$x$$ , $$q$$ が共に理想値であるときの Stakerの平均年利 $$i(x,q)$$ 。言い換えると $$i_{ideal}= i(X_{ideal}, Q_{ideal})$$ です。 
* $$I_{Staking}$$ ： Staking によるインフレーションレート。 $$x$$ , $$q$$ を含む二変数関数であるは $$I_{Staking}$$ 三次元の凸関数を描きます。 $$Staking 総量 \times 金利 = インフレ率$$ と表わせ数式にすると $$x \times i(x,q) = I_{Staking}$$ と表現できます。また、この値は $$i(x,q)$$ の報酬設計から $$x$$ , $$q$$ が理想値である時に最大化します。理想状態の式は $$X_{ideal} \times i(X_{ideal}, Q_{ideal}) = Maxmium I_{Staking}$$ と表すことが出来ます。 
* $$I_0$$：インフレーションレートの下限値。 $$x = 1$$ or $$x = 0$$ の時、下限値に収束するようにします。 $$I_0$$ はバリデータの 運用コストと同値です。なぜなら最低限バリデータの運用インセンティブを確保しなければ、チェーンが途絶えてしまうからです.ここでは $$I_0=0.025$$ を推奨します。 
* $$d$$ はそれぞれ $$x$$ にかかる調整可能な減衰率です。 $$x$$ が $$X_{ideal}$$ より $$d$$ 増加するごとに $$I_{Staking}$$ が50%減少します。言い換えると $$I_{Staking}(X_{ideal}+d, Q_{ideal})\ge I_{Staking}/2$$ です。 $$d=0.02$$ を推奨します。 
* $$g$$ は $$q$$ にかかる調整可能な減衰率です。 $$q$$ が $$Q_{ideal}$$ より $$g$$ 離れるごとに $$I_{Staking}$$ が50%減少します。言い換えると $$I_{Staking}(X_{ideal}, Q_{ideal}\pm e)\ge I_{Staking}/2$$ です。 $$g =0.15$$ を推奨します。 
* $$i_{staking}$$ ：ノミネータが Staking により得られる平均的な年利。これはインフレ率をStaking比率で割ることで求めることができます。言い換えると $$i_{staking} = \frac{I_{Staking}}{x}$$ と表現できます。 
* $$I_{operators}$$ は Operator が得られる報酬によるインフレ率です。これは $$I_{Staking}$$ における Operator への Staking が占める割合 $$(1-q)$$ を $$t$$ 倍したものです。上記より、 $$I_{operator}=t(1-q)I_{Staking}$$ と表すことができます。

$$
Staking_{validators}:Staking_{contracts}=Rewards_{stakers_{validators}}:Rewards_{stakers_{contracts}}
$$

$$
Rewards_{stakers_{validators}}:Rewards_{stakers_{contracts}}:Rewards_{operators}=y:1:t
$$

$$
Rewards_{stakers_{validators}}:(Rewards_{stakers_{contract}}+Rewards_{stakers_{validators}})=y:(y+1)
$$

$$
Rewards_{staking_{validators}}(y+1)=(Rewards_{staking_{contract}}+Rewards_{staking_{validators}})y
$$

$$
q=\frac{Staking_{validators}}{Staking_{validators}+Staking_{contracts}}=\frac{Rewards_{stakers_{validators}}}{Rewards_{stakers_{validators}}+Rewards_{stakers_{contracts}}}\\=y/(y+1)
$$

$$
q=y/(y+1)\\(y+1)q=y\\yq+q=y\\q+q/y=1\\q/y=1-q\\y=q/(1-q)
$$

$$
Rewards_{stakers_{validators}}:Rewards_{stakers_{contracts}}:Rewards_{operators}=q/(1-q):1:t
$$

$$
Rewards_{stakers}:Rewards_{operators}=q/(1-q)+1:t
$$

ここで、報酬の量の比率とインフレ率の比率は等しい。

$$
I_{Staking}:I_{operators}=q/(1-q)+1:t
$$

$$
I_{operstors}(q/(1-q)+1)=I_{Staking}t
$$

$$
I_{operators}=\frac{tI_{Staking}}{\frac{q}{1-q}+1}\\\frac{tI_{Staking}}{\frac{q}{1-q}+\frac{1-q}{1-q}}\\\frac{tI_{Staking}}{\frac{1}{1-q}}\\=t(1-q)I_{Staking}
$$



質問があれば、[Tech Chat](https://discord.gg/Cyjnrxv)の日本語チャネルでご質問ください。

