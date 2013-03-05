---
slug: criando-servicos-com-o-wso2-parte-1-wso2-data-services
publish: true
title: "Criando serviços com o WSO2 - Parte 1 - WSO2 Data Services"
kind: article
created_at: 2010-09-22 19:04:35 UTC
author: Leandro Prado
layout: post
external-url: http://www.leandroprado.com.br/2010/09/criando-servicos-com-o-wso2-parte-1-wso2-data-services/
categories:
- desenvolvimento
tags:
- wso2
- data services
- dss
---

<p><img class="alignleft size-thumbnail wp-image-490" title="WSO2 Logo" src="http://www.leandroprado.com.br/wp-content/uploads/2010/09/logo_wso2.jpg" alt="" width="200" height="100" />Depois de publicar o post <a title="Criando um ambiente SOA com WSO2" href="http://www.leandroprado.com.br/2010/07/criando-um-ambiente-soa-com-wso2/" target="_blank">Criando um ambiente SOA com WSO2</a> estamos recebendo vários emails e comentários de usuários que estão com diversas dúvidas e como usar as ferramentas do WSO2 integrada, por esse motivo, hoje vamos começar uma série de posts explicativos de como criar um serviço completo (DS, WSAS, BUS) usando as ferramentas WSO2.</p>
<p>Antes de começar vamos entender a arquitetura que vamos estar utilizando, veja abaixo:</p>
<p style="text-align: center;"><a href="http://www.leandroprado.com.br/wp-content/uploads/2010/09/arquitetura.png"><img class="size-thumbnail wp-image-492 aligncenter" title="Arquitetura do ambiente" src="http://www.leandroprado.com.br/wp-content/uploads/2010/09/arquitetura.png" alt="" width="326" height="326" /></a></p>
<ul>
<li>DataService será responsável por recuperar as informações em uma origem de dedos, pode ser um banco de dados (MySQL, Postegres, SQLServer, Oracle, etc&#8230;) pode ser em um arquivo XML ou em um arquivo CSV.</li>
<li>Application Server que será responsável por fazer a orquestração dos nossos serviços e pela regra de negócio</li>
<li>BUS será responsável por expor nosso serviços para os clientes (Mobile, Portals, Desktop, etc&#8230;)</li>
</ul>
<p>O nosso cenário para o serviço de teste será um cadastro de funcionário para o setor de RH de uma empresa, vamos estar utilizando o banco de dados MySQL 5. Então mãos no teclado!!</p>
<h3>Criando a Base de Dados</h3>
<pre class="brush: sql; title: ; notranslate">

create database rh;
use rh;

CREATE TABLE funcionario (
  id_funcionario int(10) NOT NULL AUTO_INCREMENT,
  nome_funcionario varchar(100) NOT NULL,
  endereco_funcionario varchar(100) NOT NULL,
  sexo_funcionario char(1) NOT NULL,
  data_aniversario datetime NOT NULL,
  PRIMARY KEY (id_funcionario),
  UNIQUE KEY PK_Funcionario (id_funcionario)
);

INSERT INTO funcionario (nome_funcionario, endereco_funcionario, sexo_funcionario, data_aniversario) VALUES ('Leandro Prado 1', 'Rua xyz 367', 'M', '2000-10-10');
INSERT INTO funcionario (nome_funcionario, endereco_funcionario, sexo_funcionario, data_aniversario) VALUES ('Leandro Prado 2', 'Rua xyz 367', 'M', '2000-10-10');

</pre>
<h3>Criando um WSO2 DataService</h3>
<p>1. Dentro do Management Console do DataService clique no menu DataServices -&gt; Create</p>
<p style="text-align: center;"><a href="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem1.png"><img class="aligncenter size-medium wp-image-502" title="Selecione a opção Create" src="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem1.png" alt="" width="136" height="300" /></a></p>
<p>2. Coloque no nome e a descrição do Serviço e clique em Next</p>
<p style="text-align: center;"><a href="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem2.png"><img class="aligncenter size-medium wp-image-503" title="Adicione o nome do Serviço" src="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem2.png" alt="" width="514" height="190" /></a></p>
<p>3. Agora vamos adionar a nossa fonte de dados, selecione Add New Data Source</p>
<p style="text-align: center;"><a href="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem3.png"><img class="aligncenter size-medium wp-image-505" title="Adicione uma fonte de dados" src="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem3.png" alt="" width="514" height="107" /></a></p>
<p>4. Na tela de configuração do DataSource temos os seguintes campos:</p>
<ul>
<li>DataSource id:</li>
<li>DataSource Type:</li>
<li>Database Engine:</li>
<li>Driver Class:</li>
<li>JDBC URL:</li>
<li>User Name:</li>
<li>Password:</li>
<li>Min. Pool Size:</li>
<li>Max. Pool Size:</li>
<li>AutoCommit:</li>
</ul>
<p style="text-align: center;"><a href="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem4.png"><img class="aligncenter size-medium wp-image-504" title="Configurando o MySQL" src="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem4.png" alt="" width="512" height="279" /></a></p>
<p>Clique no botão Test Connection para verificar se a conexão com o banco está correta.</p>
<p style="text-align: center;"><a href="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem5.png"><img class="aligncenter size-medium wp-image-507" title="Testando a conexão com o BD" src="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem5.png" alt="" width="513" height="279" /></a></p>
<p>Se esse o erro acima ocorrer significa que está faltando o jar de conexão com o MySQL, então acesse esse <a title="MySQL Connector" href="http://www.mysql.com/downloads/connector/j/" target="_blank">link</a> e baixe o conector e copie o jar para a pasta  wso2/wso2dataservices-2.2.1/repository/components/lib e depois restart o  serviço do WSO2 DataServices.</p>
<p style="text-align: center;"><a href="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem6.png"><img class="aligncenter size-medium wp-image-508" title="Adicionando a fonte de Dados" src="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem6.png" alt="" width="513" height="278" /></a></p>
<p>5. Na próxima tela vamos criar as querys que nosso serviço vai executar</p>
<p style="text-align: center;"><a href="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem18.png"><img class="aligncenter size-medium wp-image-509" title="Criando uma nova query" src="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem18.png" alt="" width="512" height="88" /></a></p>
<p>6. Na tela para adicionar uma nova query temos os seguintes campos:</p>
<ul>
<li>Query ID:</li>
<li>Data Source:</li>
<li>SQL:</li>
<li>Input Mappging</li>
<li>Grouped by element:</li>
<li>Row name:</li>
<li>Row namespace:</li>
<li>Output Mappging:</li>
</ul>
<p>7. Se sua query possuir parâmetros de entrada deve ser adicionado clicando no botão Input Mappings, essa tela possui os seguintes campos:</p>
<ul>
<li>Mapping Name</li>
<li>SQL Type</li>
<li>IN/OUT Type</li>
<li>Ordinal</li>
</ul>
<p style="text-align: center;"><a href="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem8.png"><img class="aligncenter size-medium wp-image-514" title="Adicionando os parâmetros de entrada" src="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem8.png" alt="" width="513" height="210" /></a></p>
<p>8. Para recuperar os dados de retorno da sua query clique no botão Output Mappings e adicione os campos que deseja retornar, essa tela possui os seguintes campos:</p>
<ul>
<li>Mapping Type</li>
<li>Output field name</li>
<li>Data source column Name</li>
<li>Schema Type</li>
<li>Allowed User Roles</li>
</ul>
<p style="text-align: center;"><a href="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem81.png"></a><a href="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem9.png"><img class="aligncenter size-medium wp-image-517" title="Adicionando os parâmetros de saída" src="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem9.png" alt="" width="510" height="302" /></a></p>
<p>Veja como vai ficar com todos nossos campos de saída mapeados</p>
<p style="text-align: center;"><a href="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem10.png"><img class="aligncenter size-medium wp-image-518" title="Mapeamento da query" src="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem10.png" alt="" width="513" height="321" /></a></p>
<p>9. Na próxima tela é para adicionar as operações (métodos) do serviço, cada query vai ter uma operação:</p>
<p style="text-align: center;"><a href="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem13.png"><img class="aligncenter size-medium wp-image-522" title="Criando os métodos" src="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem13.png" alt="" width="530" height="100" /></a></p>
<p>10. Na tela Add New Operation temos um campo para colocar o nome da operação (método) e uma combo para selecionar qual query essa operação vai chamar</p>
<p style="text-align: center;"><a href="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem14.png"><img class="aligncenter size-medium wp-image-523" title="Adicionando uma nova operação" src="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem14.png" alt="" width="512" height="177" /></a></p>
<p>Veja como fica a nossa operação PesquisarFuncionario.</p>
<p style="text-align: center;"><a href="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem15.png"><img class="aligncenter size-medium wp-image-524" title="Operação PesquisarFuncionario" src="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem15.png" alt="" width="513" height="115" /></a></p>
<p>11. Clique em Finish para criar o nosso DataService, não precisamos preencher os Resources. Veja que nosso serviço já é listado.</p>
<p style="text-align: center;"><a href="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem16.png"><img class="aligncenter size-medium wp-image-526" title="Serviço adicionado" src="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem16.png" alt="" width="513" height="144" /></a></p>
<p>12. Vamos fazer o teste para verificar se tudo está correto e funcionando, clique em Try this service</p>
<p style="text-align: center;"><a href="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem17.png"><img class="aligncenter size-medium wp-image-527" title="Testando o serviço" src="http://www.leandroprado.com.br/wp-content/uploads/2010/09/ds_imagem17.png" alt="" width="510" height="212" /></a></p>
<h3>Conclusão</h3>
<p>Criar DataServices usando a ferramenta do WSO2 é muito fácil, intuitivo e produtivo, em apenas alguns minutos conectamos na base de dados, fazemos uma query e retornamos os dados via XML sem escrever nenhuma linha de código.</p>
<p>Os serviços de DataServices também pode ser criados através de um plugin para o eclipse, <a title="WSO2 Data Services Plugin" href="http://wso2.org/library/tutorials/create-dataservice-with-eclipse-dataservice-plugin" target="_blank">veja aqui</a>.</p>
<p>No próximo post estaremos criando a camada de negócio usando o WSAS</p>
<p>Até a próxima!</p>
