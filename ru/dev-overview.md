# 開発の全体像

Plasm NetworkではWebAssemblyで記述されたコントラクトをデプロイすることができます。ここでは、RustのEmbedded DSLとして提供されるink!を利用して、Plasm Network上のコントラクトを開発する手順について説明をします。

{% hint style="info" %}
Plasm Networkには現在、上記ink!に加え、Solidityで書かれたコントラクトもコンパイルしデプロイすることができます。
{% endhint %}

{% page-ref page="writing-smart-contract.md" %}

ink!を利用したコントラクト開発の全体像は以下の図のようになります。

![&#x30B3;&#x30F3;&#x30C8;&#x30E9;&#x30AF;&#x30C8;&#x958B;&#x767A;&#x306E;&#x5168;&#x4F53;&#x50CF;](../.gitbook/assets/screen-shot-2020-07-17-at-16.52.08.png)

1. **セットアップ：** ink!の環境構築およびプロジェクトディレクトリのセットアップを行います
2. **ink!コードの更新：** 開発したいコントラクトに応じてink!コードの更新を行います
3. **テスト：** 記述したコントラクトが意図通りの挙動をとるかテストを行います
4. **コンパイル：**ink!コード\(Rust\)をwasmバイナリに変換します
5. **Dusty Networkにデプロイ：**Dusty Networkノードにwasmバイナリをデプロイします
6. **Dusty Networkの動作を確認**
7. **Plasm Networkにデプロイ：**Plasm Networkノードにwasmバイナリをデプロイします
8. **Plasm Networkの動作確認とUI開発**

