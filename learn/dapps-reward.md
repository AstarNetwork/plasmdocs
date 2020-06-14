# dApps Reward 🍭

O Dapps Rewards é um mecanismo que recompensa continuamente desenvolvedores ou administradores de contratos inteligentes. 50% da recompensa de apostas da Plasm Network é destinada a desenvolvedores de aplicativos que aprimoraram o valor da Plasm Network. A Plasm Networking  permite atribuir um administrador de contrato inteligente a um contrato inteligente, e esse administrador é chamado de "Operador". O usuário também pode fazer contratos inteligentes. Essa ação é chamada de nomeado e a pessoa que faz isso é chamada de nomeador de Dapps. Como mostrado abaixo, o operador do contrato inteligente que recebe muitos candidatos pode receber o token PLM recém-emitido da cadeia.

![](../.gitbook/assets/sukurnshotto-2020-05-31-195848png.png)

Definiremos como distribuir essa recompensa ao Operador e Nominador, respectivamente. Defina as seguintes variáveis:

* $$Rewards_{nominate}$$ : O total de recompensas alocadas ao Nominator.
* $$Rewards_{contract}$$ : O total de prêmios alocados a contratos inteligentes.
* $$Rewards_{nominate_{i,j}}$$ : As recompensas alocadas ao j-ésimo candidato ao j-th contrato inteligente.
* $$Rewards_{contract_i}$$ : As recompensas alocadas ao operador do i-th contrato inteligente.
* $$n$$ : O número de contrato inteligente.
* $$m_i$$ : O número de indicados contra o i-ésimo contrato inteligente.
* $$stake_{i,j}$$ : A quantidade de PLM apostada pelo j-th candidato para o i-th contrato inteligente.

A, $$Nominate_ {i, j}$$ dá a seguinte recompensa por esta aposta.

$$Rewards_{nominate_{i,j}}=Rewards_{nominate} \times \frac{\sum_{j}^{m_i}stake_{i,j}}{\sum_i^n\sum_j^{m_i}stake_{i,j}}$$

O nomeador pode receber uma recompensa proporcional à proporção entre o valor da sua estaca e o valor total da estaca do contrato inteligente, independentemente do contrato inteligente selecionado. O operador de  $$contract_i$$ que recebeu a Estaca receberá a seguinte recompensa.

$$Rewards_{contract_i}=Rewards_{contract}\times\frac{stake_{i,j}}{\sum_i^n\sum_j^{m_i}stake_{i,j}}$$

Por outro lado, o operador pode receber uma recompensa proporcional à proporção da participação do contrato inteligente de sua propriedade em relação à participação do contrato inteligente. Isso cria um incentivo para o nomeador apostar em contratos inteligentes que simplesmente aumentariam o valor do token. Os operadores também podem receber recompensas semi-permanentes, recebendo participações em contratos inteligentes gerenciados por eles mesmos. Esperamos que esta seja uma solução inovadora para o difícil problema de monetizar desenvolvedores de aplicativos \(administradores\) na cadeia.

{% hint style="info" %}
**Os operadores e nominadores precisam esperar para receber recompensas.**
{% endhint %}

