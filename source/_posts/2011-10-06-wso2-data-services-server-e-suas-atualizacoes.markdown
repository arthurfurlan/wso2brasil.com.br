---
author: Leonardo Saraiva
date: '2011-10-06 15:58:00'
layout: post
slug: wso2-data-services-server-e-suas-atualizacoes
comments: true
status: publish
title: WSO2 Data Services Server e suas atualizações
categories:
- desenvolvimento
tags:
- código aberto
- data services
- dss
- mysql
- oracle
- postgresql
- soapui
- software livre
- sql server
- testes
- wso2
- wso2 carbon
---

[![](http://assets.mcorp.com.br/wp-content/uploads/2011/10/testes-e-a-neura.jpg)](http://assets.mcorp.com.br/wp-content/uploads/2011/10/testes-e-a-neura.jpg)

Se tem uma tarefa que toma muito tempo nosso, são os testes quando sai versão nova de algum produto do [WSO2](http://wso2.org).

Estamos trabalhando na migração do [WSO2 Data Services Server](/tag/data-services/) [2.5.1](/2010/04/novidades-do-proximo-wso2-data-services-server-2-5-x/) para a [2.6.0](/2011/06/novidades-wso2-data-services-server-2-6-x/) e isso gera uma árdua tarefa de testar todos os serviços que temos rodando, que rodam com diferentes banco de dados ([MySQL](http://dev.mysql.com), [PostgreSQL](http://www.postgresql.org), [SQL Server](http://www.microsoft.com/sqlserver/), [Oracle](http://www.oracle.com/br/)).

Na maioria das vezes não encontramos problema algum ou apenas uma pequena
mudança de atributo ou _tag_ na definição dos .dbs. Mas as vezes encontramos
problemas que fogem da simples configuração do data service, e como aconteceu
agora conosco: um _bug_.

Para tentar minimizar esse trabalho gerei um projeto que tem a ideia de
automatizar ao máximo esse tipo de trabalho! E, para com isso, irmos além dos
testes unitários que são realizados pelo pessoal do desenvolvimento do WSO2,
testar as interfaces em real funcionamento, nos mais variados bancos de dados.

E assim nasceu o pequeno projeto [wso2-ds-tests](http://github.com/WSO2Brasil/wso2-ds-tests). Que é um apanhando de data
services, sql's e projeto do [SOAPUI](http://www.soapui.org/). Para maiores
informações basta [acessar o projeto](http://github.com/WSO2Brasil/wso2-ds-tests) no [Github](http://github.com)!

Deem uma olhadela por lá e qualquer contribuição é muito bem vinda, basta
fazer um _fork_ e mandar um _pull request_.
