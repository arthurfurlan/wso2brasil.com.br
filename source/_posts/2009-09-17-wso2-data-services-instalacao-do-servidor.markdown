---
author: Leonardo Saraiva
date: '2009-09-17 13:32:41'
layout: post
slug: wso2-data-services-instalacao-do-servidor
comments: true
status: publish
title: WSO2 Data Services - Instalação do servidor
categories:
- desenvolvimento
tags:
- data services
- dss
- eclipse
- instalação
- wso2
---

A instalação do WSO2 Data Services se divide em duas partes, a instalação do
servidor e a preparação do ambiente de desenvolvimento.

## 1. Servidor

É necessário realizar o download da última versão (utilizamos aqui a
[2.0](http://dist.wso2.org/products/solutions/data-services/java/2.0/wso2dataservices-2.0.zip)) do servidor na [página do projeto](http://wso2.org/projects/solutions/data-services/java).

Vou exemplificar os comandos como se fosse utilizar pasta
"~/Applications/wso2" para colocar todos os servidores do WSO2, caso tenha
outra escolha, verifique a adaptação dos comandos.

Criando a pasta:

    mkdir -p ~/Applications/wso2

Descompactando o arquivo (lembrando de verificar a versão do arquivo que você
baixou - no meu caso, 2.0):

    unzip /path/to/download/wso2dataservices-2.0.zip -d ~/Applications/wso2

Após descompactado, vamos iniciar o servidor:

    cd ~/Applications/wso2/wso2-dataservices-2.0 ./bin/wso2server.sh

Após algumas (várias) mensagens depois, você deve receber algo como:

    [2009-05-29 14:30:30,330] INFO - HTTPS port : 9443 {org.wso2.carbon.core.StartupServlet}
    [2009-05-29 14:30:30,333] INFO - HTTP port : 9763 {org.wso2.carbon.core.StartupServlet}
    [2009-05-29 14:30:30,333] INFO - WSO2 Carbon started in 35 sec {org.wso2.carbon.core.StartupServlet}[/code]

E isso representa que tudo já está instalado e funcionando! Para sair, basta
usar "CTRL + C".

Esse comando que acabou de utilizar é usado para controlar o serviço do WSO2,
tem alguns parâmetros que podem ser utilizados, para vê-los basta digitar:

    ./bin/wso2server.sh help

E com isso temos o servidor instalado! Para mantê-lo iniciado, em background,
basta utilizar o comando:

    ./bin/wso2server.sh start

## 1. Ambiente de desenvolvimento

É necessário realizar o download e instalação
[desse](http://dist.wso2.org/products/solutions/data-services/java/1.0.1/org.wso2.ws.dataservices.ide_1.0.1.jar) _plugin_ para o
[Eclipse](http://www.eclipse.org).

Numa próxima "jornada", vamos fazer nosso primeiro _data service_.