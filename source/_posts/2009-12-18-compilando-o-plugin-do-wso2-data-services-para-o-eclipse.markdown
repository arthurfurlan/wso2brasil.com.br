---
author: Leonardo Saraiva
date: '2009-12-18 12:21:41'
layout: post
slug: compilando-o-plugin-do-wso2-data-services-para-o-eclipse
comments: true
status: publish
title: Compilando o plugin do WSO2 Data Services Server para o Eclipse
categories:
- desenvolvimento
tags:
- código aberto
- compilação
- data services
- dss
- eclipse
- instalação
- maven2
- plugin
- repositório
- subversion
- wso2
---

![Eclipse + WSO2 Data Service](http://assets.mcorp.com.br/wp-content/uploads/2009/12/eclipse-wso2-ds.png) Como não encontrei uma versão
final do plugin para o [Eclipse](http://www.eclipse.org) para criação, edição
e deploy de serviços do [WSO2 Data Services Server](http://wso2.org/projects/data-services-server/java) na página de downloads do site, o jeito foi
compilar o plugin a partir do fonte disponível no
[repositório](http://wso2.org/svn) (e viva o código aberto). E seguem abaixo
os passos necessário para o procedimento.

## Requisitos

Será necessário que você tenha instalado os programas abaixo para poder
realizar esse processo. Não é minha ideia ensinar como instalar, mas com uma
busca no [Google](http://www.google.com.br) esse problema deve ser facilmente
resolvido:

  * [Subversion](http://subversion.tigris.org/)
  * [Maven2](http://maven.apache.org/)

## Baixando fontes

Primeiro passo é baixar do [repositório](http://wso2.org/svn) o código fonte
da última versão:

    svn co https://wso2.org/repos/wso2/trunk/tools/ide/eclipse/data-service/org.wso2.ws.dataservices.ide/

## Compilação

Depois de baixados os fontes, basta entrar na pasta que foi gerada e mandar
compilar:

    cd org.wso2.ws.dataservices.ide
    mvn install

Esse processo pode demorar um pouco, pois ele realiza o download de diversas
dependências para compilação, mas no fim ele gera dentro do diretório "target"
com o arquivo "org.wso2.ws.dataservices.ide_1.0.0.jar" que deve ser instalado
no seu Eclipse.

## Instalação

No meu caso, o Eclipse está instalado no meu _home_ e é para lá que copiei o
arquivo.

    cp target/org.wso2.ws.dataservices.ide_1.0.0.jar ~/Applications/eclipse/plugins/.

## Finalização

[![WSO2 Data services: Wizard new](http://assets.mcorp.com.br/wp-content/uploads/2009/12/wso2-data-services-wizard-new-300x234.png)](http://assets.mcorp.com.br/wp-content/uploads/2009/12/wso2-data-services-wizard-new.png)

E com isso, no menu de "Novo", do seu Eclipse, deve
ter a opção de _wizard_ para criação e após criado o serviço (que ficará para
um outro post) você tem a opção de clicar com o botão direito no arquivo e
editar (_Edit Data Service_) ou realizar o [deploy](/glossario/#Deploy)
(_Deploy Data Service_).

