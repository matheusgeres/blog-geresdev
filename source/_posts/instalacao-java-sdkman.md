---
title: Instalação do Java no Linux via SDKMAN
date: 2019-08-21 00:30:58
thumbnail: /images/sdkman.png
tags: 
  - linux
  - java
  - sdkman
  - ubuntu
  - linux mint
---
A instalação do Java pode ser facilitada através do SDKMAN, ele configura as variáveis de ambiente e tem
várias versões do java.

Para instalar: https://sdkman.io/install
Já a configuração do Java é bem simples através dos seguintes comandos.

`$ sdk list java`

![Lista dos Javas disponíveis do SDKMAN](/images/print-sdkman-java.png)

Observe que temos várias versões do Java! :smiley:

Você pode instalar a versão do Java que a Amazon disponibiliza ou a do Zulu, que são empresas que criam versões da JDK que respeitam as diretrizes da Oracle e são compatíveis com a JDK da Oracle. Massa né?

Para instalar é super fácil, basta rodar o comando com a versão desejada da JDK.

`$ sdk install java 8.0.212-zulu`

E pronto! O Java está configurado e as variáveis de ambiente setadas! Muito massa, né? :wink: