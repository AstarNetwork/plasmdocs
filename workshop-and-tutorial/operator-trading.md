# Negociação do operador 💱

## **Preparação**

Para acompanhar esta demonstração no testnet, você precisará de alguns tokens. Se você não possui um, junte-se ao nosso [servidor do Discord](https://discord.gg/wUcQt3R) e vá para **\#faucet** para obter alguns! Se você quiser apenas testá-lo sem tokens, também poderá usar o Nó Local do Desenvolvedor.

{% hint style="info" %}
**O nó local pode ser facilmente configurado usando a imagem da janela de encaixe para o nó Plasm, o que pode ser feito a partir dos seguintes comandos.**
{% endhint %}

```text
$ docker pull staketechnologies/plasm-node:dApps-reward
$ docker run -p 9944:9944 staketechnologies/plasm-node:dApps-reward --dev --ws-external
```

After that, go to [https://local.plasmnet.io/](https://local.plasmnet.io). It connects to your local node.

![Home](../.gitbook/assets/screen-shot-2020-06-11-at-15.24.26.png)

Para aqueles que desejam executar o nó em outro método, consulte nosso Leia-me. Para perguntas e comentários, junte-se ao nosso Discord, teremos o maior prazer em entrar em contato com você!

## **Vamos usar a negociação com operadores !!**

Para começar, acesse https://apps.plasmnet.io/

### ① **Upload Contrato**

Não podemos fazer nada sem fazer upload de nossos contratos; portanto, primeiro, faça isso clicando em OP Contracts \(abreviação de Contracts Operated\) na barra lateral e clique em Upload WASM.

**Upload do contrato por nós mesmos**

Quando não há Contratos carregados, a página Contratos OP será semelhante à imagem a seguir.

![Upload WASM](../.gitbook/assets/screen-shot-2020-06-11-at-15.44.05.png)

Quando você clica no botão Carregar WASM na página, o seguinte modal aparecerá na sua tela.

![Upload WASM \(Modal Window\)](../.gitbook/assets/screen-shot-2020-06-11-at-15.45.42.png)

É aqui que fornecemos o arquivo WASM e o ABI JSON que foi compilado a partir da tinta! Contrato. Claro, você sempre pode criar o seu próprio, mas não será uma tarefa trivial para as pessoas que estão participando. Então, desta vez, preparei uma amostra de Contrato inteligente usando o ink-playground.

## **Faça o download do contrato de amostra**

Primeiro, visite [https://ink-playground.com](https://ink-playground.com/), você verá um contrato pré-codificado no editor na tela. Tudo o que você precisa fazer é pressionar o botão **COMPILE CODE** para \(você adivinhou\) compilar o código.  


![Click COMPILE CODE](../.gitbook/assets/screen-shot-2020-06-11-at-15.50.03.png)

Aguarde alguns segundos e você verá a seguinte mensagem no painel do lado direito. É possível fazer o download do arquivo WASM e do arquivo METADATA clicando no botão com o mesmo nome. Os nomes padrão dos arquivos baixados serão "sample.wasm" e "metadata.json".

![Download WASM and METADATA](../.gitbook/assets/screen-shot-2020-06-11-at-15.56.52.png)

Agora vamos voltar ao modal Upload WASM. Em seguida, carregamos o “sample.wasm” no painel WASM do contrato compilado e o “metadata.json” no painel ABI do contrato. Quando terminarmos tudo isso, o seguinte parâmetro será exibido.

![Ready upload contract binary](../.gitbook/assets/screen-shot-2020-06-11-at-15.56.08.png)

Depois disso, fazemos o upload -&gt; Assinar e enviar. Agora você deve poder ver o contrato que enviamos.

![Uploaded the Smart Contract](../.gitbook/assets/screen-shot-2020-06-11-at-15.59.49.png)

É isso aí! Fizemos o upload do contrato inteligente com sucesso!  


### **① Lendo um contrato existente**

Se você estiver usando o Plasm Testnet v3 em vez de um nó local, poderá facilitar sua vida escolhendo OpContracts -&gt; Adicionar um hash de código existente e copie o seguinte hash no painel de hash de código.

```text
0x22b781155b1a9df69ea97ac5ec8f35af8e90f5dc7173439dcab50aafdcd7b5bb
```

Depois disso, basta fornecer o "metadata.json" ao painel da ABI do contrato para ler o contrato inteligente existente no blockchain.

![add](https://user-images.githubusercontent.com/6259384/77171472-d7ec1700-6aff-11ea-8615-87129335dab3.png)

### ② **Vamos implantar o contrato !!**

No Plasm, você não pode simplesmente usar o contrato fazendo o upload dele. Ele funcionará apenas como um Contrato inteligente adequado depois de implantá-lo na cadeia. Isso é para aumentar a reutilização do contrato inteligente. A implantação do contrato é muito simples. Tudo o que você precisa fazer é clicar no botão de implantação, localizado no canto superior direito, e preencher os valores exigidos no item anterior Implantar um novo portal de contratos e clicar em Deploy\(Implementar\) -&gt; Sing\(Assinar\) e Submit\(enviar\).

![Click Deploy](../.gitbook/assets/screen-shot-2020-06-11-at-16.04.52.png)

![Input Parameters and click deploy](../.gitbook/assets/screen-shot-2020-06-11-at-16.10.34.png)

Durante esta etapa, como as pessoas que fizeram o upload de um contrato inteligente em um blockchain utilizado no Substrato diferente podem ter notado algo diferente no portal de implantação de contratos. Essa é uma caixa de entrada Parâmetros, destacada em vermelho na figura acima. No Plasm, você pode definir um parâmetro especial para cada contrato. Isso é importante para o recurso especial acima mencionado para Plasm; o DappsRewards. Mas isso está além do escopo do artigo de hoje, portanto, basta fornecer o valor Sim ao parâmetro canBeNominated e enviá-lo. Quem sabe, algo de bom pode acontecer. Depois de concluir a implantação do contrato, podemos ver o contrato implantado e o operador como imagem a seguir. O primeiro operador é uma conta que implanta o contrato \(captura de tela de um nó local, portanto, o motivo pelo qual o operador chama Alice\).

![Deployed contract \(SAMPLE.WASM\) and its operator \(ALICE\)](../.gitbook/assets/screen-shot-2020-06-11-at-16.14.43.png)

Como você pode ver, no Plasm existe um conceito de propriedade entre os Smart Contracts, que chamamos de Operador.

### ③ **Vamos mudar de operador**

Agora chegou a hora de mudarmos de operador! Primeiro, clique na guia Operator\(Operador\) no lado esquerdo.

![Select Operator](../.gitbook/assets/screen-shot-2020-06-11-at-16.17.17.png)

Isso exibirá o seguinte modal. A escolha de um operador a partir daqui exibirá uma lista de todos os contratos que a conta possui. Você deverá escolher em qual contrato deseja alterar a propriedade. Depois disso, escolhemos o novo Operador que terá a propriedade do Contrato selecionado. Neste exemplo, o ALICE transferirá a BOB a propriedade do contrato SAMPLE.WASM.

![ALICE&apos;s contract list](../.gitbook/assets/screen-shot-2020-06-11-at-16.19.46%20%282%29%20%282%29%20%281%29.png)

Pressione Change Operator\(Alterar Operador\) -&gt; Sign\(Assinar\) e Submit\(Enviar\), depois de alguns momentos, podemos ver na imagem a seguir que o Operador do Contrato mudou de ALICE para BOB.  


![Changed Operator](../.gitbook/assets/screen-shot-2020-06-11-at-16.21.22.png)

Com isso, concluímos a demonstração para criar um contrato inteligente e transferir sua propriedade de um operador para outro! Obrigado por continuar conosco.  


### **Sumário** <a id="summary"></a>

* Falamos sobre como usar a função Operator Trading.
* Falamos sobre como o Plasm tem um conceito de propriedade no contrato inteligente
* E podemos transferir a propriedade do Contrato de acordo com o Operador.

Então, agora, mostramos o conceito de propriedade de contrato e a transferência de propriedade, mas por que é importante e por que todos deveriam se preocupar com isso? A resposta é simples; a propriedade do Contrato inteligente determina quem recebe o lucro dos Dapps Rewards. A próxima pergunta seria "então como é que esse Dapps Rewards funciona?" Isso será discutido no próximo artigo, passando por algumas demos. Então, fique atento para mais!

Alguma pergunta? Não hesite em perguntar-nos no [Discord Tech Channel.](https://discord.gg/Z3nC9U4)

