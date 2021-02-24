# ZKRollups

Plasm Networkは、Web3 Foundationの助成金を受けて、ZK Rollupsを実装しました。\([記事](https://medium.com/plasm-network/plasm-network-team-receives-a-web3-foundation-open-grant-to-implement-zk-rollups-2faceeeeaf1e)\)  
Plasmのビジョンは、Ethereum Virtual Machine（EVM）、WebAssembly（Wasm）の両方のロールアップをサポートするスマートコントラクトプラットフォームになることであり、将来的にはこれを拡大していきたいと考えています。

## ロールアップとは? <a id="what-is-a-rollup"></a>

ロールアップとは、Ethereumスマートコントラクト内の取引をオフチェーンで集約することで、ブロックチェーンのスループットを現在の15tpsから1,000tps以上に向上させることで、手数料や混雑を軽減します。スマートコントラクト内では、ユーザーはセキュリティが保証された状態で取引を行うことができます。その取引は悪用されることはなく、将来のある時点でメインチェーンにて決済されます。それは、誰もが状態（例：口座残高）を再現し、無効性を検出することができるように、オンチェーン上に十分なデータだけを公開します。

#### zkSyncとは？ <a id="what-is-zksync"></a>

zkSyncは、Ethereum用のスケーリングおよびプライバシーエンジンです。現在の機能範囲には、Ethereumネットワーク内でのETHとERC20トークンの低ガス転送が含まれています。![](https://cdn-images-1.medium.com/max/800/1*nhUeqOVM1ij6dwSM_nLyaw.png)

zkSync は ZK-Rollupのアーキテクチャに基づいて構築されています。要するに、ZK-Rollupはレイヤー2スケーリングソリューションであり、すべての資金はメインチェーン上のスマートコントラクトによって保持され、計算とストレージはゼロ知識証明によってサイドチェーンの有効性が保証されるオフチェーンで実行されます。Rollupブロックごとに、状態遷移ゼロ知識証明（SNARK）が生成され、メインチェーンのコントラクトによって検証されます。このSNARKには、Rollupブロック内のすべての単一トランザクションの有効性の証明が含まれています。さらに、各ブロックの公開データ更新は、安価なCALLDATAでメインチェーンネットワーク上に公開されます。

言い換えれば、ZK-Rollupは、基礎となるレイヤー1のセキュリティ保証を厳密に継承しています。

## ロードマップ <a id="roadmap"></a>

下の表を見ていただければわかるように、私たちは前もって設定したマイルストーンに沿って進んでいます。まだまだ先のことがたくさんありますが、私たちの道のりのすべての進展を皆さんにお知らせします。

![](https://gblobscdn.gitbook.com/assets%2F-M8GVK5H7hOsGnYqg-7q%2F-MTV2l9E8kyfV_8sF0Ov%2F-MTV4-JkuEPF2Hoqj9Ft%2Fimage.png?alt=media&token=e1f74d12-f63d-40e6-8f9b-6d6784bf33b7)

