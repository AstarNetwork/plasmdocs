# Optimistic Virtual Machine

### Optimistic Virtual Machine（OVM）とは何か？

Plasma を扱う上で私達は OVM という技術を用います。これは、前述した Plasma を記述するために使用するプロトコルです。

{% page-ref page="reiy2soryshon.md" %}

さらに、**OVM は Plasma だけでなくすべてのレイヤー2ソリューションを抽象化したプロトコルです。**レイヤー2ソリューションには前述した State Channel や、Plasmaの無限のスケーラビリティとトレードオフに取引履歴の可用性に関する問題を解決した Optimistic Rollup などがあります。**OVMを用いることでこれらのような Plasma 以外のレイヤー2ソリューションも扱えるようにする発展性を持ち合わせることが出来ます。**

[Plasm Network](https://www.plasmnet.io/) では OVM をスマートコントラクトと切り離してモジュールとして用意することでより簡潔で便利に OVM を利用できるようにします。[Plasm Network ](https://www.plasmnet.io/)内では OVM とその周囲のアーキテクチャは以下のようになっています。

![](../.gitbook/assets/sukurnshotto-2020-05-29-161123png.png)

専用のクライアントアプリケーションである L1 adapter を介すことで適切に Plasmaアプリケーションを作成、動作させることが出来ます。アプリケーションは [Plasm Network ](https://www.plasmnet.io/)において OVM, Contracts module によって構成されます。Ethereum における Plasma 開発では、これらのモジュールで提供されているものはすべてスマートコントラクトで管理されていました。しかし、その場合だと複雑なロジックを内包しているPlasmaアプリケーションを実行する際のガスコストを予測しづらいという問題が発生します。

また、複数のコントラクトを組み合わせたアプリケーション構築は開発者に度々混乱を招くことが予想されます。そのため、[Plasm Network](https://www.plasmnet.io/) では3つのモジュールに役割を分離することで表面的に簡潔且つわかりやすい構成を考えました。

OVM Module ではユーザが Layer1 に上がっている情報に過ちを見つけた際に紛争を起こすための Universal Adjudication と呼ばれる機能が実装されています。Plasma Module は幾つかの Plasma のために必要不可欠なスマートコントラクトの共通実装をサポートしています。そして、各アプリケーションごとに異なるロジックが必要な実装のみを Contracts Module で管理しています。

私達はこれらのシステムをPolkadotを軸に展開しようと考えています。

{% page-ref page="../ekoshisutemu/polkadotnitsuite.md" %}

Polkadot は複数の異なるブロックチェーンを束ねるプロトコルです。Polkadot によって今まで独立だった複数のブロックチェーンが透明で分権的なガバンスのもと相互運用性を得ることができます。

さらに、Substrate と呼ばれるブロックチェーンを作るためのフレームワークがあります。

{% page-ref page="../ekoshisutemu/substratenitsuite.md" %}

Polkadot が束ねるチェーンや Polkadot 自体も Substrate を使って作られます。

#### 一つの理想的なブロックチェーンですべての用途を賄うことは現実的ではありません。ブロックチェーンを使う理由はユーザーごとに多様であり、すべてのニーズを満たすガバナンスの構築ないし可用性を維持することが難しいからです。

それ故に、今まで900を超えるパブリックブロックチェーンが作られてきました。Polkadot と Substrate は人々が用途に応じてブロックチェーンを作っていく時代にさらに拍車を掛けていくでしょう。Plasm Networkはこの大きな流れにのっています。当然、Polkadot においても Plasma は必要不可欠な役割です。

質問があれば、[Tech Chat](https://discord.gg/Cyjnrxv)の日本語チャネルでご質問ください。

