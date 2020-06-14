---
description: 'To Do: Finish the translation'
---

# dApps Reward 🍦

## **Preparação**

Assim como fizemos no tutorial anterior, precisamos implantar um contrato. Depois disso, quando você for para a barra lateral e pressionar DappsStaking, deverá aparecer da seguinte maneira. Quando você estiver aqui, nossa preparação terminou!

{% page-ref page="operator-trading.md" %}

![dAppsStaking Board](../.gitbook/assets/screen-shot-2020-06-11-at-16.26.00.png)

## **O conceito de Dapps Rewards**

A logística geral de como o Dapps Rewards funciona é a seguinte.

1. Selecione um contrato inteligente para apostar. \(isso também é chamado de nomeado\) 2. O nomeador e o operador de contrato inteligente nomeado ganharão incentivos econômicos da cadeia Plasm que são proporcionais à quantia que foi apostada.

![](../.gitbook/assets/sukurnshotto-2020-05-30-160230png%20%281%29.png)

### ① **Vamos nomear um contrato inteligente!**

Clique DappsStaking -&gt; Account actions.Se você não apostou nada anteriormente, sua tela deve se parecer com a seguinte. A partir daqui, pressione + Novo botão de aposta no canto superior direito.

![](../.gitbook/assets/screen-shot-2020-06-11-at-16.29.20.png)

Depois disso, você poderá ver uma tela parecida com a imagem a seguir. Existem quatro parâmetros de entrada aqui e vamos analisar todos eles.

* **Stash account:** Especifica quais tokens da conta usar. Pense nisso como uma "conta bancária".
* **Controller account:** Especifica a conta que controlará o status da indicação. Por motivos de segurança, é recomendável ter contas diferentes para as contas Stash e Controller, mas para esta demonstração, usarei a conta de Bob para ambas.
* **Value bonded:** Especifica a quantidade de token usada para staking.
* **Payment destination:** Especifica o destinatário das recompensas.

The following screen should appear that contains four input parameters as follows:

![Bonding](../.gitbook/assets/screen-shot-2020-06-11-at-16.31.22.png)

Depois de concluir as entradas, pressione Bonding\(união\) -&gt; sign\(Assinar\) e Submit \(Enviar\) para emitir uma transação. Agora você deve conseguir ver algo como a imagem a seguir; um novo cartão deve aparecer com o mesmo valor que foi fornecido no menu Preferências de ligação.

![](../.gitbook/assets/screen-shot-2020-06-11-at-16.33.28.png)

A quantia especificada vinculada e a conta receptora são iguais ao valor que fornecemos

Com isso, bloqueamos com sucesso nosso token. Mas isso não basta dizer que nomeamos alguém. Para isso, devemos pressionar o botão Nomear no lado direito do cartão.

![](../.gitbook/assets/screen-shot-2020-06-11-at-16.35.14.png)

Pressionar para mostrar o seguinte formulário. Aqui, escolhemos o Contrato Inteligente que será indicado. Vamos selecionar o contrato de demonstração chamado "SAMPLE.WASM" que enviamos do último artigo! Observe que só podemos escolher um contrato inteligente que tenha o parâmetro canBeNominate como Sim.

![](../.gitbook/assets/screen-shot-2020-06-11-at-22.54.43.png)

Pressione Nominate\(Nomear\) -&gt; Sign\(assinar\) e Submit \(Enviar\) para emitir uma transação. Após alguns instantes, como podemos ver na imagem a seguir, vemos uma nova seção denominada Nomeando com o contrato inteligente que escolhemos na etapa anterior.

![](../.gitbook/assets/screen-shot-2020-06-11-at-16.38.25.png)

Agora terminamos de nomear um contrato inteligente!

### ② **Vamos receber algumas recompensas Dapps!**

If you nominate a smart contract in the era \(E\), you can receive rewards after the next era \(E + 1\) is finished.

In case of Dusty

* Era = 1 day
* Session = 10 minutes

Actually, we need to wait until the era \(E + 2\), but we can fast-forward the era by using ForceNewEra on your local node. 

First, go to the sidebar and choose Extrinsics. Then with your root user \(Alice in this case\) to issue the following transaction two times. Sudo\(forceNewEra\(\)\).

![](../.gitbook/assets/screen-shot-2020-06-11-at-21.23.53.png)

Now, you can claim rewards with "Claim for Nominator" tab and "Claim for Operator" tab. Click "Claim for Nominator" tab on Staking page and click "Claim" button. Then, you can see the following modal.

![](../.gitbook/assets/screen-shot-2020-06-11-at-23.07.30.png)

To claim rewards for nominators, select nominator address and latest era, and push "Claim" button. You can use "Claim for Operator" tab for the same way.

![](../.gitbook/assets/screen-shot-2020-06-11-at-22.58.13.png)

### Summary <a id="summary"></a>

* We have played to nominate a smart contract!
* In Plasm, there is a system for incentivizing \(rewarding\) the Smart Contract owner!
* The amount being incentivized will be different from the users’ nomination!

New functionality of Plasm has been introduced through this and the previous article. As the Plasm Network is improved upon you will find updates to the documentation as well.

Any questions? Feel free to ask us on [Discord Tech Channel](https://discord.gg/Z3nC9U4).

