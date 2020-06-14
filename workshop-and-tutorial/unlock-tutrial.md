# Unlock Tutorial 🔓

O Contrato de Bloqueio do Lockdrop contém a seguinte função anônima.  


```text
/**
* @dev Withdraw function once timestamp has passed unlock time
*/

function () external payable {
 assembly {
  switch gt(timestamp, sload(0x01))
  case 0 { revert(0, 0) }
  case 1 {
   switch call(gas, sload(0x00), balance(address), 0, 0, 0, 0)
  case 0 { revert(0, 0) }
  }
 }
}
```

Isso permite que o contrato retorne o saldo bloqueado \(todo o saldo do contrato\) para o endereço do cacifo original, enviando uma transação vazia para esse endereço do contrato. No entanto, o registro de data e hora da transação deve ser maior que o registro de data e hora do bloqueio, incluindo a duração do bloqueio. Quando alguém envia uma transação antes que a duração dos bloqueios seja passada, a transação retornará um erro. O envio de uma transação para o bloqueio \(ou seja, desbloquear os tokens\) pode ser feito por qualquer pessoa, uma vez que eles têm fundos suficientes para pagar a taxa da transação. Mas os tokens bloqueados retornarão apenas ao armário original, e não ao endereço que enviou a transação. Portanto, é possível permitir que outro endereço desbloqueie o token bloqueado em nome do armário original, mas eles não podem reivindicar os tokens por si mesmos. Um ponto a ser observado é que, quando a duração do bloqueio terminar, o contrato não terá nenhuma rejeição de transação, ou seja, mesmo que o token tenha sido devolvido ao armário original, qualquer pessoa ainda poderá enviar uma transação ao contrato sem erros. Depois que o token for reivindicado, ele não poderá retornar mais tokens, pois o saldo do contrato será 0, mas torna difícil para o cacifo original verificar se os tokens foram desbloqueados ou não sem ter que verificar o saldo do contrato ou rastreie seu saldo, efetivamente dando um possível problema de desperdício de taxa de transação por tentar reivindicar os tokens bloqueados que já estavam desbloqueados.

![](../.gitbook/assets/sukurnshotto-2020-05-31-191620png.png)

O aplicativo da Web Lockdrop é fornecido com um formulário intuitivo que exibe qualquer informação de bloqueio. Na guia `Unlock Tokens`, ele exibirá uma lista de bloqueios bloqueados pelo endereço atual em uma extensão da carteira do navegador habilitada para Web3. Quando a duração do bloqueio terminar, o ícone de bloqueio à direita mudará para uma cor mais clara. Clicar neste ícone permitirá enviar para a transação 0 ETH para o endereço de bloqueio, desbloqueando os tokens. Este formulário permite que você verifique facilmente as informações do bloqueio, tempo até o bloqueio terminar e desbloquear assim que terminar. No entanto, como mencionado acima, é difícil verificar se o bloqueio já foi reivindicado ou não; portanto, mesmo se os bloqueios foram reivindicados com êxito, os elementos da interface do usuário ainda terão a mesma aparência.

Alguma pergunta? Não hesite em perguntar-nos no [Discord Tech Channel.](https://discord.gg/Z3nC9U4)

