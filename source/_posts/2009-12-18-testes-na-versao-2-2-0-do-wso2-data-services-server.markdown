---
author: Leonardo Saraiva
date: '2009-12-18 17:46:09'
layout: post
slug: testes-na-versao-2-2-0-do-wso2-data-services-server
comments: true
status: publish
title: "Testes na versão 2.2.0 do WSO2 Data Services Server"
categories:
- desenvolvimento
tags:
- data services
- dbs
- dss
- eclipse
- wso2
---

Estava eu, numa calma sexta-feira, realizando testes na recém lançada versão
2.2.0 do [WSO2 Data Services Server](http://wso2.org/projects/data-services-server/java), e para começá-los resolvi fazer [deploy](/glossario/#Deploy) dos
serviços que já temos desenvolvido, pensando que tudo seria tranquilo, como
estava o meu dia, mas... ledo engano.

## Erro - Primeiro ato

Fui no básico: "Add > Data Service > Upload" e...

[![wso2-data-services-faulty-01](http://assets.mcorp.com.br/wp-content/uploads/2009/12/wso2-data-services-faulty-01-300x199.png)](http://assets.mcorp.com.br/wp-content/uploads/2009/12/wso2-data-services-faulty-01.png)

Um erro que não me
diz muito, então o jeito foi ver o que poderia ser por "tentativa" e erro.
Após um pouco de luta e leitura do código fonte do arquivo DBS, descobri que
era algum método que executa uma procedure e não tinha o ordinal preenchido.

{% gist 2907872 %}

Então peguei a linha 3 e corrigi, deixando assim:

{% gist 2907878 %}

Ou seja, devíamos ter prestado mais atenção quando falavam ser obrigatório
para procedures o preenchimento desse campo, mas como nunca deu problema,
então não prestávamos a devida atenção.

## Erro - Segundo ato

Com o serviço devidamente publicado, fui a execução dos métodos para ver se
tudo iria bem. Primeiro método (sem parâmetros de entrada) foi tranquilo,
retornou tudo que eu precisava. Já no segundo método...

[![wso2-data-services-faulty-02](http://assets.mcorp.com.br/wp-content/uploads/2009/12/wso2-data-services-faulty-02-300x199.png)](http://assets.mcorp.com.br/wp-content/uploads/2009/12/wso2-data-services-faulty-02.png)

E voltamos a busca do
erro perdido... E dessa vez não foi falta de atenção nossa, apenas o plugin
que o pessoal do WSO2 disponibiliza (e que ensinei a
[compilar](http://www.mcorp.com.br/2009/12/compilando-o-plugin-do-wso2-data-services-para-o-eclipse/))
que não preencheu o atributo como devia. Na chamada
da operação estava assim:

{% gist 2907879 %}

Enquanto deveria estar assim:

{% gist 2907881 %}

E feito todas essas alterações na definição dos data service, tudo correu bem
e tranquilo com essa nova versão.

Mas ainda acho que vale a pena esperar um pouco pra ver se não aparece nenhuma
correção que levem eles a gerar a versão 2.2.1; também tenho que verificar se
os _patches_ que aplicamos na versão anterior deixaram de ser necessário. Mas
isso fica pra uma próximo oportunidade.
