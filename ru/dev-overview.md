# 開発の全体像

Plasm NetworkではWebAssemblyで記述されたコントラクトをデプロイすることができます。ここでは、RustのEmbedded DSLとして提供されるink!を利用して、Plasm Network上のコントラクトを開発する手順について説明をします。

{% hint style="info" %}
Plasm Networkには現在、上記ink!に加え、Solidityで書かれたコントラクトもコンパイルしデプロイすることができます。
{% endhint %}

{% page-ref page="writing-smart-contract.md" %}

ink!を利用したコントラクト開発の全体像は以下の図のようになります。

![&#x30B3;&#x30F3;&#x30C8;&#x30E9;&#x30AF;&#x30C8;&#x958B;&#x767A;&#x306E;&#x5168;&#x4F53;&#x50CF;](../.gitbook/assets/screen-shot-2020-07-17-at-16.52.08.png)

① セットアップ: ink!の環境構築およびプロジェクトディレクトリのセットアップを行います  
② ink!コード更新: 開発したいコントラクトに応じてink!コードの更新を行います  
③ テスト: 記述したコントラクトが意図通りの挙動をとるかテストを行います  
④ コンパイル: ink!コード\(Rust\)をwasmバイナリに変換します  
⑤ Plasmノードに: wasmバイナリをデプロイします

