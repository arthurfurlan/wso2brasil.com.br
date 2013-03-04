---
author: Leonardo Saraiva
date: '2011-06-11 15:39:37'
layout: post
slug: novidades-wso2-data-services-server-2-6-x
comments: true
status: publish
title: Novidades WSO2 Data Services Server (2.6.x)
categories:
- arquitetura
- desenvolvimento
tags:
- carbon
- complex result
- csv
- data services
- database
- distributed transactions
- dss
- excel
- java
- soa
- sql
- stratos
- transações distribuídas
- transformation
- wso2
- wso2 carbon
- xsl
- xslt
---

[![WSO2 - Data Services Server 2.6.0 - Home](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-home-300x159.png)](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-home.png)

Tenho acompanhado os [_builds_ diários](http://builder.wso2.org/~carbon/releases/carbon/3.2.0/) que o pessoal
do [WSO2](http://wso2.org/) tem feito e logo percebi várias novidades na
interface, alteração essa que acontecerá em todos or produtos da série Carbon
3.2.*.

Mas, hoje eu tratarei apenas das novidades que teremos no Data Services
Server, que são muitas e algumas bem importantes e há muito esperadas!

  * [UDT (User Defined Type) Support](/2011/06/novidades-wso2-data-services-server-2-6-x/#udt-support)
  * [Complex Results](/2011/06/novidades-wso2-data-services-server-2-6-x/#complex-results)
  * [Auto Generated Keys Support](/2011/06/novidades-wso2-data-services-server-2-6-x/#auto-generated-keys-support)
  * [Distributed Transactions](/2011/06/novidades-wso2-data-services-server-2-6-x/#distributed-transactions)
  * [Improved Boxcarring Support](/2011/06/novidades-wso2-data-services-server-2-6-x/#improved-boxcarring-support)
  * [Improved Batch Request Support](/2011/06/novidades-wso2-data-services-server-2-6-x/#improved-batch-request-support)
  * [Scheduled Tasks](/2011/06/novidades-wso2-data-services-server-2-6-x/#scheduled-tasks)
  * [Registry Integration for Excel, CSV, XSLT](/2011/06/novidades-wso2-data-services-server-2-6-x/#registry-integration)
  * [Web Scraping Support](/2011/06/novidades-wso2-data-services-server-2-6-x/#web-scraping-support)
  * [Multiple SQL Dialect Support](/2011/06/novidades-wso2-data-services-server-2-6-x/#multiple-sql-dialect-support)
  * [Database to Data Service Generation](/2011/06/novidades-wso2-data-services-server-2-6-x/#db-to-ds-generation)
  * [Data Service Query Improvements](/2011/06/novidades-wso2-data-services-server-2-6-x/#data-service-query-improvements)
  * [Service Group/Hierarchy Support](/2011/06/novidades-wso2-data-services-server-2-6-x/#service-group-hierarchy-support)
  * [Database Explorer](/2011/06/novidades-wso2-data-services-server-2-6-x/#database-explorer)
  * [Data as a Service Features - DSS Stratos Service](/2011/06/novidades-wso2-data-services-server-2-6-x/#dss-stratos-service)

### <a name="udt-support"></a>UDT (User Defined Type) Support

Não encontrei maiores detalhes na documentação ou no próprio WSO2 Data
Services Server, talvez não tenha saído ainda nessa _release_.

### <a name="complex-results"></a>Complex Results

[![WSO2 Data Services Server 2.6.0 - Complex Elements - List](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-complex-elements-list-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-complex-elements-list.png) [![WSO2 Data Services Server 2.6.0 - Complex Elements - Insert nested](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-complex-elements-insert-nested-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-complex-elements-insert-nested.png)

Agora fica possível criar elementos complexos, facilitando algumas coisas em
que era necessário utilizar um _transformation_ (XSLT) ou _sub-queries_,
ganhando - e muito - em performance.

### <a name="auto-generated-keys-support"></a>Auto Generated Keys Support

[![WSO2 Data Services Server 2.6.0 - Generate keys](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-generate-keys-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-generate-keys.png) [![WSO2 Data Services Server 2.6.0 - Generate keys: Invoke](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-generate-keys-invoke-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-generate-keys-invoke.png)

Muito útil para recuperar a _primary key_ de um registro inserido no banco,
tirando a necessidade de fazer _stored procedures_ ou outro método de consumo
apenas para recuperar a chave inserida.

### <a name="distributed-transactions"></a>Distributed Transactions

[![WSO2 Data Services Server 2.6.0 - Distribute Transactions](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-distribute-transactions-300x159.png)](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-distribute-transactions.png)

Uma maneira de realizar transações distribuídas (na maioria das vezes em
_databases_ separados), será usado JTA para controlar as transações e também é
necessário que usará XA. Com isso ganhamos em não mais precisarmos controlar
isso manualmente com um serviço no WSO2 Application Server.

### <a name="improved-boxcarring-support"></a>Improved Boxcarring Support

Apenas melhorias no suporte que já existia desde a versão 2.5.0, não encontrei
nenhuma alteração visual ou no processo de desenvolvimento.

### <a name="improved-batch-request-support"></a>Improved Batch Request Support

Apenas melhorias no suporte que já existia desde a versão 2.5.0, não encontrei
nenhuma alteração visual ou no processo de desenvolvimento.

### <a name="scheduled-tasks"></a>Scheduled Tasks

[![WSO2 Data Services Server 2.6.0 - Scheduled Tasks](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-scheduled-tasks-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-scheduled-tasks.png) [![WSO2 Data Services Server 2.6.0 - Scheduled Tasks: Insert](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-scheduled-tasks-inserting-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-scheduled-tasks-inserting.png)

Agora, ao invés de fazermos _shell scripts_ que ficam na _crontab_ do servidor
para agendar alguns consumos, podemos fazer isso diretamente no WSO2 Data
Services Server.

### <a name="registry-integration"></a>Registry Integration for Excel, CSV, XSLT

Não encontrei maiores detalhes na documentação ou no próprio WSO2 Data
Services Server, talvez não tenha saído ainda nessa _release_.

### <a name="web-scraping-support"></a>Web Scraping Support

[![WSO2 Data Services Server 2.6.0 - Web Scraping: Data Source](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-web-scraping-data-source-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-web-scraping-data-source.png) [![WSO2 Data Services Server 2.6.0 - Web Scraping: Query](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-web-scraping-query-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-web-scraping-query.png)

Poderemos consumir dados diretamente de sites, fazendo _parser_ em conteúdo de
páginas, por exemplo.

### <a name="multiple-sql-dialect-support"></a>Multiple SQL Dialect Support

[![WSO2 Data Services Server 2.6.0 - Multiple Dialects SQL: Options](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-dialects-options-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-dialects-options.png) [![WSO2 Data Services Server 2.6.0 - Multiple Dialects SQL: Add](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-dialects-sql-add-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-dialects-sql-add.png)

Apesar de ter encontrado referências na _wizard_ de criação/alteração de
serviços, não encontrei nada na documentação ou entendi como funcionará, vamos
aguardar outros _releases_.

### <a name="db-to-ds-generation"></a>Database to Data Service

[![WSO2 Data Services Server 2.6.0 - Database to Data Service Generation](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-db-to-ws-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-db-to-ws.png) [![WSO2 Data Services Server 2.6.0 - Database to Data Service Generation: Choise Type](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-db-to-ws-choise-type-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-db-to-ws-choise-type.png) [![WSO2 Data Services Server 2.6.0 - Database to Data Service Generation: Select Tables](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-db-to-ws-select-tables-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-db-to-ws-select-tables.png) [![WSO2 Data Services Server 2.6.0 - Database to Data Service Generation: Try-it](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-db-to-ws-tryit-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-db-to-ws-tryit.png)

Nessa versão é possível gerar automaticamente os métodos para um database e
tabela específico, mas apenas para Carbon Data Sources. Apesar de não ter
gostado no padrão gerado, pode ser bom para gerar o CRUD básico e ser alterado
posteriormente.

### <a name="data-service-query-improvements"></a>Data Service Query Improvements

Imagino que tenha sido apenas melhorias nas rotinas internas de montagem e
processamento de _queries_. Porque as opções avançadas de _query_ já existiam
na versão 2.5.*.

### <a name="service-group-hierarchy-support"></a>Service Group/Hierarchy Support

[![WSO2 Data Services Server 2.6.0 - Service Group: Option](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-group-option-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-group-option.png)[![WSO2 Data Services Server 2.6.0 - Service Group: List](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-group-list-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-group-list.png)

Apenas um agrupamento de serviços, imagino que venha como padrão em todo
aplicativo da suíte Carbon, pois em alguns outros aplicativos já existia essa
opção.

### <a name="database-explorer"></a>Database Explorer

[![WSO2 Data Services Server 2.6.0 - Database Console: Login](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-dbconsole-login-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-dbconsole-login.png) [![WSO2 Data Services Server 2.6.0 - Database Console: Simple Query](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-dbconsole-simple-query-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-dbconsole-simple-query.png)

Uma novidade muito interessante e prática, eles colocaram dentro do WSO2 Data
Services Server uma maneira de explorarmos as bases de dados. E a interface
lembra bastante o [SQuirreL SQL](http://www.squirrelsql.org/), ficou muito
prático.

### <a name="dss-stratos-service"></a>Data as a Service Features - DSS Stratos Service

Existem algumas novidades também sobre os produtos como serviço na nuvem, que
chamam de [Stratos](http://www.mcorp.com.br/2010/06/lancamento-do-wso2-stratos-alpha/),
mas não encontrei documentação nesse _build_.

E algumas outras pequenas alterações que foram percebidas, como:

  * [Generate response](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-generate-response.png): baseado na _query_ é gerada a resposta do serviço;
  * [Force stored procedure](http://assets.mcorp.com.br/wp-content/uploads/2011/06/wso2-data-services-server-2.6.0-force-stored-procedure.png): força a executar a _query_ como uma _stored procedure_;
  * Entre outras inúmeras pequenas alterações que vão sendo notadas no uso dia-a-dia.
