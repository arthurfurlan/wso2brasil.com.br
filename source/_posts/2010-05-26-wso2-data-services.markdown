---
slug: wso2-data-services
publish: true
title: "WSO2 Data Services"
created_at: 2010-05-26 20:32:11 UTC
author: Leandro Prado
layout: post
external-url: http://www.leandroprado.com.br/2010/05/wso2-data-services/
categories:
- desenvolvimento
tags:
- wso2
- data services
- dss
- soa
---
Quanto estamos construindo um sistema temos que nos preocupar em qual abordagem de acesso aos dados vamos utilizar, tais como Enterprise Java Beans (EJBs), CORBA e Hibernate, cada um procura uma abordagem diferente para obtenção de dados, para SOA essa abordagem deve ser simples, para que possamos concentrar nossos esforços na implementação das funcionalidades de negócios.

<h3><img class="aligncenter size-full wp-image-95" title="dataservices" src="http://www.leandroprado.com.br/wp-content/uploads/2010/05/dataservices.gif" alt="" width="558" height="291" />Porque Data Services?</h3>

Os dados são o sangue da vida de uma empresa, por esse motivo eles devem sem bem armazenados e seguros. Geralemente em SOA (Service Oriented Architecture) temos que ter acesso à dados armazenados em fontes de dados heterogêneas.

Data Services essencialmente tira o esforço de desenvolver um mecanismo de acesso a dados para diferentes aplicações, ou seja, é um mecanismo para levar os dados armazenados em bases de dados relacionais, arquivos de Excel e arquivos de CSV e torná-los facilmente disponíveis como WebServices ou como REST.

Na sua essência os Data Services são responsáveis por quebrar a frágil ligação entre as aplicações e dados. Com o Data Services, dados e as aplicações existem isoladamente, mas podem colaborar quando necessário com isso temos a capacidade de manipular os mesmos dados de forma diferente quando solicitados por diferentes canais.

## Beneficios do Data Services

 * Fácil extrasão de dados de bases relacionais através de JDBC, além de arquivos como Excel, CSV e XML;
 * Gera um arquivo único de mapeamento no formato XML para expor os dados em vários formatos diferentes e protocolos, sem a necessidade de programação redundante para acesso múltiplo diferentes tecnologias de banco de dados;
 * Expõe seus dados como os serviços estilo Web Services ou recursos REST. Através de XML sobre HTTP, os dados podem até ser exposto como JSON (JavaScript Object Notation), tornando muito mais fácil para construir interfaces Ajax;
 * Gerar acesso transparente e unificado de um repositório consistente, que proporciona maior acessibilidade aos dados da empresa.

Para manipular o WSO2 Data Services temos o DSDL (Data Services Description Language) que permite especificar como as entradas das solicitações serão mapeadas e controlar como os resultados serão mostrados para o usuário.

## Performance

O WSO2 Data Services armazena em cache as solicitações mais usadas para ser recuperado por chamadas semelhantes subseqüentes, também é capaz de forçar um flush cache, caso as circunstâncias requerer o esvaziamento de cache de dados.

## Segurança

WSO2 Data Services oferece suporte a segurança em nível de elemento e segurança baseada em função de indivíduos e grupos no acesso aos dados, incluindo a assinatura digital, criptografia e diversas outros tokens de segurança.

## Conclusão

WSO2 Data Services é uma abordagem para o tratamento de dados da empresa como um serviço de primeira classe empresarial. Ele encapsula toda a lógica que executa a descoberta de dados, acesso a dados, validação de dados, segurança em uma camada de abstração simples.

WSO2 Data Services ajuda a criar serviços com rapidez e facilidade para o consumo de um serviço orientada a arquitetura.
