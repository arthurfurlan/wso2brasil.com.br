---
author: Leonardo Saraiva
date: '2011-01-04 07:28:06'
layout: post
slug: lancamento-do-wso2-complex-event-processing-server-1-0-0-alpha
comments: true
status: publish
title: Lançamento do WSO2 Complex Event Processing Server 1.0.0 (Alpha)
categories:
- desenvolvimento
tags:
- cep
- drools
- esper
- lançamento
- wso2
---

![](http://assets.mcorp.com.br/wp-content/uploads/2011/01/wso2-complex-event-processing-server-300x28.gif)

Foi lançado ontem na lista de desenvolvedores do WSO2 (carbon-dev@wso2.org) o
WSO2 Complex Event Processing Server, em sua versão 1.0.0 (alpha), faz com que
tenhamos processamento de eventos complexos em nosso ambiente SOA.

Alguns dos recursos que podemos encontrar no WSO2 CEP:

  * Plugable back end rutime support - WSO2 CEP supports following back end run time engines.
    * Drools Fusion - This back end runtime engine is distributed with the CEP pack
    * Esper     - This back end runtime is available at WSO2 GPL P2 repository : [http://dist.wso2.org/wso2-gpl-p2/carbon/releases/3.1.0-alpha/](http://dist.wso2.org/wso2-gpl-p2/carbon/releases/3.1.0-alpha/) and can be added as a feature with WSO2 Carbon Feature Management.
  * Support Multiple Broker Types - WSO2 CEP supports WS-Event and JMS-Qpid broker types;
  * GUI Support -  WSO2 CEP supports create,edit,delete operations on Buckets, Inputs and Queries;
  * Use Registry resources - WSO2 CEP supports using resources stored in registry (Queries) to create buckets;
  * Persistence   - WSO2 CEP supports persisting created buckets in the registry;
  * I18n Support for CEP - WSO2 CEP supports internationalization.

O povo do WSO2 nos convida para [baixar o WSO2 CEP](http://wso2.org/downloads/cep), instalar, testar e reportar bugs
(utilizando o [Jira do WSO2](https://wso2.org/jira/secure/project/ViewProject.jspa?pid=10190)) - caso
encontremos!
