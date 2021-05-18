# Guia do validador 🔱

{% hint style="info" %}
Este pequeno guia explica como se tornar um validador Plasm testnet passo a passo.
{% endhint %}

1. Instale o node v1.0.0-dusty  usando [binários](https://github.com/staketechnologies/Plasm/releases/tag/v1.0.0-dusty) ou a partir do [código fonte](https://github.com/staketechnologies/Plasm#building-from-source)
2. Inicie o node plasm-node --validator --name node-name --rpc-cors all.
3. Aguarde a sincronização



![](../.gitbook/assets/testnet_sync.png)

* Abra "[Configuração](https://apps.plasmnet.io/#/settings)" e selecione o nó local.

![](../.gitbook/assets/testnet_settings.png)

* Abra “[Accounts](https://apps.plasmnet.io/#/accounts)” e crie uma nova conta.

![](../.gitbook/assets/testnet_accounts%20%281%29.png)

* Compartilhe o endereço da sua conta de validador com a equipe da Stake Technologies por meio do [Formulário do Google.](https://docs.google.com/forms/d/e/1FAIpQLSday0ckkK43TzJgKtQmJdzkudQNFDXspZAuUGi5Y5vfjkis3Q/viewform)
* [Reivindique tokens](https://medium.com/stake-technologies/dusty-lockdrop-how-to-claim-def048fa353) para transações ou solicite-os no canal [Discord](https://discord.gg/Z3nC9U4) \#faucet.
* Abra a ToolBox  e faça uma chamada RPC `rotateKeys ()` ou use o comando curl:

```bash
curl -H "Content-Type: application/json" -d '{"id":1, "jsonrpc":"2.0", "method": "author_rotateKeys", "params":[]}' http://localhost:9933
```

![](../.gitbook/assets/testnet_rotate.png)

* Salve o resultado para as próximas etapas
* Clique no botão "Session Key" e cole o resultado da conta do validador.

## **Conclusão**

Ao concluir este tutorial, aguarde um pouco enquanto a equipe da Stake Technologies aprova sua conta como validadora. Obrigado pela contribuição da Plasm Network e vamos melhorar o Plasm juntos!

## **Migração Testnet v3**

Se você já participou do testnet V3 como validador, pode estar interessado na migração. Copie suas chaves de sessão do keystore testnet v3 no keystore empoeirado, seguindo os comandos antes de iniciar o nó:

```text
mkdir .local/share/plasm-node/chains/dusty
cp -r .local/share/plasm-node/chains/plasm_testnet_v3/keystore .local/share/plasm-node/chains/dusty
```

alguma pergunta? Não hesite em perguntar-nos no [Discord Tech Channel.](https://discord.gg/Z3nC9U4)

