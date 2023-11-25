---
layout: internal
---

# Guia rápido do aplicativos a se instalar no Ubuntu

## Navegador

Utilizo o Microsoft Edge, então vou começar por ele já que muita coisa depende de senhas e favoritos já cadastrados na minha conta.

Instalação do Microsoft Edge

1. `sudo apt install curl`
1. `curl <https://packages.microsoft.com/keys/microsoft.asc> | gpg --dearmor > microsoft.gpg`
1. `sudo install -o root -g root -m 644 microsoft.gpg /etc/apt/trusted.gpg.d/`
1. `sudo sh -c 'echo "deb [arch=amd64] <https://packages.microsoft.com/repos/edge> stable main" > /etc/apt/sources.list.d/microsoft-edge-dev.list'`
1. `sudo rm microsoft.gpg`
1. `sudo apt update && sudo apt install microsoft-edge-stable`

Caso precisa desinstalar:

`sudo apt remove microsoft-edge-stable`

Após a instalação torne o Edge o navegador padrão e faça login.

## Git

1. Configurar o user.name globalmente [veja comando aqui](https://jeannandrade.github.io/content/git/index.html#configurando-o-git)
1. [Gere a chave](https://jeannandrade.github.io/content/git/index.html#gerando-uma-nova-chave-ssh-e-adicionando-a-ao-agente-ssh) tanto para a conta outlook quanto para gmail
1. Registre as chaves no github, gitlab, bitbuket
1. Crie a estrutura de pastas $repo -> (github, gitlab, bitbuket)
1. Clone os projetos
1. Configurar o user.email localmente

## VS Code

Instale o VS Code a partir da loja e faça login para sincronizar

## Oh My Zsh

Siga o [passo a passo](https://jeannandrade.github.io/content/linux/terminal/index.html#instalando-o-oh-my-zsh-no-linux) para instalar

## Calibre

Segundo o [site do Calibre](https://calibre-ebook.com/download_linux), a instalação deve ser feita através do binário fornecido pela URL listada abaixo. Não deve ser instalado da Loja.

Primeiro foi preciso instalar uma lib chamada libxcb-cursor0:

`sudo apt-get -y install libxcb-cursor0`

Em seguida:

`sudo -v && wget -nv -O- https://download.calibre-ebook.com/linux-installer.sh | sudo sh /dev/stdin`

## .NET SDK

Seguir as instruções da [página oficial](https://learn.microsoft.com/en-us/dotnet/core/install/linux-ubuntu-2310)

`sudo apt-get update && sudo apt-get install -y dotnet-sdk-8.0`

## Docker

O [roteiro](https://jeannandrade.github.io/content/docker/como_instalar/index.html) presente na sessão do Docker deu certo. Seguir também a instrução que comenta um erro comum de instalação.

## Multipass

Para instalar o Multipass, seguir os passos do [site](https://multipass.run/install)

`sudo snap install multipass`
