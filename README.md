# Simplificando Pagseguro API Pagamento Recorrente

Certifique-se de ter criado sua aplicacao no ambiente de produçao e Sandbox.


## Autenticação

Para efetuar chamadas para as APIs do PagSeguro é necessário se autenticar usando suas credenciais.

URL do serviço de Planos e Assinatura do PagSeguro:

POST https://ws.pagseguro.uol.com.br/v2/pre-approvals/request
O cabeçalho Content-Type deve ser informado como no exemplo abaixo:

Content-Type: application/x-www-form-urlencoded;charset=ISO-8859-1
Accept: application/vnd.pagseguro.com.br.v3+json;charset=ISO-8859-1

## Credenciais de Conta

As credenciais de conta são utilizadas para que você efetue vendas através da sua conta, informando o email={mail} e token={token} como forma de autenticação, sendo que o e-mail é o mesmo utilizado no cadastro de sua conta PagSeguro.

Exemplo:

    curl -k https://ws.pagseguro.uol.com.br/v2/pre-approvals/request -d\
    "email={mail}\
    &token={token}"


**Criando Plano Test no sandbox pagseguro (NodeJS):**

    var request = require("request");
    
    var options = { method: 'POST',   url: 'https://ws.sandbox.pagseguro.uol.com.br/pre-approvals/request',   headers:     { 'cache-control': 'no-cache',
         Accept: 'application/vnd.pagseguro.com.br.v3+json;charset=ISO-8859-1',
         'Content-Type': 'application/x-www-form-urlencoded;charset=ISO-8859-1' },   form:     { email: 'seuemail@cadastrado.com.br',
         token: '66B11B80ESSEJOLHIFGIT9A43164CD',
         preApproval: '',
         preApprovalName: 'test',
         preApprovalCharge: 'AUTO',
         preApprovalPeriod: 'Monthly',
         preApprovalExpirationValue: '999',
         'preApproval.expiration.unit': 'YEAR',
         reference: 'devjfnf',
         preApprovalAmountPerPayment: '59.90',
         undefined: undefined } };
    
    request(options, function (error, response, body) {   if (error) throw new Error(error);
    
      console.log(body); });

**Consulta Planos por intervalo de datas no sandbox pagseguro (NodeJS):**

    var request = require("request");
    
    var options = { method: 'GET',
      url: 'https://ws.sandbox.pagseguro.uol.com.br/pre-approvals/request',
      qs: 
       { email: 'seuemail@cadastrado.com.br',
         token: '66B11B80ESSEJOLHIFGIT9A43164CD',
         startCreationDate: '2019-01-26T08:06:01-02:00',
         endCreationDate: '2019-01-26T16:07:01-02:00',
         status: 'ACTIVE' },
      headers: 
       { 'cache-control': 'no-cache',
         Accept: 'application/vnd.pagseguro.com.br.v3+json;charset=ISO-8859-1',
         'Content-Type': 'application/x-www-form-urlencoded' },
      form: { undefined: undefined } };
    
    request(options, function (error, response, body) {
      if (error) throw new Error(error);
    
      console.log(body);
    });










Alguns parametros nao estao de acordo com a Api de pagamento recorrente (link) https://devs.pagseguro.uol.com.br/v2/reference#pagamento-recorrente-1

é preciso consultar tambem esse pdf (link)
http://download.uol.com.br/pagseguro/docs/pagseguro-assinatura-automatica.pdf#page=17&zoom=100,0,238




---
Quando comecei a trabalhar com essa API ti dificultades com a documentaçao, entao decide organizar aqui os principais pontos e exemplos que precisei. Aproveito também para deixar os links utilizados para o desenvolvimento desse mini guia.

Contato:
jessefilhojfnf@gmail.com

---
Referencia:
https://devs.pagseguro.uol.com.br/v2/docs/modelo-de-aplicacoes-criando-sua-aplicacao
https://devs.pagseguro.uol.com.br/docs/pagamento-recorrente-endpoints-da-api
https://devs.pagseguro.uol.com.br/docs/pagamento-recorrente-criacao-do-plano
https://devs.pagseguro.uol.com.br/v1/reference#api-pagamento-recorrente-consultar-dados-de-planos
http://download.uol.com.br/pagseguro/docs/pagseguro-assinatura-automatica.pdf#page=17&zoom=100,0,238
