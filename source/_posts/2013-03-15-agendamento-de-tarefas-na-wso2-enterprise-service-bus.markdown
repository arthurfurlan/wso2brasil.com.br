---
author: José Nogueira
date: '2013-03-15 11:11:13'
layout: post
slug: agendamento-de-tarefas-na-wso2-enterprise-service-bus
comments: true
status: publish
title: "Agendamento de tarefas na WSO2 Enterprise Service Bus"
external-url: http://mcorp.com.br/2013/03/agendamento-de-tarefas-na-wso2-enterprise-service-bus/
categories:
- desenvolvimento
tags:
- wso2
- wso2 esb
- esb
- enterprise service bus
- agendamento de tarefas
- agendamento
- tarefa
- crontab
---

Em alguns casos vemos a necessidade de agendar algumas tarefas para a execução de algum script ou rotina, no projeto que estou trabalhando atualmente surgiu a necessidade de monitorar um _WS_ a cada 5 segundos. Pensei em criar uma tarefa no [crontab](http://pt.wikipedia.org/wiki/Crontab), mas com isso seria complicado eu ter um controle mais detalhado sobre a execução da mesma, então me lembrei que na [WSO2 Enterprise Service Bus](http://wso2.com/products/enterprise-service-bus/) existe uma funcionalidade que provê exatamente essa funcionalidade.

Nesse caso, especificamente, eu teria que controlar através de _log_ as informações de execução, criei um _log_ no meu programa e pude utilizar os gráficos e relatórios da própria ferramenta.

# Vamos exemplificar na prática esse uso

As configurações abaixo foram feitas utilizando a versão 4.5.0 da WSO2 ESB.

## Criando a aplicação a ser executada

Utilizando o jar _[synapse-core.1.1.jar](http://mirrors.ibiblio.org/pub/mirrors/maven2/org/apache/synapse/synapse-core/1.1/synapse-core-1.1.jar) digitacomo dependência da aplicação, a seguir temos uma classe que exemplifica como ficarão nossos métodos, o método _execute_ será invocado de tempo em tempo na execução da tarefa, podemos programar o que quisermos ali, tanto a execução de um processo, uma atualização de base, uma chamada de um webservices e etc.

{% gist 5090589 %}

Iremos gerar o arquivo .jar dessa aplicação e o colocaremos dentro de _[ESB - Home]/repository/components/lib_

## Criando o agendamento

Primeiramente vamos selecionar a opção "Scheduled Tasks", na sequência "Add Task".

{% img center http://assets.mcorp.com.br/wp-content/uploads/2013/03/agendamento-de-tarefas-na-wso2-esb-passo-1.png %}

Iremos visualizar a tela onde cadastraremos nosso agendamento:

{% img center http://assets.mcorp.com.br/wp-content/uploads/2013/03/agendamento-de-tarefas-na-wso2-esb-passo-2.png %}

Nessa tela devemos preencher as opções obrigatórias, na opção "Task Implementation" iremos colocar o endereço da classe que iremos chamar, a mesma do arquivo .jar que colocamos no diretório da ESB anteriormente.

E após apontar o endereço da classe clicaremos em "Load Task Properties", caso ocorra algum erro do endereçamento, será nos avisado pela aplicação.

{% img center http://assets.mcorp.com.br/wp-content/uploads/2013/03/agendamento-de-tarefas-na-wso2-esb-passo-3.png %}

Podemos adicionar mais propriedades para o nosso agendamento (de acordo com a classe implementada), após isso iremos configurar a "trigger" do agendamento, podemos utilizar o padrão _crontab_ ou um padrão mais simples, nesse exemplo iremos cadastrar a opção de agendamento mais simples.

Na opção "Count" iremos dizer ao agendamento quantas vezes essa tarefa será executada, caso essa tarefa rode sempre podemos colocar o valor "-1".

Na opção "Interval" iremos colocar o período de cada execução dessa tarefa, o padrão do valor está em segundos. Então, após isso podemos clicar em "Schedule" e finalizarmos o agendamento.

{% img center http://assets.mcorp.com.br/wp-content/uploads/2013/03/agendamento-de-tarefas-na-wso2-esb-passo-4.png %}

É sempre interessante acompanharmos o _log_ da aplicação para termos certeza que o agendamento funcionou perfeitamente.
