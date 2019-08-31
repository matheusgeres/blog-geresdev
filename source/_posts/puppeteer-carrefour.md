---
title: Teste automatizado com Puppeteer no site do Carrefour
date: 2019-08-30 21:12:30
tags:
    - Puppeteer
    - NodeJS
    - Javascript
    - Teste automatizado
    - Chrome
---
{% img /images/puppeteer-carrefour/puppeteer.png "Puppeteer Logo" 500  %}

# O que é o Puppeteer?
Puppeteer é uma biblioteca Node que permite um acesso alto nível a API de controle do Chrome ou Chromium headless (sem interface gráfica) através do protocol DevTools. Ele pode ser usado também de forma completa (não headless) tanto com o Chrome quanto com o Chromium.
<!-- more -->
## O que podemos fazer com o Puppeteer?
- Gerar prints e páginas PDF. 
- Acessar uma SPA (Single-Page Application) e gerar uma pré-renderização do conteúdo, por exemplo, "SSR" (Server-Side Rendering).
- Automação de envio de formulário, Teste de interface, digitação (input) do teclado, etc.
- Criar um teste com as tecnologias mais recentes para web, automatizando o teste no ambiente, rodando testes na última versão do Chrome e JavaScript. 
- Capturar a linha do tempo de execução do site para ajudar no diagnósticos de problemas de performance. 
- Testar extensões do Chrome.

# O que me motivou a criar um teste automatizado no Chrome?
Quando eu fiz o meu primeiro teste com {% post_link teste-automizado-restapi-mocha "Mocha em REST API"  %} para o Carrefour me perguntei se não era possível fazer o mesmo, porém navegando pelo site, fazendo login, selecionando produtos, digitando os dados do cartão e fechando a compra. Para a minha surpresa, tudo isso foi possível e não somente isso, dá para fazer testes automatizados bem inteligente, unindo outras ferramentas. É uma delicinha ver tudo isso funcionando! :heart_eyes:

# Mãos na massa!
Parece difícil? :confounded:
![Hands-on  Exemplo do uso do Puppeteer](/images/puppeteer-carrefour/1-handson.png)
É bem simples! :sweat_smile:

Apenas uma biblioteca é necessária para usar o Puppeteer.
![Lib do Puppeteer](/images/puppeteer-carrefour/2-biblioteca.png)

Para iniciar o Puppeteer passamos a informação se será executado headless e se é para ignorar os erros HTTPs
![Instância do Chrome](/images/puppeteer-carrefour/3-instancia-chrome.png)

Abrimos uma aba do Chrome.
![Abrir aba do Chrome](/images/puppeteer-carrefour/4-aba-chrome.png)

Definimos qual será o tamanho da tela onde o teste será executado.
![Tamanho da tela](/images/puppeteer-carrefour/5-tamanho-tela.png)

Com a ajuda do poderoso async / await, podemos escrever funções como essas, delegando para outra parte de nosso teste a resposabilidade por executar alguma determinada ação.
![Chamadas async / await](/images/puppeteer-carrefour/6-asyc-await-metodos.png)

Com a page que criamos, navegamos para a tela de login e com o id dos componentes de login, o usuário e senha são digitados.
Em seguida o botão de login é clicado.
![Função de login](/images/puppeteer-carrefour/7-funcao-login.png)

A função que adiciona o primeiro item da categoria considera através do seletor CSS o primeiro filho da lista de itens que são exibidos na tela e clica para adicioná-lo.
![Função que adiciona primeiro item da lista](/images/puppeteer-carrefour/8-funcao-adiciona-item.png)

Um dos recursos mais utilizados e necessários para testes automatizados são os “wait”, a partir dele informamos ao teste aguardar por algum tempo, função, resposta de requisições, etc.
![Função "wait"](/images/puppeteer-carrefour/9-funcao-wait.png)

No _place order_ temos o maior fluxo de interação com a tela, o teste clica em botões, aguarda respostas, digita dados de cartões, seleciona combos e finaliza a compra.
![Fluxo de Place Order](/images/puppeteer-carrefour/10-fluxo-compra.png)

Link do repositório: https://github.com/matheusgeres/carrefour-test-chrome-headless
Aproveita e me segue por lá no [Github](https://github.com/matheusgeres/). :wink:

Demonstração em vídeo do teste automatizado executando e realizando uma compra.
<div class="video-responsive">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/dPsXPqW1gcs" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

Se ficou alguma dúvida, só escrever aqui embaixo nos comentários. :grin: