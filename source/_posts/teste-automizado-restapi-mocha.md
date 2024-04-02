---
title: Testes automatizados utilizando Mocha no NodeJS
date: 2019-08-23 22:49:26
tags:
  - NodeJS
  - Mocha
  - Rest API
  - Teste
  - Teste automatizado
---
![Mocha](/images/teste-automizado-restapi-mocha/mocha.png)

O teste automatizado foi criado no intuito de facilitar o teste do API Rest do Hybris Croisement, anteriormente realizado através do Postman e tendo muitos passos para o fluxo completo de uma compra. A partir do teste criado, é possível executar o fluxo com a ausência de tantos cliques. A ideia de BDD também foi seguida, no intuito de termos uma documentação de como a API Rest deve trabalhar do e-commerce do Carrefour.

Em sua arquitetura temos a seguinte combinação: _Node.JS_ com as dependências _Mocha_, _Mocha Steps_, _Mocha Logger_, _Should_, _Request_ e _Chai_.

Pré-requisito: **Node.JS** >= 11.0.0
<!-- more -->


Repositório: https://github.com/matheusgeres/croisement-app-test-node



No página inicial do repositório contém as instruções básicas para que o projeto seja executado, a ideia desenvolvida foi de separar o projeto primeiramente por pastas que contenha algum **conceito** importante para a API Rest, por exemplo, foi desenvolvido teste para compra (purchase), onde a compra com um ou vários itens é realizada do começo ao fim.

![Estrutura do teste](/images/teste-automizado-restapi-mocha/1-estrutura.png)

Dentro de cada pasta há arquivos com testes mais específicos, tomando como exemplo a compra, temos testes com compra de um item, compra com quarenta itens e a versão dois (v2) da compra de um item.

![Estrutura de arquivos do teste](/images/teste-automizado-restapi-mocha/2-estrutura-arquivos.png)

Observe que os testes possuem um número sequencial na frente, essa ordem foi colocada na ideia de quando o Mocha executar os testes eles possuírem uma ordem de importância para ser executado.



Os testes são estruturados em duas partes:

1. **Describe**
  a. O _describe_ é a definição do que será testado, no exemplo mostrado é descrito que o teste realizará uma compra com um produto.
2. **Step**
  b. O _step_ é o passo do processo a ser executado no teste. No nosso exemplo o passo buscará o token de login do cliente. Os steps são executados na ordem em que estão escritos, dessa forma sempre que um novo passo for escrito, lembre-se de colocar na ordem em que eles precisam ser executados.

![Conceito do teste](/images/teste-automizado-restapi-mocha/3-conceito-teste.png)


A ideia da estrutura que criamos nos testes é que os os _steps_ possam reutilizar os dados obtidos no _step_ anterior. Então logo no começo, após o _describe_, colocamos todas as variáveis globais que são utilizadas entre os passos. Com o processo sendo programático, fica bem mais fácil passar os resultados de um step para o outro.

![Steps do teste](/images/teste-automizado-restapi-mocha/4-step-teste.png)

Observe que no step _Retrieve (Get) Customer Token_ o token de autenticação é obtido e setado na variável _headers_ **(1)** como a proprierdade _Authorization_ e no step _Retrieve Cart_ o _headers_ **(2)** é utilizado.



Você encontrará na estrutura do projeto a pasta **commons**, a ideia é que existem etapas que entre os fluxos de teste que são idênticas ou muito próximas. Pensando nisso, tudo que pode ser reutilizado é organizado por entidades. Algumas das entidades são: _customer, payment, product, etc_.

![Estrutura Commns com promise](/images/teste-automizado-restapi-mocha/5-commons.png)



Cada _common_ terá em sua estrutura funções que são exportadas para o uso, no exemplo temos o _export_ do método que retorna o token do cliente. As funções que chamam uma API Rest são assíncronas, por isso essas funções terão a anotação de **async**.

E por que async? A resposta é de que precisamos trabalhar com promises! E o jeito mais fácil de trabalhar com promises em Node.JS são com a estrutura async / await, vamos explicar melhor depois a respeito.

![Estrutura Commons com promise](/images/teste-automizado-restapi-mocha/6-estrutura-common.png)

Observou como ficou nosso código? Quando avisamos o Node.JS que o método é async e retornamos uma promise ele sabe que existe uma promessa que será executada e pode levar algum tempo para retornar os dados que requisitamos.

Com nossa promise criada, dependendo do que acontecer na nossa requisição usaremos a função **resolve** para quando der sucesso e **reject** para quando houver erro.



![Rejeição e aceite das promises](/images/teste-automizado-restapi-mocha/7-common-promise.png)

![Conceito do await na promise](/images/teste-automizado-restapi-mocha/8-await-promise-common.png)

Quando usamos a nossa função exportada, sabemos que ela é async, logo avisamos o Node.JS de que é necessário esperar que o processo acabe, escrevendo a frente da chamada da função **await** o Node esperará que a promise seja concluída para dar sequência a execução do nosso código. Lembra do **resolve** que usamos? O Node está esperando que ele seja chamado para continuar a execução. Bacana, né? :grin:



Duas bibliotecas são importantes no nosso processo de validação que nosso teste está retornando o que esperávamos: _Chai e Should_. Através delas podemos verificar se um objeto JSON possui uma propriedade, se o retorno devolvido pela promise é uma string ou um número. Dê uma olhada no exemplo e também recomendo que você acesse a documentação das APIs para entender o que você pode validar com elas.

![Papel do Chai e Should](/images/teste-automizado-restapi-mocha/9-chai-should.png)



Para facilitar a configuração dos testes em múltiplos ambientes, criamos o objeto JSON **env**, que nada mais que é um arquivo de propriedades do ambiente, para que seja simples trocar onde os testes estão rodando. Ah! E repare que passamos para classe _commons_ qual o ambiente está configurado no teste, assim podemos criar e rodar em ambientes diferentes.

![Ambiente](/images/teste-automizado-restapi-mocha/10-enviroment.png)



No projeto atualmente temos dois ambientes configurados, mas fique a vontade para criar o seu próprio arquivo de ambiente com suas necessidades específicas.

![Ambiente](/images/teste-automizado-restapi-mocha/11-local-enviroment.png)



O Mocha possui algumas estruturas para facilitar os testes, visando estrutura BDD, que são os **hooks**. No arquivo de teste ao final inserimos um **after** que exibirá o nosso código do carrinho que foi transformado em código da compra.

Muito massa, né? :grin:

![Ambiente](/images/teste-automizado-restapi-mocha/12-hooks.png)

Através do código da compra poderemos rastrear no hac se todo o processo foi executado como esperávamos.



Para rodar os testes você pode rodar todos de uma vez ou individual.

No terminal na pasta raíz, os seguintes comandos podem ser executados.

### Todos os testes
`$ mocha --recursive --require mocha-steps --timeout 0`

### Individual
`$ mocha test/purchase/2-forty-product.spec.js --require mocha-steps --timeout 0`


Muito massa, né? :grin:

Essa combinação de ferramentas é muito poderosa para tornar os testes muito mais fáceis e divertidos! Espero que te ajude a tornar o processo de testar a API Rest mais tranquilo, como foi para mim. :wink:



Dá uma olhada como fica o teste no final. :smiley:
![Exemplo de execução do teste](/images/teste-automizado-restapi-mocha/13-execucao-teste.png)


