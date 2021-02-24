# Ankr

Ankrは、デスクトップとモバイルでPlasm Networkのノードホスティングとバリデート\(検証\)サービスを簡単に実現します。

Plasm Networkは、Web3へのゲートウェイである[Ankr](https://www.ankr.com/)との統合を展開しており、個人ユーザ、開発者、法人を数回のクリックで簡単に新しいインターネットに接続することができます。発表の全文は[こちら](https://medium.com/plasm-network/one-click-plasm-testnet-node-on-ankr-1a177f988bcc)

## アカウントを作成する

Ankrのウェブサイトにアクセスして、アカウントを作成します。アカウントを作成したら、彼らのマーケットにアクセスすることができます。「Plasm Testnet - Dusty」を検索し、「Deploy」をクリックします。

![](../../.gitbook/assets/image%20%287%29.png)

## ノードをSetupする

ノードが完全にデプロイされ、ネットワークに同期されたら、次の手順に進みます。

![](../../.gitbook/assets/image%20%288%29.png)

[Polkadot Telemetry Web App](https://telemetry.polkadot.io/#/Dusty)でノードのリアルタイムの統計を取得できます。Dustyタブで、ノード名を検索して詳細情報を取得します。ノードの同期が完了したら、次の手順に従います。

**\#1** - [Plasm Network UI](https://apps.plasmnet.io/#/accounts) に移動し、アカウントを作成します。「Dusty」testnetに接続されていることを確認します。左上のメニューでネットワークから変更できます。

![](../../.gitbook/assets/image%20%286%29.png)

**\#2 -** アカウントをお持ちでない場合は、「アカウントの追加」をクリックしてアカウントを作成することができます。フォームがポップアップします。名前とパスワードを選択します。このフォームの最も重要な部分は、あなたのニーモニックシードです！これを書き留めたり、スクリーンショットを撮ったり、絶対に紛失しないようにしてください。

 「次へ」と「保存」をクリックします。あなたの\*.jsonファイルをコンピュータ、クラウド、に保存します。あなたのニーモニックシードを失った場合には、常にこのファイルを使用してアカウントを復元することができます。

**\#3 -** Ankrのダッシュボードにある「Session Key」をコピーします。Plasm UIに戻り、「Developer」-「Extrinsics」-「Session」-「setKeys\(keys, proof\)」をクリックし、結果を「keys」フィールドに、「proof」フィールドに「0x00」と入力して貼り付けます。

![Image for post](https://miro.medium.com/max/1869/1*o9mHfP4suI_1i7kzymaxAg.png)

キーを貼り付けたら「Submit Transaction」を忘れずに。

**\#4 -** あなたのバリデータアカウントのアドレスを[Google Form](https://docs.google.com/forms/d/e/1FAIpQLSday0ckkK43TzJgKtQmJdzkudQNFDXspZAuUGi5Y5vfjkis3Q/viewform).でStake Technologiesチームと共有します。 

**\#5 -** Dusty バリデータシートであなたの投稿をフォローします。（[Dusty validator sheet](https://docs.google.com/spreadsheets/d/1AYsS6V_Ypwde5lYulhZBMAx1X2vZ1u1zDXni_ddz-6c/edit#gid=2013382367).）

That's it!

