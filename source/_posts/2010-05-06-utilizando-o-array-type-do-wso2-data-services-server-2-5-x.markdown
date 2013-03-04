---
author: Leonardo Saraiva
date: '2010-05-06 18:27:32'
layout: post
slug: utilizando-o-array-type-do-wso2-data-services-server-2-5-x
comments: true
status: publish
title: Utilizando o Array Type do WSO2 Data Services Server 2.5.x
categories:
- desenvolvimento
tags:
- array type
- builder
- carbon
- data services
- dss
- mysql
- release candidate
- soa
- soapui
- web services application
- wso2
- wso2 carbon
---

Uma das [novidades do WSO2 Data Services Server 2.5.x](/2010/04/novidades-do-proximo-wso2-data-services-server-2-5-x/), já listada anteriormente, é que
agora poderemos trabalhar com _Array Types_. Essa opção não existia
anteriormente e as únicas maneiras que tínhamos para contornar, digamos que
não eram muito legais. Por exemplo: invocar várias vezes o método ou
concatenar as várias entradas em um campo _string_ e posteriormente (em uma
_procedure_ ou algo do gênero) realizar o _parser_.

Ambas tem seus problemas, muitas requisições invocando várias vezes ou
dificuldade de implementação (dependendo do banco de dados) para o caso de
realizar o _parser_ na _procedure_; mas, de uma forma ou outra, resolviam o
problema. Só que com a implementação de _Array Type_ resolvemos esse problema
de maneira simples, eficiente e elegante!

## Colocando a mão na massa

Digamos que temos um serviço onde nosso cliente quer listar vários produtos,
nosso cliente tem todos os códigos dos produtos e quer o restante dos dados.
Antigamente passaríamos para ele um método _productById_ que recebe um _id_,
algo como abaixo:

[![](http://assets.mcorp.com.br/wp-content/uploads/2010/05/try-it-method-productById-without-array-type-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/05/try-it-method-productById-without-array-type.png)
[![](http://assets.mcorp.com.br/wp-content/uploads/2010/05/soap-ui-method-productById-without-array-type-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/05/soap-ui-method-productById-without-array-type.png)

Mas agora tudo foi facilitado, vamos a "mágica"! Para alteração do método que
aceite a entrada de um _Array Type_, serão necessários apenas dois passos.

### Passo 1: editando a _query_

Teremos que trocar a _query_ que antigamente aceitava apenas um parâmetro como
entrada "id = :id" e colocaremos uma que aceita "N" parâmetros "id in (:id)".
Então na tela de edição da _query_ do WSO2 Data Services Server, basta
trocarmos, como fiz abaixo:

[![](http://assets.mcorp.com.br/wp-content/uploads/2010/05/query-without-array-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/05/query-without-array.png) [![](http://assets.mcorp.com.br/wp-content/uploads/2010/05/query-with-array-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/05/query-with-array.png)


### Passo 2: editando o tipo da entrada

E o segundo passo, editando os _Input Mappings,_ basta trocarmos o tipo
_scalar_ para _array_, novamente, como fiz abaixo:

[![](http://assets.mcorp.com.br/wp-content/uploads/2010/05/input-scalar-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/05/input-scalar.png) [![](http://assets.mcorp.com.br/wp-content/uploads/2010/05/input-array-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/05/input-array.png)



## O resultado

E agora vamos a parte legal: o resultado!

[![](http://assets.mcorp.com.br/wp-content/uploads/2010/05/try-it-method-productById-with-array-type-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/05/try-it-method-productById-with-array-type.png)
[![](http://assets.mcorp.com.br/wp-content/uploads/2010/05/soap-ui-method-productById-with-array-type-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/05/soap-ui-method-productById-with-array-type.png)



## Conclusão

Essa implementação facilitou muito e melhorou a qualidade de nossos serviços.
Ainda não foi lançada a versão final, apenas algumas _releases candidates_,
que podem ser acompanhadas pelo [repositório de _builders_ do WSO2 Carbon 3.0.0](http://builder.wso2.org/~carbon/releases/carbon/3.0.0/).

Deixo aqui o [download dos arquivos utilizados para implementar o _Array Type_](http://assets.mcorp.com.br/wp-content/uploads/2010/05/wso2tutorial-array-type.zip) nesse exemplo, contém os arquivos abaixo:

  * _Data Service_ antes da implementação do _Array Type_
  * _Data Service_ depois da implementação do _Array Type_
  * Script de criação do banco de dados utilizado (MySQL)

