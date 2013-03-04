---
author: Leonardo Saraiva
date: '2010-06-16 10:17:12'
layout: post
slug: compilando-o-wso2-carbon-3-0-0-e-corrigindo-o-wso2-data-services-server-2-5-0
comments: true
status: publish
title: Compilando o WSO2 Carbon 3.0.0 e corrigindo o WSO2 Data  Services Server 2.5.0
categories:
- desenvolvimento
tags:
- carbon
- data services
- dss
- java
- maven
- maven2
- openssl
- software livre
- wso2
- wso2 carbon
---

![](http://assets.mcorp.com.br/wp-content/uploads/2010/06/wso2-data-services-server.gif)Versões novas de produtos sempre são uma alegria, seja pelos
recursos novos ou somente pela novidade que sempre alegra-nos, principalmente
nós desenvolvedores. Mas juntamente com as novas versões (principalmente nos
primeiros releases) vem também problemas, bugs ou incompatibilidade de
versões- os problemas mais comuns.

E para não pararmos no tempo, vendo que [as novidades do WSO2 Data Services Server 2.5.0](/2010/04/novidades-do-proximo-wso2-data-services-server-2-5-x/)
seriam muito bem vindas para nós, resolvemos realizar testes para verificar a
possibilidade de atualizarmos nossa versão da 2.2.1 para a 2.5.0, e surgiu
aquela alegria quando vimos que não teríamos problemas de incompatibilidade
como ocorreu nos testes de migração da 2.0 para [WSO2 Data Services Server 2.2.1](/2009/12/testes-na-versao-2-2-0-do-wso2-data-services-server/).

Mas como nem tudo são rosas, um velho _bug_ conhecido nosso na versão 2.0 e
discutido no [fórum - de não aceitar valores _null_](http://wso2.org/forum/thread/5349), tinha sido corrigido na versão
2.2.1; mas resolveu dar as caras na versão 2.5.0. E por necessitarmos das
novidades dessa versão, tivemos que correr atrás e corrigir o problema, já
corrigido anteriormente.

![](http://assets.mcorp.com.br/wp-content/uploads/2010/06/wso2-carbon.gif)Como já
conhecemos a estrutura, fomos direto ao site do projeto para realizar o
[download do fonte do WSO2 Data Services Server](http://wso2.org/downloads/data-services-server) e fomos atrás do arquivo problemático (SQLQuery.java).
Mas para nossa surpresa, o arquivo não estava mais lá, foi centralizado no
projeto [WSO2 Carbon](http://wso2.org/downloads/carbon).

Então com o arquivo de [código-fonte do WSO2 Carbon
3.0.0](http://dist.wso2.org/products/carbon/3.0.0/wso2carbon-3.0.0-src.zip)
devidamente baixado, vamos colocar a mão na massa.

## Baixando e descompactando o fonte

    wget http://dist.wso2.org/products/carbon/3.0.0/wso2carbon-3.0.0-src.zip
    unzip wso2carbon-3.0.0-src.zip

## Baixando e aplicando o _patch_

    wget /wp-content/uploads/2010/06/wso2-dataservices-accept-null.txt
    cd wso2carbon-3.0.0-src patch -p1 wso2-dataservices-accept-null.patch

E a mensagem recebida aqui será algo como:

    patching file components/data-services/org.wso2.carbon.dataservices.core/3.0.0/src/main/java/org/wso2/carbon/dataservices/dispatch/query/SQLQuery.java

## Compilando o componente

Levando em consideração que você tenha as dependências necessárias, vai ser um
passo bem demorado. Vai fazer download de alguns pacotes, compilar, testar e
gerar uma nova versão do componente, com a correção.

    cd components/data-services
    mvn install

## Corrigindo o Data Services Server

Agora que temos o componente corrigido e devidamente compilado, vamos copiá-lo
para a instância do WSO2 Data Services Server (levando em consideração que
minha instalação fica em ~/Applications/wso2/wso2dataservices-2.5.0).

    cp org.wso2.carbon.dataservices.core/3.0.0/target/org.wso2.carbon.dataservices.core-3.0.0.jar ~/Applications/wso2/wso2dataservices-2.5.0/wso2dataservices-2.5.0/repository/components/plugins/org.wso2.carbon.dataservices.core-3.0.0.jar
    cp org.wso2.carbon.dataservices.ui/3.0.0/target/org.wso2.carbon.dataservices.ui-3.0.0.jar ~/Applications/wso2/wso2dataservices-2.5.0/wso2dataservices-2.5.0/repository/components/plugins/org.wso2.carbon.dataservices.ui-3.0.0.jar

## Conclusão

Com o _patch_ criado, testado e aplicado. Abrimos um [pedido de correção no JIRA do WSO2](https://wso2.org/jira/browse/CARBON-7589), para que eles possam
corrigir na próxima _release_ (provavelmente a 2.5.1). Caso você não tenha
disponibilidade (de tempo ou paciência), pode baixar os componente do WSO2
Data Services Server corrigido (bastando apenas descompactá-los).

  * [org.wso2.carbon.dataservices.core-3.0.0.jar](/wp-content/uploads/2010/06/carbon-dataservices-core-3.0.0.tar.gz)
  * [org.wso2.carbon.dataservices.ui-3.0.0.jar](/wp-content/uploads/2010/06/carbon-dataservices-ui-3.0.0.tar.gz)

E tenho que falar, viva o código aberto e o software livre! (;
