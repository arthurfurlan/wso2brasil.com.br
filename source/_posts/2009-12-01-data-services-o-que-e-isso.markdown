---
author: vyper
date: '2009-12-01 00:41:16'
layout: post
slug: data-services-o-que-e-isso
comments: true
status: publish
title: 'Data Services: O que é isso?'
categories:
- arquitetura
- desenvolvimento
tags:
- data services
- definições
- dss
- wso2
---

!["Já viu algum datacenter assim?"](http://assets.mcorp.com.br/wp-content/uploads/2009/11/server.jpg "Já viu algum datacenter assim?")

Se fisicamente algumas empresas mantém um _datacenter_ como esse acima,
imagine o que não conseguem fazer com relação a "fontes de dados" e, para
tentar minimizar esse problema, o [SOA](/glossario/#SOA) propõe a utilização
do "data services", que não podemos afirmar ser a solução para toda e qualquer
empresa, mas foi a nossa opção e tem nos atendido muito bem.

## Definição

[**Data Services**](/glossario/#DataServices): Camada que fornece acesso às
diversas fontes de dados, podendo essas fontes serem: banco de dados,
planilhas ou arquivos textos.

## Então o que é isso afinal?

Digamos que temos uma maneira de organizar aquela "bagunça" generalizada que
as vezes temos em nossa arquitetura, imagine o seguinte cenário: um sistema
para o RH utilizando SQL Server, o sistema de compras utilizando Firebird, uma
planilha de gerenciamento de projetos em excel e o restante em um ERP próprio
utilizando PostgreSQL.

Analisando esse cenário, aparece o problema de integrar todas essas soluções
e, para não acessarmos diversas fontes de dados, cada um com seu _driver_
específico, utilizamos o [WSO2 Data Services Server](http://wso2.org/projects/data-services-server/java)!

Que - basicamente - funciona como uma camada acima de toda aquela bagunça, com
uma única maneira de acesso (serviços) às várias fontes de dados e sem maiores
dependências, independente da forma dos dados o acesso será o mesmo.

[![WSO2 Data Services - Lista de serviços](http://assets.mcorp.com.br/wp-content/uploads/2009/11/wso2-data-services-list-300x155.png)](http://assets.mcorp.com.br/wp-content/uploads/2009/11/wso2-data-services-list.png)

A tela acima mostra a visão do WSO2 Data Services Server na sua página de
listagem de serviços, com atalhos para o [WSDL](/glossario/#WSDL) (na versões
1.1 e 2.0) e um "try-it", que são as duas formas de acesso aos serviços que
expomos no WSO2 Data Services Server. E com isso teremos uma única fonte para
consultar os dados de nossa empresa, atendendo uma das camadas da arquitetura
que explicamos no post "[SOA está para WSO2 ou WSO2 está para SOA?](http://www.mcorp.com.br/2009/11/soa-esta-para-wso2-ou-wso2-esta-para-o-soa/)".

O desenvolvimento desses serviços é relativamente simples e será abordado em
um próximo post.

Caso esteja sendo muito superficial, aceito comentários e/ou críticas caso
esteja muito rápido.
