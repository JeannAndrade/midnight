# Editor Vim (Table of Contents)

Este é um resumo do [post](https://www.tutorlinux.com.br/2017/07/12/editor-vim-guia-completo/) disponível no TutorLinux

1. [Abrindo o Editor Vim](#abrindo-o-editor-vim)
1. [Modo de comando](#modo-de-comando)
1. [Modo de inserção](#modo-de-inserção)
1. [Teclas para inserção de texto](#teclas-para-inserção-de-texto)
1. [Salvando e/ou saindo do arquivo](#salvando-eou-saindo-do-arquivo)
1. [Desfazendo e refazendo uma ação](#desfazendo-e-refazendo-uma-ação)
1. [Localização de texto](#localização-de-texto)
1. [Remoção de caracteres](#remoção-de-caracteres)
1. [Copiar e colar](#copiar-e-colar)
1. [Substituição de textos](#substituição-de-textos)
1. [Opções para o comando SET](#opções-para-o-comando-set)
1. [Invertendo maiúsculas/minúsculas](#invertendo-maiúsculasminúsculas)
1. [Modo visual do vim](#modo-visual-do-vim)
1. [Copiando e colando textos no vim (utilizando o mouse)](#copiando-e-colando-textos-no-vim-utilizando-o-mouse)
1. [Comandos mais comuns](#comandos-mais-comuns)

## Abrindo o Editor Vim

| Comando | Descrição |
| ------ | ------ |
| vim | Abre o vim vazio, sem nenhum arquivo e exibe a tela de apresentação |
| vim arquivo | Abre o arquivo de nome “arquivo” |
| vim arquivo + | Abre o arquivo de nome “arquivo”, com o cursor no final do mesmo |
| vim arquivo +10 | Abre o arquivo de nome “arquivo”, com o cursor na linha 10 |
| vim arquivo +/Fulano | Abre o arquivo de nome “arquivo”, na primeira ocorrência da palavra “Fulano” |

 [top](#editor-vim-table-of-contents)

## Modo de comando

Ao executar o vim, ele inicia diretamente em modo de comando. Neste modo você não conseguirá digitar nada no texto, apenas navegar sobre o mesmo ou entrar com algum comando como veremos mais adiante.

Vejamos algumas das principais teclas de movimentação sobre o conteúdo do arquivo no modo de comando:

| Comando | Descrição |
| ------ | ------ |
| Ctrl + f | Passa para a tela seguinte. |
| Ctrl + b | Passa para a tela anterior. |
| H | Move o cursor para a primeira linha da tela. |
| M | Move o cursor para o meio da tela. |
| L | Move o cursor para a última linha da tela. |
| h | Move o cursor para caractere a esquerda. |
| j | Move o cursor para linha abaixo. |
| k | Move o cursor para linha acima. |
| l | Move o cursor para caractere a direita. |
| w | Move o cursor para o início da próxima palavra (não ignorando a pontuação). |
| W | Move o cursor para o início da próxima palavra (ignorando a pontuação). |
| b | Move o cursor para o início da palavra anterior (não ignorando a pontuação). |
| B | Move o cursor para o início da palavra anterior (ignorando a pontuação). |
| 0 (zero) | Move o cursor para o início da linha corrente. |
| ^ | Move o cursor para o primeiro caractere não branco da linha. |
| $ | Move o cursor para o fim da linha corrente. |
| nG | Move o cursor para a linha de número “n” (substitua n pelo número da linha).
| gg | Mome o cursor para a primeira linha do arquivo. |
| G | Move o cursor para a última linha do arquivo. |

[top](#editor-vim-table-of-contents)

## Modo de inserção

Para começar a escrever, pressione “i” em seu teclado. O vim entra em modo de inserção, que você comprova pelo rodapé da tela, onde fica a seguinte marcação:
– – — INSERT —

[top](#editor-vim-table-of-contents)

## Teclas para inserção de texto

| Comando | Descrição |
| ------ | ------ |
| i | insere o texto antes do cursor |
| I | insere o texto no início da linha |
| a | insere o texto após o cursor |
| A | Insere o texto no fim da linha onde se encontra o cursor |
| o | Adiciona uma linha vazia abaixo da linha corrente |
| O | Adiciona uma linha vazia acima da linha corrente |

Pressione a tecla ESC para voltar em modo de comandos

[top](#editor-vim-table-of-contents)

## Salvando e/ou saindo do arquivo

Estando no modo de comando, digite estas combinações para o fim desejado:

| Comando | Descrição |
| ------ | ------ |
| :w | Salva o arquivo que está sendo editado no momento |
| :q | Sai |
| :wq | Salva e sai |
| “:x” (sem aspas) | Salva e sai |
| ZZ | Idem |
| :w! | Salva forçado |
| :q! | Sai forçado |
| :wq! | Salva e sai forçado |

[top](#editor-vim-table-of-contents)

## Desfazendo e refazendo uma ação

É claro que você pode desfazer uma ação que você considera errado, ou que errou ao digitar o texto. É só utilizar: u

Shift+u => Desfaz todas as modificações feitas no arquivo.

Se você precisar voltar o texto na tela, utilize as teclas Ctrl + r.

[top](#editor-vim-table-of-contents)

## Localização de texto

| Comando | Descrição |
| ------ | ------ |
| /palavra | Procura pela palavra ou caractere acima ou abaixo do texto |
| ?palavra | Move para a ocorrência anterior da palavra (para repetir a busca use “n”) |
| n | Repete o último comando utilizando / ou ? |
| N | Repete o último comando / ou ? ao contrário (baixo para cima) |
| Ctrl+g | Mostra o nome do arquivo, o número da linha corrente e o total de linhas |

[top](#editor-vim-table-of-contents)

## Remoção de caracteres

| Comando | Descrição |
| ------ | ------ |
| x | Apaga o caractere onde o cursor estiver |
| dd | Apaga a linha inteira onde o cursor estive |
| D | Apaga a linha a partir da posição do cursor até o fim |
| J | Une a linha corrente à próxima |
| 5dd | Remove as próximas 5 linhas a partir da posição do atual do cursor |(qualquer número) |
| :A,Bd | Deleta da linha A até a linha B e copia para a área de transferência |
| Ctrl + h | Apaga último caractere à esquerda (no modo de inserção) |
| cc | Apaga a linha atual e copia para a área de transferência |
| cNc | Apaga N linhas e copia para a área de transferência |

[top](#editor-vim-table-of-contents)

## Copiar e colar

| Comando | Descrição |
| ------ | ------ |
| yy | Copia a linha onde o cursor se encontra |
| 5yy | Copia as próximas 5 linhas a partir da posição atual do cursor |
| p | Cola o que foi copiado na linha abaixo do cursor atual |
| Np | Cola N vezes o conteúdo da área de transferência |

[top](#editor-vim-table-of-contents)

## Substituição de textos

| Comando | Descrição |
| ------ | ------ |
| rCARACTER | Substitui o caractere onde o cursor se encontra pelo caractere especificado em CARACTERE |
| RTEXTO | Substitui o texto corrente pelo texto digitado (sobrepõe) |
| cw | Remove a palavra corrente para substituição |
| cc | Remove a linha corrente para substituição |
| C | Substitui o restante da linha corrente, esperando o texto logo após o comando |
| J | Une a linha corrente à próxima |
| :s/velho/novo | Substitui a primeira ocorrência de “velho” por “novo” na linha corrente |
| :% s/velho/novo | Substitui em todo o arquivo (%) a primeira ocorrência de “velho” por “novo” em cada linha |
| :% s/velho/novo/g | Substitui em todo o arquivo (%), todas (g) as ocorrências de “velho” por “novo” |
| :% s/velho/novo/gc | Igual ao anterior, mas pedindo confirmação para cada substituição |
| :% s/^String[0-9]//gc | Expressões regulares também funcionam, como no sed |
| :10,20s/^/# | Insere o caractere # no início (^) das linhas 10 a 20 |
| :10,20s/^#/ | Remove o primeiro caractere nas linhas 10 a 20 |
| :% s/./\u&/gc | Converte para maiúsculas (\u) o primeiro caractere (.) de cada linha. |

[top](#editor-vim-table-of-contents)

## Opções para o comando SET

:set
| Comando | Descrição |
| ------ | ------ |
| autowrite aw | Salva a cada alteração |
| backspace bs | Comportamento backspace (1 ou 2) |
| errorbell eb | Campainha de erro |
| expandtab et | Troca tab por espaços |
| fileformat=dos ff | Converte o arquivo para DOS |
| hidden hid | Preserva o buffer |
| hlsearch hls | Ilumina a última procura |
| cursorline | Exibe uma linha onde o cursor se encontra |
| ignorecase ic | Case insensitive na busca |
| incsearch is | Ilumina procura enquanto digita |
| laststatus=2 | Mostra linha de estado |
| lazyredraw lz | Não redesenha em macros |
| lines=N | Número de linhas na tela |
| magic | Usar mágicas na procura de padrões |
| number nu | Mostra núm da linha |
| report=N | Mostra aviso quando N linhas mudaram (0=sempre) |
| showcmd | Mostra o comando que se está fazendo |
| showmatch sm | Mostra o casamento de {},[],() |
| smartcase scs | Assume “noic” quando tiver maiúsculas |
| textwidth=N | Quebra de linha do texto |
| undolevels ul=N | Guarde os N últimos comandos para desfazer (padrão=1000) |
| vb t_vb= | Retira o “beep” de erro |

[top](#editor-vim-table-of-contents)

## Invertendo maiúsculas/minúsculas

| Comando | Descrição |
| ------ | ------ |
| 5~ | Inverte os 5 próximos caracteres |
| g~$ | Inverte todos os caracteres até o fim da linha |
| seleciona, u | Converte para minúsculas |
| seleciona, U | Converte para maiúsculas |
| seleciona, ~ | Inverte |

Observação: Onde está escrito “seleciona”, é para fazer utilizando o modo visual (v).

[top](#editor-vim-table-of-contents)

## Modo visual do vim

Entre no modo visual: v
Agora, utilize as teclas direcionais (setas) do teclado, para selecionar o texto desejado.
Pressione “y para copiar” ou “u” para recortar e cole, utilizando a tecla “p” (paste).
Veja agora como apagar um determinado texto:
Utilizando normalmente as teclas Backspace/Delete, ou entrando em modo visual (v) e pressionando a tecla Delete.
Você pode remover até o final de uma palavra, utilizando: dw
Pode também remover até o final de uma frase: d$

[top](#editor-vim-table-of-contents)

## Copiando e colando textos no vim (utilizando o mouse)

Selecione o texto necessário com o botão esquerdo do mouse. Quando você for colar, saiba que o texto será colado a partir de onde se encontra o cursor (esse que aparece, às vezes piscando e às vezes não, quando você está digitando). Para colar, depois de ter selecionado o texto, você pode utilizar uma dessas opções:

1. Pressionando o botão direito do mouse;
2. Pressionando o botão direito + botão esquerdo juntos;
3. Pressionando o botão do meio do mouse (mouse de 3 botões);

Observação: Lembre-se que o vim deve estar no modo de inserção.

[top](#editor-vim-table-of-contents)

## Comandos mais comuns

| Comando | Descrição |
| ------ | ------ |
| :e arquivo | abre o arquivo |
| :e. | abre o diretório atual para selecionar um arquivo |
| :Vex | abre uma janela vertical para selecionar um novo arquivo a ser editado |
| Ctrl+w seguido de v | abre uma janela vertical |
| Ctrl+w seguido de s | abre uma janela horizontal |
| Ctrl+w seguido de n | abre uma nova janela horizontal |
| :ce | alinhamento centralizado |
| :ri | alinhamento a direita |
| :le | alinhamento a esquerda |
| :new | abre nova janela |
| :n ou :next | vai para próximo arquivo (quando utilizado vim file1 file2) |
| :prev ou :previous | vai para arquivo anterior (quando utilizado vim file1 file2) |
| :split | divide a janela atual em duas |
| :split arquivo | abre o arquivo em nova janela |
| Ctrl+w+k | ir para janela superior |
| Ctrl+w+j | ir para janela inferior |
| Ctrl+w Ctrl+w | alternar entre janelas |
| :! | Permite executar um comando do shell e retorna ao vim (Ex: :!ls = executa o comando ls e retorna ao vim) |
| :.! | Executa um comando no shell e insere a saída no vim abaixo do cursor (Ex: :.!ls = executa o comando ls e insere a saída no vim) |
| :r! | Executa um comando no shell e insere a saída no vim acima do cursor (Ex: :r!ls = executa o comando ls e insere a saída no vim) |
| :quit ou :q | Fecha |
| :quit! ou :q! | Fecha sem gravar |
| :w | Salva o arquivo |
| :w arquivo | salvar arquivo como |
| :wq | Salva e fecha |
| :exit ou “:x” (sem aspas) | Fecha e grava se necessário |
| :help | ajuda do VI |

[top](#editor-vim-table-of-contents)
