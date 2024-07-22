---
title: Configurar fish como shell e colocando um tema minimalista
date: 2024-07-21
tags: 
  - shell
  - bash
  - fish
  - spaceship
  - themes
---
{% img  /images/fish-e-spaceship/logo-fish.gif 500 "Fish Logo" %}
# Instalando fish no Fedora

```bash
sudo dnf install fish
```

# Configurando tema

```bash
curl -sS https://starship.rs/install.sh | sh
```

Adicione ao final do arquivo config.fish

```bash
# ~/.config/fish/config.fish

starship init fish | source
```
Fonte: https://starship.rs/


# Instalando oh my fish (omf) plugin manager

```bash
curl https://raw.githubusercontent.com/oh-my-fish/oh-my-fish/master/bin/install | fish
```
Fonte: https://github.com/oh-my-fish/oh-my-fish


# Instalando plugin para o nvm

```bash
omf install nvm
```
Fonte: https://github.com/derekstavis/plugin-nvm


# Instalando plugin para o sdkman

```bash
omf install sdk
```
Fonte: https://github.com/deather/omf-sdk


# Instalando o plugin para o pyenv

```bash
omf update  # Just in case omf is outdated. Avoids missing the package.
```

```bash
omf install pyenv
```
Fonte: https://github.com/oh-my-fish/plugin-pyenv


# Configurando no Gnome Terminal como Terminal padrão
![Configurando fish como shell padrão](/images/fish-e-spaceship/gnome-terminal-comando.png)

1. Vá em configurações do Gnome Terminal
2. Entre em perfil no que está em uso (no meu caso "Sem nome")
3. Selecione a opção nas abas "Comando"
4. Cheque a opção "Executar um comando personalizado em vez da shell padrão"
5. Insira em "Comando persolinzado": fish

Reiniciando o seu terminal, ele deverá se parecer com isso
![Exemplo Terminal](/images/fish-e-spaceship/gnome-terminal-exemplo.png)
Se você entrar em um projeto git, ele o auxiliará mostrando a branch atual
![Exemplo Terminal com Git](/images/fish-e-spaceship/gnome-terminal-exemplo-git.png)


# Instalando as fontes para os ícones serem exibidos

Baixe as fontes através do link: https://github.com/ryanoasis/nerd-fonts/releases/download/v3.2.1/FiraCode.zip
Se preferir, acesse o site https://www.nerdfonts.com/font-downloads e escolha uma fonte de sua preferência.

*Bônus*
Por padrão o gnome-terminal utiliza as fontes _Source Code Pro_, no caso das NerdFont o nome que você encontrará será _SauceCodePro Nerd Font_, caso você goste das fontes padrões do sistema, baixe através do link a fonte: https://github.com/ryanoasis/nerd-fonts/releases/download/v3.2.1/SourceCodePro.zip

Extraia os arquivos em um pasta e realize o seguintes comandos para copiar todas as fontes e atualizar o cache.
```bash
cp *.ttf ~/.local/share/fonts/
```

```bash
fc-cache -v
```

No Gnome Terminal siga os seguintes passos
![Configurando fonte no Gnome Terminal](/images/fish-e-spaceship/gnome-terminal-fonte.png)

1. Vá em configurações do Gnome Terminal
2. Entre em perfil no que está em uso (no meu caso "Sem nome")
3. Cheque a opção "Fonte personalizada"
4. Selecione a fonte instalada (no meu caso "FiraCode Nerd Font")


# Bônus

Caso você não queira a mensagem de boas vindas a cada vez que você se logar no shell, coloque no arquivo config.fish 
```bash
# ~/.config/fish/config.fish

set -g fish_greeting
```