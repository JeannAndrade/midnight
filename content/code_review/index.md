---
layout: internal
---

# Code Review (Table of Contents)

Este é um resumo do curso [Code Review: Best Practices](https://www.pluralsight.com/courses/code-review-best-practices) by Andrejs Doroninss at Plural Sight.

1. [Estabeleça um Processo de revisão](#estabeleça-um-processo-de-revisão)
1. [Envie bons Pull Requests](#envie-bons-pull-requests)
1. [Envie bons feedbacks como revisor](#envie-bons-feedbacks-como-revisor)
1. [Situações desafiadoras durante a revisão de código](#situações-desafiadoras-durante-a-revisão-de-código)

## Estabeleça um Processo de revisão

### Concordar com coisas fundamentais

- Deve existir um guia de estilo padronizado e documentado para toda a equipe.

- Crie um arquivo de configuração importável para cada uma de suas IDEs.

- Distribua esse arquivo de configuração para os membros da equipe, de forma que a equipe use o estilo padronizado mesmo que de forma inconsciente.

- A ideia é evitar discussões que refletem preferências pessoais e acabam atrasando a entrega do código em produção.

### Ferramentas automatizadas

- As IDEs atuais já dispõe de formatadores de código, analisadores de código e outras funcionalidades para evitar que a equipe perca tempo revisando estilo de codificação.

- Uma dessas ferramentas é o sonarlint

### Atitudes corretas

- Ao menos 2 revisores precisam aprovar o código, sendo que obrigatoriamente um dele deve ter conhecimento da lógica do sistema e seu requisitos. O outro revisor pode focar apenas na qualidade do código.

- A revisão de código pode ser feita por qualquer um da equipe, não importa a sua senioridade. Um Junior pode e deve revisar o código escrito por um sênior e isso deve ser tratado como uma oportunidade para colaboração e mentoria. Esse comportamento diversifica o entendimento do código.

- Tente não impor soluções que são apenas uma preferência. Melhores práticas podem ser colocadas na mesa mas outras soluções, se corretas, também devem ser aceitas.

- A revisão de código deve ser algo que leve horas e não dias.

 [top](#code-review-table-of-contents)

## Envie bons Pull Requests

### Espere por comentários em seu código

A menos que sua mudança seja muito simples, com apenas uma linha de código alterada, espera por comentários e colaboração. Esse é o mindset esperado de um sênior.

Não receber nenhum comentário em um PR atrás do outro PR não é uma situação normal. O normal é que seu PR receba comentários antes de ser aprovado.

### O código é do time

Ao receber um comentário, não fique na defensiva achando que seu trabalho de vários dias foi questionado. Entenda que o código pertence ao time e que outra pessoa precisará entender e manter este código, portanto caso algo não esteja prontamente entendível no código que vc escreveu, ele deve ser questionado por seus colegas.

### O PR deve ser pequeno

Defina com sua equipe o significado de pequeno. Por ser um limite máximo de linhas de código ou de arquivos. A equipe deve concordar com este critério.

Os benefícios são:

- São mais fáceis de revisar
- Mais fácil de encontrar um bug ou problema
- O concerto é mais rápido
- O merge é mais rápido
- Menor o número de conflitos

Para contornar o problema vc pode dividir o PR em outros pequenos e ordenados PR ou dividir a tarefa em sub-tarefas, fazendo um PR para casa divisão feita na task original.

### Divida as mudanças em vários commits

Não deixe para comitar todo o código alterado de um só vez:

Um exemplo seria:

- Implemente um DTO
- Refatore a função que fará uso deste DTO
- Atualize qualquer outra função que dependa deste DTO

Um guia para commits é: commit atomic self-contained changes

O objetivo é que as ferramentas modernas de revisão permitem que a revisão seja feita por commit, e se cada commit for uma pequena atividade, fica mais fácil entender o objetivo geral da mudança.

### Faça a revisão do seu próprio trabalho

Ao criar um PR, siga estes passos:

- Verifique se todos os testes passaram
- Faça vc mesmo uma revisão final do se próprio trabalho
- Peça por revisão aos seus colegas

### Não explique partes do código nos comentários

Se um comentário foi feito no seu PR solicitando esclarecimento sobre algo, tente melhorar a legibilidade do código, refatore ou coloque um comentário no próprio código caso o que esteja resolvendo seja muito complexo. Explicar o código no comentário do PR não trará ganho algum e provavelmente futuramente outras pessoas terão duvidas semelhantes na mesma parte do código.

### Não ignore nenhum comentário

É uma questão de educação e respeito ao revisor responder a todos os comentários.

Possíveis respostas são:

- Corrigido com sugerido.
- Corrigido.
- Feito.

Não responder pode ser percebido como um esforço foi feito na revisão, mas foi simplesmente ignorado pelo autor do código.

[top](#code-review-table-of-contents)

## Envie bons feedbacks como revisor

### Enquadre os feedbacks em questionamentos ou solicitações

Vc pode renomear essa variável para X?

Esse método poderia ser movido para outra classe?

Considere quebrar essa função em duas outras menores.

### Evite apontar o dedo com "você"

Evite usar termos como "você implementou isso errado.".  Ao invés de citar a pessoa, cite o código, como em: "eu não estou conseguindo entender esse código."

Exemplos:

Você pode refatorar essa duplicação? --> Podemos evitar duplicação aqui?

Você precisa escrever teste unitário para esse código --> Esse código precisa ser coberto por teste unitário.

### Aplique a regra Observação/Impacto/Solicitação

Observação: Essa função parece muito grande

Impacto: Isso faz com que eu tenha dificuldade para entender esse código

Solicitação: Sugiro extrair algumas partes em funções separadas e dar a elas nomes expressivos.

Outro exemplo:

Observação: Essa classe parece estar no lugar errado

Impacto: Será difícil para o time acha-la caso alguém queira usa-la

Solicitação: Considere move-la para outro pacote.

### Ajude com exemplos quando apropriado

Tente aumentar o nível de detalhes:

- Vc pode renomear essa variável?

  - Você pode tornar essa variáveis mais descritiva?

    - Você pode tornar essa variáveis mais descritiva, como {x} ou {y}?

### Não tente resolver todos os problemas

Em um código com muitos pontos de melhoria, tente focar nos dois mais importantes. Caso os demais sejam significantes o suficiente, crie uma task para refatoração subsequente.

A dica é:

- Corrija 1 ou 2 coisas no máximo
- Crie uma task para o resto.

### Use labels

O uso de labels pela equipe pode comunicar a gravidade de um problema encontrado.

Por exemplo: nitpick ou nit indica que o problema encontrado é de pequeno impacto e pode não ser aceito pelo autor do código.

Exemplos:

nit: deveria estar em camelCase

nitpick: deveria estar em camelCase

minor: deveria estar em camelCase

Os labels e suas definições podem ser acordados a nível de equipe.

Nitpick = to find faults in details that are not important

### Ofereça elogios sinceros

Quando encontrar algo que lhe surpreendeu de forma positiva, deixe isso claro para o autor deixando um elogio para o trabalho feito.

### Revisão atômica

Faça a revisão de todo o código de uma vez. Se encontrou 5 problemas, reporte os 5 problemas, espere a correção e depois aprove o PR.

Caso um novo problema grave seja encontrado na nova revisão, reporte-o novamente. Mas não entre no jogo de revisões infinitas tentando refatorar todo o código ou mudando de ideia a cada nova revisão.

O número máximo de iterações de revisão deve ser 2, pois o nível de stress a cada iteração costuma subir

### Não desapareça

Se vc fez uma solicitação de correção, espere pela correção e aprove o código. Uma revisão deve durar horas e não dias. Termine o que vc começou.

[top](#code-review-table-of-contents)

## Situações desafiadoras durante a revisão de código

### Construa relações de confiança

Converse com as pessoas por chat

Converse sobre outros assuntos de interesse e hobbies

Saia para almoçar com os colegas

Se for remoto, faça encontros virtuais ocasionais, para falar de outros assuntos diferente do trabalho.

Relações de confiança fortalecem a comunicação entre as pessoas durante as revisões, uma vez que torna a relação mais leve e amigável.

### Trate as desavenças offline

Quando o revisor e o autor não entram em acordo, o melhor é tratar o problema offline, num encontro face a face, num café ou numa conversa direta um com o outro.

### Lidando com autores e revisores difíceis

Existem pessoas que são dificeis de lidar:

- Alguns querem impor uma solução "sugerida"
- Usam uma linguagem inapropriada nas revisões
- São arrogantes
- Bloqueam o PR

Nestes casos algumas possíveis soluções são:

- Tente uma conversa 1-a-1
- Busque opiniões de fora e siga a opinião da maioria
- Escale para um senior

Se a solução for favorável a vc, ótimo. Se não, aceite e siga em frente

[top](#code-review-table-of-contents)
