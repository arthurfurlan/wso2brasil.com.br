---
author: Leonardo Saraiva
date: '2009-11-26 19:08:32'
layout: post
slug: software-livre-codigo-aberto-e-o-mundo-soa
comments: true
status: publish
title: Software livre, código aberto e o mundo SOA
categories:
- arquitetura
- desenvolvimento
tags:
- biztalk
- código aberto
- comunidade
- documentação
- oracle
- software livre
- websphere
- wso2
---

Procurando por suítes SOA é muito comum ouvir falar de Oracle, WebSphere e -
meio de longe - BizTalk. Mas, além de pagas, não são nem um pouco baratas.

Esse preço pode ser na maioria das vezes inviável para empresas de menor
porte, sobrando apenas as soluções de menor porte (e preço) e as opções
livres. E aí sobra pra quem "inventou" a moda, afinal, "quem inventa aguenta".

Dois anos atrás, quando começamos os estudos para implementação de SOA aqui no
trabalho, apanhamos - e muito - com esse problema. Tínhamos que implantar toda
a arquitetura escolhida de maneira barata (entenda: de graça).

Achamos muitas opções que prometiam resolver os problemas, mas que no fim
trazia "N" dificuldades na implementação, desenvolvimento e/ou até instalação.
Tudo parecia meio cru e o que diziam ser as melhores, não passavam de um
serviço e um milhão de arquivos (em sua maioria XML) para serem editados quase
que totalmente manual.

Alguns dos problemas que enfrentamos na maioria das soluções foram:

  * **Documentação**: se não fosse nula, era fraca e muito pouco clara;
  * **Desenvolvimento**: o lançamento de novas versões e correções de bugs eram lentos (sem contar as frases do tipo "na versão Enterprise está resolvido");
  * **Comunidade**: praticamente o mesmo problema da documentação, nula; e
  * **Código aberto**: algumas ferramentas dizem "código aberto", porém abrem uma parte do código (que normalmente doam para a Apache Foundation) e o crucial não, impossibilitando corrigirmos ou descobrimos o que acontece.

A lista acima não diz tudo pelo que passamos e enfrentamos, é apenas um
resumo. Então, após testar algumas ferramentas e utilizar algumas outras,
optamos pelo [WSO2](http://www.wso2.org/), que apesar de não resolver todos
nossos problemas, pelo menos chegou mais perto.

Vamos fazer uma comparação com os problemas listados e o que nos levou a
escolhê-lo:

  * **Documentação**: quando começamos era praticamente nula, mas como eles utilizam outros projetos livres (como: [Apache Synapse](http://synapse.apache.org), [Apache Axis2](http://ws.apache.org/axis2), [Apache Rampart](http://ws.apache.org/rampart) e etc) sem maiores modificações, fica mais fácil achar documentação para o seu problema naquele projeto ou biblioteca e atualmente eles estão melhorando um pouco nisso escrevendo [artigos](http://wso2.org/library) e disponibilizando alguns webcasts grátis;
  * **Desenvolvimento**: os lançamentos de versões está numa velocidade boa e rápida, apenas os bugs ainda peca um pouco, mas olhando o JIRA é possível achar vários _patches_, nos deixando ainda a opção de alterar o código, caso queira;
  * **Comunidade**: é fraca como todos os outros, existe o [fórum](http://wso2.org/forum), mas é somente em inglês; e
  * **Código aberto**: como dito antes, o [código](https://wso2.org/svn/browse/wso2/trunk/) é aberto e você pode alterar a vontade, que pode ajudar na necessidade de resolução de bugs mais críticos.

Pode não ser a solução perfeita, mas foi o que mais nos deixou tranquilos para
trabalhar. Alguns produtos ainda tem muito o que evoluir e alguns estão bem
evoluídos, mas com muito a melhorar. Posso dizer que estamos bem com a opção
que fizemos, mesmo que não tenhamos chego aos 100% de implantação da
arquitetura que pensamos.

