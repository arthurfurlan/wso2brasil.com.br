---
author: Leonardo Saraiva
date: '2010-04-06 15:44:57'
layout: post
slug: wso2-business-activity-monitoring-sql-server
comments: true
status: publish
title: WSO2 Business Activity Monitoring + SQL Server
categories:
- desenvolvimento
tags:
- bam
- business activity monitoring
- business process
- data services
- dss
- governance registry
- h2
- identity
- instalação
- monitor
- mssql
- mysql
- oracle
- registry
- sql server
- wso2
---

[![](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wso2-bam.gif)](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wso2-bam.gif)A pedidos do "chefe", realizei o download
e a instalação do [WSO2 Business Activity Monitoring](http://wso2.org/downloads/bam) (versão 1.0.1) e parti para os
testes.

Mas como migramos toda a suíte para rodar sobre o SQL Server, configurei tudo
para apontar para o banco de dados do [WSO2 Governance Registry](http://wso2.org/downloads/governance-registry)
(arquivo _conf/registry.xml_) e do [WSO2 Identity Server](http://wso2.org/downloads/identity)
(arquivo _conf/user-mgt.xml_) - maiores explicações ficam para uma outra oportunidade.

Só que ainda ficou uma dúvida no ar! Aonde estavam as configurações de conexão
de banco de dados que armazenam as informações do [BAM](/glossario/#BAM)
propriamente dito? Pesquisando nos arquivos instalados encontrei um diretório
"bam", e para minha não-surpresa, lá estavam mais dois diretórios:

  * **./bam/database/**: diretório com arquivos da base de dados do H2;
  * **./bam/sql/**: scripts de criação da base de dados em diferentes bancos (H2, SQL Server, MySQL e Oracle).

Com essa descoberta, o jeito foi partir para o básico, buscar um arquivo de
configuração que pudesse conter a conexão apontando para esses arquivos.

    leonardo@mcorp:~/Applications/wso2/wso2bam-1.0.1$ grep -r h2:database *
    conf/registry.xml: jdbc:h2:database/WSO2CARBON_DB
    conf/user-mgt.xml: jdbc:h2:database/WSO2CARBON_DB

Ops, não encontrei nada. Nova tentativa:

    leonardo@mcorp:~/Applications/wso2/wso2bam-1.0.1$ grep -r h2 *
    [milhões de respostas - ocultadas por mim - que não ajudam em nada]

Vamos lá, filtrar um pouco mais para quem sabe ser mais feliz:

    leonardo@mcorp:~/Applications/wso2/wso2bam-1.0.1$ grep -r jdbc:h2 *
    conf/registry.xml: jdbc:h2:database/WSO2CARBON_DB
    conf/user-mgt.xml: jdbc:h2:database/WSO2CARBON_DB
    repository/dataservices/BAMSummaryGenerationDS.dbs:jdbc:h2:bam/database/WSO2BAM_DB
    repository/dataservices/BAMConfigurationDS.dbs:jdbc:h2:bam/database/WSO2BAM_DB
    repository/dataservices/BAMStatQueryDS.dbs:jdbc:h2:bam/database/WSO2BAM_DB
    repository/dataservices/BAMDataCollectionDS.dbs:jdbc:h2:bam/database/WSO2BAM_DB
    repository/dataservices/BAMSummaryQueryDS.dbs:jdbc:h2:bam/database/WSO2BAM_DB

E agora sim! Com isso descobrimos que ele utiliza alguns [data services](/glossario/#DataServices) que realizam o trabalho "sujo".

Então, basta alterarmos todos esses serviços para conectarem na base de dados
criada no SQL Server (dentro de cada serviço tem exemplos). Os serviços são:

  * repository/dataservices/BAMSummaryGenerationDS.dbs
  * repository/dataservices/BAMConfigurationDS.dbs
  * repository/dataservices/BAMStatQueryDS.dbs
  * repository/dataservices/BAMDataCollectionDS.dbs
  * repository/dataservices/BAMSummaryQueryDS.dbs

E carregar o arquivo _bam/sql/bam_schema_mssql.sql_ na base de dados e...
_voilà_.

    INFO - Server : WSO2 Business Activity Monitor-1.0.1 INFO - WSO2 Carbon started in 6 sec

Os estudos sobre o WSO2 Business Activity Monitoring continuarão num próximo
capítulo, sempre acompanhado de dicas e descobertas. (:
