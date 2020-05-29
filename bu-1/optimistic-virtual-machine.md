# Optimistic Virtual Machine ✨

### Optimistic Virtual Machine（OVM）とは何か？

Plasma を扱う上で私達は OVM という技術を用います。これは、前述した Plasma を記述するために使用するプロトコルです。

{% page-ref page="reiy2soryshon.md" %}

さらに、**OVM は Plasma だけでなくすべてのレイヤー2ソリューションを抽象化した存在です。**レイヤー2ソリューションには前述した State Channel や、Plasmaの無限のスケーラビリティとトレードオフに取引履歴の可用性に関する問題を解決した Optimistic Rollup などがあります。**OVMを用いることでこれらのような Plasma 以外のレイヤー2ソリューションも扱えるようにする発展性を持ち合わせることが出来ます。**

私達はこれらのシステムをPolkadotを軸に展開しようと考えています。

{% page-ref page="../ekoshisutemu/polkadotnitsuite.md" %}

Polkadot は複数の異なるブロックチェーンを束ねるプロトコルです。Polkadot によって今まで独立だった複数のブロックチェーンが透明で分権的なガバンスのもと相互運用性を得ることができます。

さらに、Substrate と呼ばれるブロックチェーンを作るためのフレームワークがあります。

{% page-ref page="../ekoshisutemu/substratenitsuite.md" %}

Polkadot が束ねるチェーンや Polkadot 自体も Substrate を使って作られます。

#### 一つの理想的なブロックチェーンですべての用途を賄うことは現実的ではありません。ブロックチェーンを使う理由はユーザーごとに多様であり、すべてのニーズを満たすガバナンスの構築ないし可用性を維持することが難しいからです。

それ故に、今まで900を超えるパブリックブロックチェーンが作られてきました。Polkadot と Substrate は人々が用途に応じてブロックチェーンを作っていく時代にさらに拍車を掛けていくでしょう。Plasm Networkはこの大きな流れにのっています。当然、Polkadot においても Plasma は必要不可欠な役割です。

