---
slug: configurando-o-wso2-com-postgresql
publish: true
title: "Configurando o WSO2 com PostgreSQL"
kind: article
created_at: 2010-10-18 13:47:56 UTC
author: Leandro Prado
layout: post
external-url: http://www.leandroprado.com.br/2010/10/configurando-o-wso2-com-postgresql/
categories:
- desenvolvimento
tags:
- wso2
- postgresql
- data services
- dss
- greg
---

Quando instalamos as ferramentas do WSO2 por padrão vem configurado com o banco <a title="H2 Database" href="http://www.h2database.com/html/main.html" target="_blank">H2</a>, mas hoje vamos ver como alterar para o <a title="PostgreSQL" href="http://www.postgresql.org.br/downloads" target="_blank">PostgreSQL</a> dessa forma deixando nossa arquitetura mais robusta.

## 1. Configurando a base

Primeiro de tudo temos que criar a base de dados no Postgre, para isso vamos utilizar a ferramenta PgAdmin que ja vem na instalação do PostgreSQL. Abra o PgAdmin e clique com o botão direito em cima de DataBases e selecione a opção New Database.

<a href="http://www.leandroprado.com.br/wp-content/uploads/2010/10/postgre_imagem1.png"><img class="aligncenter size-full wp-image-697" title="Criando a DataBase" src="http://www.leandroprado.com.br/wp-content/uploads/2010/10/postgre_imagem1.png" alt="" width="335" height="278" /></a>

Na nova janela coloque o nome da nova database de <strong>gregdb</strong> e clique em OK

<a href="http://www.leandroprado.com.br/wp-content/uploads/2010/10/postgre_imagem2.png"><img class="aligncenter size-full wp-image-698" title="Configurando a DataBase" src="http://www.leandroprado.com.br/wp-content/uploads/2010/10/postgre_imagem2.png" alt="" width="374" height="547" /></a>

Agora vamos criar um novo usuário, clique com o botão direito em cima de Login Roles e selecione a opção New Login Role

<a href="http://www.leandroprado.com.br/wp-content/uploads/2010/10/postgre_imagem3.png"><img class="aligncenter size-full wp-image-699" title="Criando um novo usuário" src="http://www.leandroprado.com.br/wp-content/uploads/2010/10/postgre_imagem3.png" alt="" /></a>

Na nova janela configure da seguinte maneira:

 * Role Name: **gregadmin**
 * Password: **gregadmin**
 * Password (again): **gregadmin**

Para finalizar clique em OK

<a href="http://www.leandroprado.com.br/wp-content/uploads/2010/10/postgre_imagem4.png"><img class="aligncenter size-full wp-image-700" title="Configuração do Login" src="http://www.leandroprado.com.br/wp-content/uploads/2010/10/postgre_imagem4.png" alt="" width="429" height="454" /></a>

## 2. Configurando o Registry

Agora vamos alterar as configurações do Registry, abra o arquivo registry.xml que se encontra no diretório $GREG_HOME/repository/conf, onde $GREG_HOME é o local onde  está instalado o WSO2 Governance Registry, e adicione as seguintes linhas.

<pre class="brush: xml; title: ; notranslate">
&lt;dbConfig name=&quot;postgresql-db&quot;&gt;
    &lt;url&gt;jdbc:postgresql://localhost:5432/gregdb&lt;/url&gt;
    &lt;userName&gt;gregadmin&lt;/userName&gt;
    &lt;password&gt;gregadmin&lt;/password&gt;
    &lt;driverName&gt;org.postgresql.Driver&lt;/driverName&gt;
    &lt;maxActive&gt;80&lt;/maxActive&gt;
    &lt;maxWait&gt;60000&lt;/maxWait&gt;
    &lt;minIdle&gt;5&lt;/minIdle&gt;
&lt;/dbConfig&gt;
</pre>

Explicando a configuração:

 * url: Endereço JDBC para o banco
 * username: Usuário para conectar ao banco
 * password: Senha do usuário
 * driverName: Nome do driver
 * maxActive: O número máximo de conexões ativas
 * maxWait: O número máximo de milissegundos que o pool de espera para uma conexão ser devolvido
 * minIdle: O número mínimo de conexões ativas que pode permanecer inativo no pool

<p>Depois de criado a conexão temos que ativa-la, altere a opção <strong>currentDBConfig</strong> para a coneão que acabamos de criar.</p>
<pre class="brush: xml; title: ; notranslate">
&lt;currentDBConfig&gt;postgresql-db&lt;/currentDBConfig&gt;
</pre>
<p>Agora vamos editar o arquivo user-mgt.xml que se encontra no mesmo diretório ($GREG_HOME/repository/conf) e faça a seguinte alteração.</p>
<pre class="brush: xml; title: ; notranslate">
&lt;Configuration&gt;
    ...
    &lt;Property name=&quot;url&quot;&gt;jdbc:postgresql://localhost:5432/gregdb&lt;/Property&gt;
    &lt;Property name=&quot;userName&quot;&gt;gregadmin&lt;/Property&gt;
    &lt;Property name=&quot;password&quot;&gt;gregadmin&lt;/Property&gt;
    &lt;Property name=&quot;driverName&quot;&gt;org.postgresql.Driver&lt;/Property&gt;
    &lt;Property name=&quot;maxActive&quot;&gt;50&lt;/Property&gt;
    &lt;Property name=&quot;maxWait&quot;&gt;60000&lt;/Property&gt;
    &lt;Property name=&quot;minIdle&quot;&gt;5&lt;/Property&gt;
&lt;/Configuration&gt;
</pre>
<h2>3. Adicionando o Driver</h2>
<p>Para que nossa conexão com o banco funcione, temos que fazer o download do driver JDBC em <a title="PostgreSQL JDBC" href="http://jdbc.postgresql.org/download.html" target="_blank">http://jdbc.postgresql.org/download.html</a>, baixe a versão JDBC4 e depois copie o JAR para o diretório $GREG_HOME/repository/components/lib</p>
<h2>4. Criando a base</h2>
<p>Para finalizar, vamos criar as tabelas na base, para isso temos que iniciar o serviço do Registy com a opção -Dsetup.</p>
<pre class="brush: xml; title: ; notranslate">
./wso2server.sh -Dsetup
</pre>
<p><strong>ATENÇÃO:</strong> Essa opção só deve ser executada apenas uma vez</p>
<p>Vamos acessar o PgAdmin e verificar se as tabelas foram criadas</p>
<p><a href="http://www.leandroprado.com.br/wp-content/uploads/2010/10/postgre_imagem5.png"><img class="aligncenter size-full wp-image-706" title="postgre_imagem5" src="http://www.leandroprado.com.br/wp-content/uploads/2010/10/postgre_imagem5.png" alt="" width="275" height="347" /></a></p>
<h2>5. Configurando o DS, WSAS, ESB</h2>
<p>Depois de ter criado a base do Registry, podemos configurar os outros servers para se comunicar com a base Postgre. Basicamente é o mesmo processo temos que editar o arquivo registry.xml adicionando as configurações de conexão com o banco.</p>
<p><strong>Data Services </strong></p>
<ul>
<li>Abra o arquivo $DS_HOME/repository/conf/registry.xml e adicione a configuração do Postgre conforme descrito acima</li>
<li>Abra o arquivo $DS_HOME/repository/conf/user-mgt.xml e altere a configuração de conexão conforme descrito acima</li>
<li>adicione o jar no diretório $DS_HOME/repository/components/lib</li>
</ul>
<p><strong>Application Services</strong></p>
<ul>
<li>Abra o arquivo $WSAS_HOME/repository/conf/registry.xml e adicione a configuração do Postgre conforme descrito acima</li>
<li>Abra o arquivo $WSAS_HOME/repository/conf/user-mgt.xml e altere a configuração de conexão conforme descrito acima</li>
<li>adicione o jar no diretório $WSAS_HOME/repository/components/lib</li>
</ul>
<p><strong>Enterprise Service Bus</strong></p>
<ul>
<li>Abra o arquivo $ESB_HOME/repository/conf/registry.xml e adicione a configuração do Postgre conforme descrito acima</li>
<li>Abra o arquivo $ESB_HOME/repository/conf/user-mgt.xml e altere a configuração de conexão conforme descrito acima</li>
<li>adicione o jar no diretório $ESB_HOME/repository/components/lib</li>
</ul>
<p>Depois de alterado as configurações, podemos iniciar os serviços normalmente (sem a opção -Dsetup)</p>
<p>Agora nosso ambiente está configurado para usar o PostgreSQL, se você quiser usar o MySQL, Oracle, SQLServer como SGBD pode usar esses mesmos passos apenas alterando as configurações de conexão.</p>
<p>Até a próxima!</p>
