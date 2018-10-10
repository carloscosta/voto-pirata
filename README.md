# Decisões distribuídas a.k.a. ``dd``

Este documento descreve um sistema para tomadas de decisão distribuídas em grupos 
horizontais usando principios de democracia líquida, ou seja baseada em um modelo 
de representação dinâmica onde as pessoas podem votar livremente em seu gráfico social 
em quem eles querem ter como representantes (amigos, colegas, família), para um conjunto 
específico de tópicos (*tags*). Democracia Líquida é a forma mais flexível de 
governança democrática que pode ser construída com tecnologia digital, operando como 
um híbrido que possibilita votação direta ou delegada a qualquer momento.

## Token Vote

Um sistema de decisão ideal deve ser capaz de satisfazer, na maior medida possível, estas condições:

* Anonimato (sigilo): o usuário deve poder votar em segredo.
* Passível de Verificabilidade: o usuário deve ser capaz de verificar o registro do voto.
* Líquida: O usuário pode escolher no sim, não, em alguém (delegar) e pode não escolher nada (abstenção).
* Tempo limitado para tomada de decisão.
* Integridade: o sistema deve ser capaz de verificar a contagem correta de votos.

Além disso, devido ao risco de coerção através de violência física ou ameaças em contextos 
propensos à violência política, uma opção capaz de proteger os eleitores coagidos deve ser introduzida:

* Resistência: o eleitor deve ser capaz de anular o próprio voto, se necessário.

No trabalho liderado pelos pesquisadores Hosp & Vorai[1], uma abordagem da Teoria da Informação foi 
tomada para modelar os sistemas de votação, levando à conclusão de que existe uma tensão natural
com um sistema que visa integridade perfeita, perfeito sigilo e perfeita verificabilidade. Todos 
os três não podem ser alcançados simultaneamente quando o adversário é computacionalmente ilimitado, 
capaz de forçar um sistema se o tempo for ilimitado ou houver memória disponível. Por essa razão, 
consideramos indispensável implementar democracias digitais usando *blockchains*. 

Com os efeitos de rede já em vigor, os blockchains são capazes de verificar a integridade das transações e evitar 
o gasto duplo do *token*. Além disso, o blockchain não é seguro em uma rede assíncrona, mas é seguro e 
ativo (para contagem de confirmação) em uma rede parcialmente síncrona como a Internet. O modelo de prova 
de trabalho do Bitcoin consegue isso premiando a capacidade computacional de verificar os blocos de transação 
(o que geralmente é chamado de mineração). Por essa razão, nosso *design* é baseado em *tokens* dentro de uma 
rede blockchain operando como crypto-política.

O que diferencia um voto do dinheiro (ou em termos mais amplos: uma economia política de uma economia financeira) 
é que a moeda política é projetada para garantir os direitos de participação em condições justas a todos os membros
de uma organização. Os direitos visam satisfazer a legitimidade geral na governança de uma instituição. Enquanto 
o dinheiro é a linguagem do interesse próprio, os votos expressam as visões compartilhadas de uma comunidade. 
A moeda política não é estritamente destinada ao comércio, mas à escolha social.

Neste contexto, o *token* de votação visa ser um padrão para a democracia digital capaz de interoperar com outros *tokens*, 
estabelecendo uma linguagem comum para a governança de organizações baseadas em blockchain. 
Dentro do contexto das democracias líquidas, uma série de transações de votação é permitida com votos:

* Voto Direto: É permitido ao usuário usar seus *tokens* para votar diretamente em questões como em uma democracia direta.
* Delegação Básica: Usuário A pode delegar votos para B. Enquanto B tiver acesso a esses tokens, ele poderá usá-los para votar em nome de A.
* Delegação Limitada de Tag: usupario A pode delegar votos a C sob a condição especificada de que C só pode usar esses tokens em problemas 
  com uma tag específica. Se a delegação especificar que os votos delegados só podem ser usados em decisões com a tag ``#environment``, C 
  não poderá usá-los em nenhum outro lugar, exceto nesses problemas específicos. Isso leva a um modelo de representação não baseado no território, 
  mas no conhecimento.
* Delegação transitória: Se B recebeu votos de A, ele pode delegar isso para F. Isso gera uma cadeia de delegações que ajuda a capacitar atores 
  específicos dentro de uma comunidade. Se A não desejar ter terceiros recebendo os votos que ela delegou a B, ela poderá desativar a configuração 
  transitiva do contrato de delegação. Delegações circulares (por exemplo, A recebendo os tokens que ela enviou ao B por meio de  F) são proibidas 
  desde que a alocação original de votos de uma organização para seus membros tenha uma assinatura indicando quem é o proprietário soberano dos votos.
* Votação primordial: Se B já usou os votos delegados que recebeu de A, mas A tem uma opinião diferente sobre uma determinada questão, como a proprietário 
  soberana de seus votos, A sempre pode anular a decisão de B. Os eleitores sempre têm a palavra final sobre qualquer decisão com seus votos originais.
* Votação Pública: Muitas vezes referida como a regra de ouro das democracias líquidas, todos os delegados têm o direito de saber como seu delegado votou
  em qualquer questão com seus votos. Da mesma forma que os votos congressistas são públicos, em democracias líquidas competidores delegados em qualquer *tag*
  têm um incentivo para construir uma reputação pública baseada em seu histórico de votação, a fim de atrair mais delegações.
* Voto Secreto: Um método capaz de garantir transações de voto não rastreáveis ao eleitor. Isso é indispensável em contextos de eleições públicas realizadas 
  em grandes populações que apresentam alto risco de coerção. Mesmo se o sigilo perfeito na transação do voto for alcançado, os usuários ainda poderão ter 
  impressões digitais com metadados expostos. Por essa razão, pesquisas sobre integração com blockchains projetadas para transações anônimas com um histórico 
  comprovado são encorajadas. Isso pode incluir uma taxa de mineração para liquidar a transação de voto que pode ser subsidiada pela organização executora ou 
  paga diretamente pelos eleitores.

### Requisitos desejados no futuro

* Conhecimento minimo - servidor com informacoes encriptadas.

## Partes

### Cliente

### Servidor

## Estudo de casos e os problemas

### Caso 1 - servidor e criptografia.

#### Preparacao
1. Um usuario pede pro cliente `dd` pra iniciar uma tomada de decisao sobre um assunto.
2. O app pede pro usuario entrar com informacoes sobre o que deve ser decidido:  
  a. O assunto e notas de informacao.  
  b. Quantas pessoas envolvidas, seus nomes e seus e-mails  
  c. Quantas pessoas precisam aprovar o processo de contagem das decisoes individuais.  
  d. Quando a decisao deve ser tomada.  

3. O App manda as informacoes pro servidor.
4. O servidor poe as informacoes relevante a decisao a ser tomada num banco.
7. O servidor gera um par de chaves GPG
9. Usa `shamir shared secret` para dividir a chave privada entre todos os participantes 
10. Servidor manda e-mail para os usuarios envolvidos na tomada de decisao: informacoes sobre o assunto a ser decidido, a chave publica GPG e as `shares` da chave privada.
11. Servidor deleta todas as chaves.

#### Tomando a decisao
1. Usuario recebe um e-mail com uma URL para entrar no App direto no assunto a ser decidido. Recebe tambem a chave publica do  e a `share`.
2. Usuarios tambem recebem a lista de nomes das outras pessoas involvidas nas decisoes.
3. Usuario decide em sim, nao ou em alguem. Usuario tambem nao precisa decidir.
4. App do usuario encripta a decisao com chave publica e o envia.
5. Usuarios podem mudar a decisao ateh o final do periodo maximo para tomada da decisao.

#### Contagem
Quando o tempo se esgota comeca a contagem
1. Servidor manda mensagem aos participantes para enviar suas `shares` como uma forma de concordar na contagem - no central authority.
2. Recebendo o numero minimo de `shares` o servidor recupera a chave GPG privada, decripta e calcula a decisao mais escolhida.
3. O servidor broadcast o resultado, mantem as decisoes individuais encriptadas e o resultado, mas deleta a chave privada e as decisoes decriptadas.
4. As decisoes podem ser recontadas.

#### Problemas e solucoes
1. Servidor sabe como as pessoas decidiram por pelo menos um instante  
  a. Se usar encriptacao homomorfica daria para nao precisar decriptar cada decisao.  
  b. Porem, nao conheco encriptacao homomorfica que funcione para decisao distribuida(explica aih!!!)  

2. Servidor age como centralizador de informacao - e se o servidor cair?  
  a. Pode usar blockchain tech para armazenar as decisoes... se o servidor cair, dah pra recuperar as decisoes da blockchain, a chave privada e revelar as decisoes na unha (mas... precisaria que encriptacao homomorfica funcionasse).
  
  
### Caso 2 - FLO blockchain e shamir

#### Preparacao
1. Um usuario pede pro cliente `dd` pra iniciar uma tomada de decisao sobre um assunto.
2. O app pede pro usuario entrar com informacoes sobre o assunto a ser decidido:  
  a. O assunto e notas de informacao.  
  b. Quantas pessoas envolvidas, seus nomes e seus e-mails  
  c. Quantas pessoas precisam aprovar o processo de contagem das decisoes individuais.  
  d. Quando a decisao deve ser tomada.

3. O App manda as informacoes pro servidor que poe as informacoes relevante a decisao a ser tomada num banco.
4. O servidor gera um endereco de FLO associado a cada pessoa decidindo e manda 0.1 FLO pra cada endereco.  
  a. A tabela de relacionamento entre enderecos FLO e pessoas decidindo tem o endereco FLO 
5. O servidor gera um endereco pra sim e outro pra nao com zero FLOs.
6. Servidor manda e-mail para os usuarios envolvidos na tomada de decisao: informacoes sobre o assunto a ser decidido e a lista de pessoas envolvidas na tomada de decisao.

#### Tomando a decisao
1. Usuario recebe um e-mail com uma URL para entrar no App direto no assunto a ser decidido.
2. Usuarios tambem recebem a lista de nomes das outras pessoas envolvidas na tomada de decisao.
3. Usuario decide em sim, nao ou em alguem. Usuario tambem nao precisa decidir.
4. O app pede pro servidor executar a transacao de FLO do seu endereco para onde deve ir a decisao.
5. O servidor verifica se o endereco de destino jah executou a transacao ou nao.  
  a. Se sim, verifica se o endereco de destino da transacao feita pelo endereco de destino original executou a transacao, repete.  
  b. Se nao, executa a transacao diretamente para o endereco de destino final.
  
>Alternativa: Servidor executa transacao para o endereco de destino e verifica se o endereco de destino jah executou alguma transacao.  
  a. Se sim, executa outra transacao do endereco original para o novo endereco de destino.  
  b. Se nao, para.

6. Servidor manda identificador da transacao como recibo de voto

#### Contagem

1. Conta-se o numero de FLOs nos enderecos de sim e nao
2. Todas as moedas distribuidas sao retornadas ao endereco do servidor.

#### Problemas:
1. Nao pode mudar de decisao.
2. Nao eh anonimo.
3. varios outros.

[1]: https://www.semanticscholar.org/paper/An-Information-Theoretic-Model-of-Voting-Systems-Hosp-Vora/24d55c866a7317dae11d37518b312ee460bc33d3 "An Information-Theoretic Model of Voting Systems"
