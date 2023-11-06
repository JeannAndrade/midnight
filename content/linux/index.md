---
layout: internal
---

# Principais comandos do terminal do Linux

Foram usados como fonte:

- [Diolinux](https://www.youtube.com/watch?v=QZ2nyxzZXPY)
- [Guia Linux](https://guialinux.uniriotec.br/)
- [Oh My Zsh: usando um terminal personalizado e produtivo!](https://blog.betrybe.com/ferramentas/oh-my-zsh/)

## Table of Contents

1. [Lista dos comandos principais](#lista-dos-comandos-principais)
1. [Instalando o Oh My Zsh no Linux](#instalando-o-oh-my-zsh-no-linux)

## Lista dos comandos principais

| Símbolo | Descrição |
| ----------- | ----------- |
| ls | comando de listagem para ver conteúdo de uma pasta (ls -al para formato longo)|
| man | dá acesso ao manual do comando. Ex man ls |
| clear | limpar o terminal (pode ser o control + L) |
| mkdir | Criar uma pasta. Se quiser criar várias pastas, separar com espaço os nomes delas |
| cd | Navegar entre pastas |
| pwd | imprimir a pasta de trabalho |
| whoami | quem é o usuário atual |
| Redirecionadores | redireciona a saída de um comando para outro. Ex. whoami >> diolinux.txt |
| criar e acessar pasta com nome composto | englobar o nome composto entre " ou ' |
| touch | usado frequentemente para criar arquivo |
| nano | editar arquivo de texto |
| cat | ler documentos pequenos. Ele pega o conteúdo do arquivo e exibe no terminal |
| mv | renomear um arquivo |
| cp | copiar um arquivo. Ex. cp origem destino |
| find | encontrar aquivos dentro de pastas. `find . -name curso_de_terminal.txt` |
| head & tail | ler as primeiras linhas de um arquivo. Ler as ultimas linhas de um arquivo |
| less | carrega somente uma parte do aquivo e vc pode ir descendo para ver o restante |
| rm | remover um arquivo |
| rmdir | remover diretórios, somente diretórios vazios |
| rm -rf | remove diretórios quando não está vazio |
| hostname | lista o nome da máquina |
| hostname -i | vai listas os IPs da máquina |
| ip a | lista os IPs da máquina e mac e outras info |
| grep | filtra a informação. Ex ip a \| grep inet  |
| ping | verifica se está havendo comunicação com outras máquinas |
| free-h & free-m | verifica o uso da memória da máquina |
| top | é como se fosse o monitor do sistema, só que mais simplificado |
| htop | mesmo que o top, só que mais formatado para humanos |
| ps | listas os processos rodando no terminal. Ex.: `ps -elf`  |
| ps aux | lista os processos do sistema, geralmente é usado com o filtro grep. ps aux \| grep gnome-terminal |
| pgrep | já é a combinação do ps com o grep. Ex. pgrep gnome-terminal |
| kill | serve para gerenciar processos. Matar o processo |
| df -h | lista os recursos de dados do sistema |
| ncdu | escaneia a pasta e indica em quais locais existem mais arquivos |
| uname | lista o kernel do Linux |
| lscpu & lsusb | mostra informações a respeito dos dispositivos |
| history | lista os comandos jã executados no terminal |

[top](#table-of-contents)

## Instalando o Oh My Zsh no Linux

### Instalando o Zsh

`sudo apt-get install zsh`

### Tornando o Zsh o shell padrão

`chsh -s $(which zsh)`

Depois de aplicado o comando, reinicie o terminal

### instalando o Oh My Zsh

`sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`

### Instalando as [fontes powerline](https://github.com/powerline/fonts)

`sudo apt-get install fonts-powerline`

### Instalando o pluging [Zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)

O que faz? Realça os comando enquanto são digitados. Se estiver escrito errado ficará em vermelho, se certo ficará em verde

`git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting`

### Instalando o plugin [FZF](https://github.com/junegunn/fzf)

O que faz? possibilita a pesquisa de arquivos e pastas pelo terminal de forma simples e rápida, além de comandos já digitados. Para pesquisar arquivos e pastas, basta pressionar as teclas CTRL + T + nome do arquivo e, para pesquisar por comandos, digite CTRL + R + comando desejado.

`git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf`

`~/.fzf/install`

### Instalando o plugin [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)

O que faz? faz a sugestão de comandos com base no que já foi digitado

`git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions`

### Instalando o plugin [k](https://github.com/supercrabtree/k)

O que faz? Exibe detalhes como a data de criação, o tamanho e as permissões de uso de arquivos e pastas. Digite 'k' em qualquer pasta para ver o resultado.

`git clone https://github.com/supercrabtree/k $ZSH_CUSTOM/plugins/k`

### Registrando os novos plugins no arquivo .zshrc

- Abra o arquivo .zshrc com o comando `sudo nano ~/.zshrc`
- Altere a linha ZSH_THEME="robbyrussell" para ZSH_THEME="eastwood"
- Adicione o zsh-syntax-highlighting a lista de plugins `plugins=(git zsh-syntax-highlighting fzf zsh-autosuggestions k)`

[top](#table-of-contents)
