---
slug: ferramentas-soa-open-source
publish: true
title: "Ferramentas SOA Open Source"
kind: article
created_at: 2010-05-19 19:18:31 UTC
author: Leandro Prado
layout: post
external-url: http://www.leandroprado.com.br/2010/05/ferramentas-soa-open-source/
categories:
- arquitetura
tags:
- wso2
- jboss
- esb
- greg
- bam
- wsas
- dss
- soa
---

Quando decidimos criar um ambiente SOA, um dos requisitos impostos pela maioria dos diretores é se é uma solução livre, ou seja, OpenSource. Partindo desse pré-requisito, pesquisamos algumas ferramentas que poderíamos utilizar.

A primeira ferramenta que testamos foi o Intalio, que, na verdade, é uma ferramenta de BPM em que podemos modelar os processos em BPEL e depois fazer um deploy como um serviço para expor na BUS. Um dos problemas que encontramos com essa ferramenta, foi que não conseguimos levantar uma excessão e retornar para o usuário.

Também estudamos o Mule, que é uma BUS para expor todos os serviços criados a partir do Intalio.

Outra opção foi o JBOSS SOA Plataform; chegamos a fazer um piloto com consultores da Red Hat, porém não supriu todas as nossas necessidades, tinhamos os mesmos problemas da ferramenta Intalio.

Até que descobrimos uma ferramenta chamada WSO2, a qual possui várias ferramentas para SOA como DataServices, Business Process Server, Web Services Application, Governance Registry, Enterprise Service Bus, etc.

A grande vantagem de usar o WSO2 é que temos um grande suporte em fóruns, e-mail, acesso ao código-fonte e atualizações frequentes de suas ferramentas, isso significa que os desenvolvedores estão aprimorando cada vez mais cada uma das ferramentas.

Outra grande vantagem é a sua fácil instalação, na maioria das vezes é necessário somente descompactar a pasta e iniciar o serviço que o servidor já está funcionando.

Atualmente estamos usando DataServices, Web Services Application, Governance Registry e Enterprise Service Bus, todos rodando em um mesmo servidor, porém em portas diferentes.

Veja abaixo a solução completa que o WSO2 implementa.

<a href="http://www.leandroprado.com.br/wp-content/uploads/2010/05/product-platform.gif"><img class="aligncenter" src="http://www.leandroprado.com.br/wp-content/uploads/2010/05/product-platform.gif" title="Plataforma WSO2" alt="Plataforma WSO2" /></a>

Nos próximos posts vou explicar a funcionalidade de cada produto.
