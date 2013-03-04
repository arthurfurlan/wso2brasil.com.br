---
author: Leonardo Saraiva
date: '2009-11-26 07:00:27'
layout: post
slug: soa-esta-para-wso2-ou-wso2-esta-para-o-soa
comments: true
status: publish
title: SOA está para WSO2 ou WSO2 está para o SOA?
categories:
- arquitetura
tags:
- arquitetura
- código aberto
- definição
- soa
- software livre
- wso2
---

Um toque do [Nivaldo](http://www.nivaldoarruda.com.br) e percebi a necessidade
de explicar melhor o que são os softwares que comento por aqui. Para tentar
suprir essa necessidade dos "perdidos" que por acaso venham parar por aqui,
farei alguns posts mais explicativos e menos práticos (assim digamos).

E para começar vou tentar explicar o que o WSO2 representa para o SOA e o que
o SOA representa para o WSO2, mas antes disso preciso explicar um pouco o que
é cada um dos dois, então vamos lá:

**[WSO2](/glossario/#WSO2):** Segundo o [site](http://www.wso2.org) da plataforma (tradução livre): "Produtos de código-livre integrados e modulares que dão suporte para criação de uma plataforma SOA, suprindo a parte de criação, conexão, composição e governança de serviços".
**[SOA](/glossario/#SOA):** É uma estratégia que propõem organizar os ativos de software de forma que eles possam representar processos, atividades ou tarefas de negócio de forma direta. Tais representações são chamadas de serviço, que devem ser baseadas em padrões e facilmente combinados e reutilizados visando a satisfação dos requerimentos de negócio (para uma explicação um pouco mais detalhada, ver [aqui](http://www.ici.curitiba.org.br/exibirArtigo.aspx?idf=13), valeu AC!).

E o que eu quero dizer com tudo isso? Digamos que para implementar e implantar
SOA necessitamos escolher uma arquitetura e nesse ponto a participação do WSO2
é muito importante. Pois alguns outros produtos tentam impor a arquitetura,
diferente do WSO2, que dá a opção de você montar todo esse "quebra-cabeça" da
forma que bem entender.

[![Arquitetura SOA (pequeno quebra-cabeça)](http://assets.mcorp.com.br/wp-content/uploads/2009/11/arquitetura-soa-300x225.png)](http://assets.mcorp.com.br/wp-content/uploads/2009/11/arquitetura-soa.png "Arquitetura SOA (pequeno quebra-cabeça)")

E agora, nessa arquitetura de exemplo mostro onde encaixam alguns dos produtos
do WSO2:

[!["Arquitetura SOA com WSO2"](http://assets.mcorp.com.br/wp-content/uploads/2009/11/arquitetura-soa-with-wso2-300x225.png)](http://assets.mcorp.com.br/wp-content/uploads/2009/11/arquitetura-soa-with-wso2.png "Arquitetura SOA com WSO2")

É claro que no decorrer do desenvolvimento do projeto, algumas coisas podem ir
se acertando. Até porque essa arquitetura que utilizei como exemplo não é a
ideal para todo e qualquer caso, tudo deve ser pensado com muita calma.

Existem outros produtos na plataforma que não estão mostrados na imagem acima
e que em determinados casos podem (e devem) ser utilizados. Mas quis passar
somente um pouco do que o WSO2 representa nesse mundo da sopa de letrinhas que
é o mundo SOA.

Com o tempo vou tentar explicar cada uma das "caixinhas" e como cada um dos
produtos se comporta para suprir essa necessidade.

