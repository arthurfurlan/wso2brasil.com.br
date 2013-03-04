---
author: Leonardo Saraiva
date: '2009-11-24 12:28:20'
layout: post
slug: novidades-nos-lancamentos-nov2009-da-plataforma-wso2
comments: true
status: publish
title: Novidades nos lançamentos (nov/2009) da plataforma WSO2
categories:
- desenvolvimento
tags:
- bpel
- business process
- carbon
- código aberto
- data services
- dss
- enterprise service bus
- esb
- governance registry
- identity
- jboss
- lançamento
- mashup
- web services application
- weblogic
- websphere
- wso2
- wso2 carbon
---

Como avisei [aqui](http://www.mcorp.com.br/2009/11/wso2-e-a-quinta-feira-agitada-muitos-lancamentos/) e no [twitter](http://www.twitter.com/vyper)
semana passada, o pessoal do [WSO2](http://www.wso2.org) lançou algumas
atualizações nos [projetos](http://wso2.org/projects) da plataforma WSO2
Carbon. Mas somente agora, com o lançamento oficial, é que podemos descobrir o
que foi atualizado.

Segue um resumão (baseado nas notas de lançamento) com o que foi atualizado em
cada um dos projetos.

## WSO2 Web Services Application Server (v3.1.2)

  * Correções em vários softwares que fazem parte dele: Apache Axis2, Apache Rampart, Apache Sandesha2, WSO2 Carbon e alguns outros projetos;
  * Correção da limpeza de memória após reiniciar o servidor.

Versão original (inglês): [aqui](http://wso2.org/project/wsas/java/3.1.2/docs/release_notes.html).

## WSO2 Enterprise Service Bus (v2.1.2)

  * Diversas melhorias e correções desde a versão 2.1.0 lançada em julho de 2009.

Versão original (inglês): [aqui](http://wso2.org/project/esb/java/2.1.2/docs/release-notes.html).

## WSO2 Governance Registry (v3.0.2)

  * Melhoria no suporte a transação;
  * Suporte ao WebSphere, WebLogic e JBoss;
  * Baseado na suíte WSO2 Carbon;
  * Suporte a clusterização;
  * Correção de vários _bugs_.

Versão original (inglês): [aqui](http://wso2.org/project/registry/3.0.2/docs/release-notes.html).

## WSO2 Business Process Server (v1.1.0)

  * Nova camada de integração WSO2 Carbon para o Apache ODE;
  * Utilizando Apache ODE 2.0-beta (baseado no trunk) como engine BPEL;
  * Suporte experimental para clusterização;
  * Suporte para consumo de serviços seguros (usando WS-Security);
  * Utilizando OpenJPA para camada de acesso a dados ODE;
  * Recuperação de atividades utilizando o management console;
  * Atualização online (_hot update_) do pacote BPEL facilitam o versionamento;
  * Suporte a manipulação de dados utilizando E4X nos processos BPEL.

Aqui deixo um adendo, baseado em alguns testes superficiais que fiz, posso
dizer que não é indicado colocar essa versão em produção. Como disseram nas
notas de lançamento, muita coisa está incompleta ainda e achei alguns
probleminhas. Mas é interessante tentarmos colocar os processos BPEL e
realizar testes para reportarmos os problemas e ajudarmos na correção dos
mesmos para a versão 1.1.1 (que espero que chegue logo).

Isso é até compreensível, já que se trata de uma nova versão e não apenas
correções de bugs como as outras. (:

Versão original com cada item comentado (inglês): [aqui](http://wso2.org/project/bps/1.1.0/docs/release-note.html).

## WSO2 Identity Server (v2.0.2)

  * Correções em vários softwares que fazem parte dele: Apache Axis2, Apache Rampart, Apache Sandesha2, WSO2 Carbon e alguns outros projetos.

Versão original (inglês): [aqui](http://wso2.org/project/solutions/identity/2.0.2/docs/release-
notes.html).

## WSO2 Mashup Server (v2.0.1)

  * Interface visual para gerenciar as tarefas agendadas;
  * Baseado no WSO2 Carbon SOA Framework que irá facilitar habilitação de funções a um clique, como o gerenciamento de Data Services nas futuras versões do Mashup Server.

Versão original (inglês): [aqui](http://wso2.org/project/mashup/2.0.1/docs/release_notes.html).
