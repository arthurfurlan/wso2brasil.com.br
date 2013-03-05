---
slug: criando-um-ambiente-soa-com-wso2
publish: true
title: "Criando um ambiente SOA com WSO2"
kind: article
created_at: 2010-07-15 23:39:23 UTC
author: Leandro Prado
layout: post
external-url: http://www.leandroprado.com.br/2010/07/criando-um-ambiente-soa-com-wso2/
categories:
- desenvolvimento
tags:
- wso2
- greg
- governance registry
- wsas
- application server
---

<p style="text-align: justify;">Nesse post vou descrever como criar um ambiente SOA completo usando as ferramentas WSO2.</p>
<p style="text-align: justify;">O ambiente que estou usando é Ubuntu 10 como Java 6 (esse tutorial parte do princípio que o Ubuntu e o Java já estão instalados e configurados)</p>
<h3>Passo 1- Criar diretório</h3>
<p>Vamos criar um diretório onde vamos instalar todas as ferramentas do WSO2</p>
<pre class="brush:java">     cd /home/leandro-prado
     mkdir wso2
     cd wso2/
     pwd
     /home/leandro-prado/wso2</pre>
<h3>Passo 2 &#8211; WSO2 Governance Registry</h3>
<p style="text-align: justify;">Baixar o arquivo em <a title="WSO3 Governance Registry" href="http://wso2.com/products/governance-registry/" target="_blank">http://wso2.com/products/governance-registry/</a> (a versão que usamos foi a 3.5.0) descompactar e depois mover para o diretório criado acima</p>
<pre class="brush:java">     cd Downloads/wso2/
     unzip wso2greg-3.5.0.zip
     mv wso2greg-3.5.0 /home/leandro-prado/wso2/
     cd /home/leandro-prado/wso2/wso2greg-3.5.0/bin/
     ./wso2server.sh</pre>
<p style="text-align: justify;">Para iniciar o serviço entrar no diretório bin e executar o arquivo wso2server.sh, se tudo ocorrer sem erros, a seguinte saída deverá ser exibida no console</p>
<pre class="brush:java">     [2010-06-05 17:46:15,887]  INFO -  Connection established with the registry
     [2010-06-05 17:46:16,732]  INFO -  HTTPS port       : 9443
     [2010-06-05 17:46:16,761]  INFO -  HTTP port        : 9763
     [2010-06-05 17:46:18,911]  INFO -  Successfully Initialized Eventing on Registry
     [2010-06-05 17:46:27,749]  INFO -  Mgt Console URL  : https://10.0.2.15:9443/carbon/
     [2010-06-05 17:46:28,702]  INFO -  Started Transport Listener Manager
     [2010-06-05 17:46:28,703]  INFO -  Server           :  WSO2 Governance Registry-3.5.0
     [2010-06-05 17:46:28,703]  INFO -  WSO2 Carbon started in 65 sec</pre>
<p>Agora podemos acessar o browser e verificar se esta tudo correto:</p>
<p>Endereco: https://10.0.2.15:9443/carbon &#8211; <strong>Usuário: admin / Senha:admin</strong></p>
<p style="text-align: center;"><a href="http://www.leandroprado.com.br/wp-content/uploads/2010/06/GovernanceRegistry.png"><img class="size-medium wp-image-165 aligncenter" title="WSO2 Governance Registry" src="http://www.leandroprado.com.br/wp-content/uploads/2010/06/GovernanceRegistry-300x187.png" alt="" width="300" height="187" /></a></p>
<h3>Passo 3 &#8211; WSO2 Data Services</h3>
<p style="text-align: justify;">Agora vamos instalar o Data Service, baixar o arquivo em <a title="WSO2 Data Services" href="http://wso2.com/products/data-services-server/" target="_blank">http://wso2.com/products/data-services-server/</a> (a versão que usamos foi a 2.2.1) descompactar e depois mover para o diretório criado no passo 1, podemos perceber que a intalação é igual para todas as ferramentas.</p>
<pre class="brush:java">     cd Downloads/wso2/
     unzip wso2dataservices-2.2.1.zip
     mv wso2dataservices-2.2.1 /home/leandro-prado/wso2/
     cd /home/leandro-prado/wso2/wso2dataservices-2.2.1/bin/
     ./wso2server.sh</pre>
<p style="text-align: justify;">Quando mandamos iniciar o servidor do Data Service pela primeira vez vamos receber o seguinte erro:</p>
<pre class="brush:java">     [2010-06-05 18:43:35,233]  INFO -  Repository       : /home/leandro-prado/wso2/wso2dataservices-2.2.1/repository/
     [2010-06-05 18:43:35,720]  INFO -  HTTPS port       : 9443
     [2010-06-05 18:43:35,721]  INFO -  HTTP port        : 9763
     [2010-06-05 18:43:35,954] ERROR -  Error initializing endpoint
     java.net.BindException: Address already in use:9443</pre>
<p style="text-align: justify;">Esse erro ocorre porque a porta 9443 ja esta sendo usanda pelo WSO2 Governance Registry, por esse motivo temos que configurar manualmente outra porta para o Data Service, para isso temos que editar o arquivo transports.xml que fica na pasta conf</p>
<pre class="brush:java">     cd ..
     cd conf/
     sudo gedit transports.xml</pre>
<p style="text-align: justify;">Temos que alterar o parâmetro port tanto para HTTP e HTTPS, essa configuração está na a linha 3 e na linha 30  e depois iniciar o serviço novamente, conforme abaixo:</p>
<pre class="brush:java">     &lt;parameter name="port"&gt;9764&lt;/parameter&gt;
     &lt;parameter name="port"&gt;9444&lt;/parameter&gt;
     cd ..
     cd bin/
     ./wsoeserver.sh</pre>
<p style="text-align: justify;">Se tudo ocorrer sem erros a seguinte saída devera ser exibida no console:</p>
<pre class="brush:java">     [2010-07-03 00:21:01,928]  INFO -  Initializing transport descriptions and their associated parameters
     [2010-07-03 00:21:01,992]  INFO -  Repository       : /home/leandro-prado/wso2/wso2dataservices-2.2.1/repository/
     [2010-07-03 00:21:02,363]  INFO -  HTTPS port       : 9444
     [2010-07-03 00:21:02,363]  INFO -  HTTP port        : 9764
     [2010-07-03 00:21:04,398]  INFO -  Mgt Console URL  : https://10.0.2.15:9444/carbon/
     [2010-07-03 00:21:04,399]  INFO -  Started Transport Listener Manager
     [2010-07-03 00:21:04,399]  INFO -  Server           :  WSO2 Data Services-2.2.1
     [2010-07-03 00:21:04,400]  INFO -  WSO2 Carbon started in 50 sec</pre>
<p style="text-align: justify;">Para ver se tudo esta correto podemos acessar o administrador do Data Service no browser.</p>
<p>Endereço: https://10.0.2.15:9444/carbon &#8211; <strong>Usuário: admin / Senha:admin</strong></p>
<p><a href="http://www.leandroprado.com.br/wp-content/uploads/2010/07/DataServices.png"><img class="aligncenter size-medium wp-image-182" title="WSO2 Data Services" src="http://www.leandroprado.com.br/wp-content/uploads/2010/07/DataServices-300x187.png" alt="" width="300" height="187" /></a></p>
<h3>Passo 4 &#8211; WSO2 Application Server</h3>
<p style="text-align: justify;">Agora vamos instalar o Application Server, baixar o arquivo em <a href="http://wso2.com/products/web-services-application-server/" target="_blank">http://wso2.com/products/web-services-application-server/</a> (a versão que usamos foi a 3.2.0) para instalar seguir o mesmo padrão, descompactar, mover para o diretório, configurar o arquivo transports.xml (port HTTP 9445 e HTTPS 9765) e iniciar o serviço</p>
<pre class="brush:java">     cd Downloads/wso2/
     unzip wso2wsas-3.2.0.zip
     mv wso2wsas-3.2.0 /home/leandro-prado/wso2/
     cd /home/leandro-prado/wso2/wso2wsas-3.2.0
     cd repository/conf
     gedit mgt-transports.xml
     cd ../../bin
     ./wso2server.sh</pre>
<p style="text-align: justify;">Se tudo ocorrer sem erros a seguinte saída devera ser exibida no console:</p>
<pre class="brush:java">     [2010-07-03 00:49:45,404]  INFO -  Repository       : /home/leandro-prado/wso2/wso2wsas-3.2.0/repository/deployment/server/
     [2010-07-03 00:49:45,657]  INFO -  Connection established with the registry
     [2010-07-03 00:49:47,821]  INFO -  HTTPS port       : 9445
     [2010-07-03 00:49:47,829]  INFO -  HTTP port        : 9765
     [2010-07-03 00:49:50,774]  INFO -  Mgt Console URL  : https://10.0.2.15:9445/carbon/
     [2010-07-03 00:49:50,787]  INFO -  Started Transport Listener Manager
     [2010-07-03 00:49:50,795]  INFO -  Server           :  WSO2 WSAS-3.2.0
     [2010-07-03 00:49:50,796]  INFO -  WSO2 Carbon started in 33 sec</pre>
<p style="text-align: justify;">Para ver se tudo esta correto podemos acessar o administrador do Application Server no browser.</p>
<p>Endereco: https://10.0.2.15:9445/carbon &#8211; <strong>Usuário: admin / Senha:admin</strong></p>
<p><a href="http://www.leandroprado.com.br/wp-content/uploads/2010/07/ApplicationServer.png"><img class="aligncenter size-medium wp-image-187" title="WSO2 Application Server" src="http://www.leandroprado.com.br/wp-content/uploads/2010/07/ApplicationServer-300x187.png" alt="" width="300" height="187" /></a></p>
<h3>Passo 5 &#8211; WSO2 Enterprise Service Bus</h3>
<p style="text-align: justify;">Agora vamos instalar a BUS, baixar o arquivo em <a href="http://wso2.com/products/web-services-application-server/" target="_blank">http://wso2.com/products/enterprise-service-bus/</a> (a versão que usamos foi a 3.0.0) novamente a instalação segue o mesmo padrão, descompactar, mover para o diretório, configurar o arquivo transports.xml (port HTTP 9446 e HTTPS 9766) e iniciar o serviço</p>
<pre class="brush:java">     cd Downloads/wso2/
     unzip wso2esb-3.0.0.zip
     mv wso2esb-3.0.0 /home/leandro-prado/wso2/
     cd /home/leandro-prado/wso2/wso2esb-3.0.0
     cd repository/conf
     gedit mgt-transports.xml
     cd ../../bin
     ./wso2server.sh</pre>
<p style="text-align: justify;">Se tudo ocorrer sem erros a seguinte saída devera ser exibida no console:</p>
<pre class="brush:java">     [2010-07-03 01:15:19,725]  INFO - CarbonUIServiceComponent Mgt Console URL  : https://10.0.2.15:9446/carbon/
     [2010-07-03 01:15:19,783]  INFO - StartupFinalizerServiceComponent Started Transport Listener Manager
     [2010-07-03 01:15:19,784]  INFO - StartupFinalizerServiceComponent Server           :  WSO2 ESB-3.0.0
     [2010-07-03 01:15:19,784]  INFO - StartupFinalizerServiceComponent WSO2 Carbon started in 114 sec</pre>
<p style="text-align: justify;">Para ver se tudo esta correto podemos acessar o administrador do Application Server no browser.</p>
<p>Endereco: https://10.0.2.15:9446/carbon &#8211; <strong>Usuário: admin / Senha:admin</strong></p>
<p><a href="http://www.leandroprado.com.br/wp-content/uploads/2010/07/EnterpriseServiceBus.png"><img class="aligncenter size-medium wp-image-191" title="WSO2 Enterprise Service Bus" src="http://www.leandroprado.com.br/wp-content/uploads/2010/07/EnterpriseServiceBus-300x187.png" alt="" width="300" height="187" /></a></p>
<h3>Passo 6 &#8211; WSO2 Business Activity Monitor</h3>
<p>Agora vamos instalar a BAM, baixar o arquivo em <a href="http://wso2.com/products/business-activity-monitor/">http://wso2.com/products/business-activity-monitor/</a> (a versão que usamos foi a 1.0.1) novamente a instalação segue o mesmo padrão, descompactar, mover para o diretório, configurar o arquivo transports.xml (port HTTP 9447 e HTTPS 9767) e iniciar o serviço.</p>
<pre class="brush:java">     cd Downloads/wso2/
     unzip wso2bam-1.0.1.zip
     mv wso2bam-1.0.1 /home/leandro-prado/wso2/
     cd /home/leandro-prado/wso2/wso2bam-1.0.1
     cd conf/
     gedit transports.xml
     cd ../bin
     ./wso2server.sh</pre>
<p style="text-align: justify;">Se tudo ocorrer sem erros a seguinte saída devera ser exibida no console:</p>
<pre class="brush:java">     [2010-07-07 16:06:32,854]  INFO -  Connection established with the registry
     [2010-07-07 16:06:33,816]  INFO -  Successfully Initialized Eventing on Registry
     [2010-07-07 16:06:47,166]  INFO -  Mgt Console URL  : https://10.0.2.15:9447/carbon/
     [2010-07-07 16:06:47,167]  INFO -  Started Transport Listener Manager
     [2010-07-07 16:06:47,168]  INFO -  Server           :  WSO2 Business Activity Monitor-1.0.1
     [2010-07-07 16:06:47,168]  INFO -  WSO2 Carbon started in 96 sec</pre>
<p>Para ver se tudo esta correto podemos acessar o administrador da BAM no browser.</p>
<p>Endereco: https://10.0.2.15:9447/carbon &#8211; <strong>Usuário: admin / Senha:admin</strong></p>
<p><a href="http://www.leandroprado.com.br/wp-content/uploads/2010/07/BAM.png"><img class="aligncenter size-medium wp-image-230" title="WSO2 Business Activity Monitor" src="http://www.leandroprado.com.br/wp-content/uploads/2010/07/BAM-300x187.png" alt="" width="300" height="187" /></a></p>
<p>Podemos ver como é fácil instalar as ferrametas do WSO2, nos próximos posts vamos configurar os servers para se conectar com o baco de dados MySQL.</p>
<p>Até a próxima!</p>
