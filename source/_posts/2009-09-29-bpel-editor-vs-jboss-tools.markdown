---
author: Leonardo Saraiva
date: '2009-09-29 07:23:41'
layout: post
slug: bpel-editor-vs-jboss-tools
comments: true
status: publish
title: BPEL Editor VS JBoss Tools
categories:
- desenvolvimento
tags:
- bpel
- bpel editor
- deploy
- eclipse
- jboss
- jboss tools
- transformation
- wso2
- xsl
---

Cansado de apanhar dos bugs e problemas do [BPEL Eclipse](http://www.eclipse.org/bpel/), resolvi tentar a sorte com o [JBoss Tools (3.1)](http://www.jboss.org/tools).

O JBoss Tools não atende só BPEL, tem diversas funcionalidades, mas o que me
importava realmente era o BPEL.

Após duas semanas trabalhando com ele e fazendo os processos o utilizando,
cheguei as conclusões abaixo:

**Boas notícias:**

  * auto-completation para xsl;
  * atalho para criação de arquivo xsl;
  * adicionar elemento no schema tem menu "antes" e "depois".

**Más notícias:**

  * na criação do arquivo de deploy, além de o nome ficar diferente (fica bpel-deploy.xml e não deploy.xml), não consigo selecionar os serviços os targets, tive que fazer o arquivo manualmente;
  * continua não alterando o nome da operação no bpel ao alterar no wsdl;
  * continua (as vezes) não criando um novo "assign" quando pergunta se quer que seja criado (mas não dá exception que obrigava abrir e fechar o bpel);
  * o problema ao alterar o nome da variável de "request" ou "response", fechar o bpel e verificar no "Details" do "Invoke" continua;
  * continua incluido as variáveis em um local do bpel que o editor não lê;
  * simplesmente os botões de "add" e "delete" do "details" de um "assign" continua parando de responder simplesmente;
  * continua perdendo as referências aos wsdl do nada.

Ou seja, não resolveu meus maiores problemas além de criar alguns novos...
Definitivamente não conheço um editor BPEL livre decente. Alguém conhece?