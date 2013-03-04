---
author: José Nogueira
date: '2011-02-24 19:30:30'
layout: post
slug: seguranca-de-informacoes-atraves-de-filtragem-de-dados-no-wso2-data-services
comments: true
status: publish
title: ' Segurança de informações através de filtragem de dados no WSO2 Data Services'
categories:
- desenvolvimento
tags:
- data services
- dss
- identity
- segurança
- ws-security
- wso2
- wss
- xml encryption
- xml signature
---

[![](http://assets.mcorp.com.br/wp-content/uploads/2011/02/cadeado-300x199.jpg)](http://assets.mcorp.com.br/wp-content/uploads/2011/02/cadeado.jpg)

Em alguns casos, podemos nos deparar com a necessidade de confidencializar
alguns dados no retorno de [Data Services](http://www.mcorp.com.br/glossario/#DataServices),
exibindo-os apenas
para determinados grupos de usuários, tanto por questão de segurança (quando
algum grupo específico não pode ter acesso a algumas informações),  quanto por
não ter a necessidade de utilizar esse retorno, para que assim não precisemos
criar dois serviços com a mesma finalidade. O WSO2 Data Services Server
oferece a possibilidade de filtrar esses dados no retorno de uma _query_,
através do [WS-Security](http://www.mcorp.com.br/glossario/#WS-Security) (tem
como foco principal o uso de [XML Signature](http://www.mcorp.com.br/glossario
/#XML-Signature) e [XML Encryption](http://www.mcorp.com.br/glossario/#XML-Encryption)). Nesse caso irei exemplificar a seguinte situação: um serviço que
retorna dados referente aos funcionários, sendo consumido por dois
departamentos: o RH (que necessita dos dados referente aos pagamentos dos
honorários) e o setor de segurança (que utiliza apenas os dados cadastrais
para acesso dos funcionários as dependências da empresa).

Iremos utilizar nesse exemplo o WSO2 Data Services Server em sua versão 2.5.1
(nesse caso considerando um conhecimento básico da suíte
[WSO2](http://www.mcorp.com.br/glossario/#WSO2), caso contrário consulte os
[_posts_ relacionados ao WSO2](http://www.mcorp.com.br/tag/wso2)):

  * [Criando um ambiente SOA com WSO2](http://www.leandroprado.com.br/2010/07/criando-um-ambiente-soa-com-wso2/)
  * [Criando serviços com WSO2 Data Services](http://www.leandroprado.com.br/2010/09/criando-servicos-com-o-wso2-parte-1-wso2-data-services/)

Supondo que possuímos o banco de dados, com uma tabela simples chamada de
TB_FUNCIONARIOS, com os campos: ID, NOME E SALARIO.

## Etapa 1 - Criando o usuário

Logado ao WSO2 Data Services Server vá em "Home > Configure > User Management > Users",
para que possamos criar novos usuários, nesse caso criaremos os
usuários "Maria" que faz parte do departamento de RH da empresa e "Joao" que
faz parte da segurança do prédio. Click em "Add User" para preenchermos os
dados do usuário que será cadastrado.

[![add user wso2](http://assets.mcorp.com.br/wp-content/uploads/2011/02/figura1.0-add-user-wso2-300x205.jpg)](http://assets.mcorp.com.br/wp-content/uploads/2011/02/figura1.0-add-user-wso2.jpg)

Após inserir os dados do usuário, clicar em "finish", repetir o procedimento
pro cadastro do outro usuário. Podemos listar os usuários criados como mostra
a imagem.

[![list user wso2](http://assets.mcorp.com.br/wp-content/uploads/2011/02/figura1.1-list-user-wso2-300x149.jpg)](http://assets.mcorp.com.br/wp-content/uploads/2011/02/figura1.1-list-user-wso2.jpg)

## Etapa 2 - Criando grupos de usuários

Com nossos usuários criados, vamos gerar um grupo para vincular ao perfil do
usuário. Vá em "Home > Configure > Users and Roles > Roles", serão listados os
grupos existentes no WSO2, clique em "Add New Role" que abrirá a tela para
cadastrarmos os grupos.

Crie um grupo com o nome "RecursosHumanos", em seguida clique em "next",
aparecerá a tela com os flags de permissões e previlégios para os membros do
grupo. Nesse caso vamos selecionar a opção "All permissions", para que sejam
marcadas todas as opções. Enquanto estamos criando o grupo, já podemos
vincular os usuários que farão parte do mesmo, faça uma busca listando todos
os usuários e selecione o usuário "Maria" criado anteriormente, como na imagem
abaixo e finalize.

[![select user wso2](http://assets.mcorp.com.br/wp-content/uploads/2011/02/figura1.2-select-user-wso2-300x170.jpg)](http://assets.mcorp.com.br/wp-content/uploads/2011/02/figura1.2-select-user-wso2.jpg)

Agora usando o mesmo processo vamos criar o grupo "Seguranca". Observe que
quando selecionamos algum usuário criado e vinculado ao grupo, o mesmo possui
um ou vários grupos selecionados.

[![roles of users wso2](http://assets.mcorp.com.br/wp-content/uploads/2011/02/figura1.3-roles-of-users-wso2-300x176.jpg)](http://assets.mcorp.com.br/wp-content/uploads/2011/02/figura1.3-roles-of-users-wso2.jpg)

## Etapa 3 - Filtrando dados da consulta

Com os usuários e grupos devidamente criados vamos finalmente ao que
interessa, filtrar os dados de acordo com o perfil de cada grupo. Considerando
que já exista um serviço "empresa", vamos criar o método
"pesquisarFuncionario" para demonstrar como filtrar os dados de retorno do
método. Nesse caso, o método nos retornará os campos "ID" e "NOME" para o
grupo Segurança, e "ID", "NOME" e "SALARIO" para o grupo RecursosHumanos.

Iremos em "Home > Manage > Services > List > Service Dashboard > Service
Details > Data Sources > Queries",  para inserirmos nosso novo método.
Preenchemos com o SQL, o campo de entrada, e na hora em que formos preencher o
retorno será onde a "mágica" acontecerá.

[![edit query wso2](http://assets.mcorp.com.br/wp-content/uploads/2011/02/figura1.4-edit-query-wso2-300x176.jpg)](http://assets.mcorp.com.br/wp-content/uploads/2011/02/figura1.4-edit-query-wso2.jpg)

No item "Add new output Mapping" abriremos a tela para cadastrar um novo campo
de retorno, preenchemos o tipo do campo, o nome de saída e o nome do campo no
SQL. Abaixo dessas opções temos o item "Allowed User Roles", aonde aparecerão
os grupos que criamos anteriormente, para os campos "ID E NOME" selecionaremos
ambos os grupos, no caso do campo "SALARIO" selecionaremos apenas o grupo
RecursosHumanos, com o método criado mostraremos como consumir esse método
filtrando os dados.

[![add edit output mapping wso2](http://assets.mcorp.com.br/wp-content/uploads/2011/02/figura1.5-add-edit-output-mapping-wso2-300x160.jpg)](http://assets.mcorp.com.br/wp-content/uploads/2011/02/figura1.5-add-edit-output-mapping-wso2.jpg)

## Etapa 4 - Testando a filtragem de dados

Agora vamos abrir a opção " Home > Manage > Services > List > Service
Dashboard > Security for the service > Activate Security > Service Dashboard >
Security for the service", selecionamos a opção "yes" no combo e setamos o
flag "UsernameToken", assim estaremos habilitando segurança por grupo e
usuário do cliente.

[![security for the service wso2](http://assets.mcorp.com.br/wp-content/uploads/2011/02/figura1.6-security-for-the-service-wso2-300x130.jpg)](http://assets.mcorp.com.br/wp-content/uploads/2011/02/figura1.6-security-for-the-service-wso2.jpg)

Simulando a execução do serviço, no próprio WSO2 Data Services Server, podemos
perceber que aparecem as opções "username" e "password". O retorno será
filtrado de acordo com o usuário que for preenchido nesses campos. Executando
a consulta, notaremos que o campo "SALARIO" só aparece no retorno se
utilizarmos o usuário "Maria".

[![full return service wso2](http://assets.mcorp.com.br/wp-content/uploads/2011/02/figura1.9-full-return-service-wso2-300x126.jpg)](http://assets.mcorp.com.br/wp-content/uploads/2011/02/figura1.9-full-return-service-wso2.jpg)

[![parcial return service wso2](http://assets.mcorp.com.br/wp-content/uploads/2011/02/figura1.8-parcial-return-service-wso2-300x128.jpg)](http://assets.mcorp.com.br/wp-content/uploads/2011/02/figura1.8-parcial-return-service-wso2.jpg)

Espero ter colaborado, sugestões e criticas são sempre bem vindas, focando o
objetivo de transformar a comunidade [WSO2 Brasil](http://www.wso2brasil.com.br/) cada vez mais forte, até o próximo
post.

Post baseado no artigo "[content filtering data services user roles](http://wso2.org/library/articles/content-filtering-data-services-user-roles)" de Anjana Fernando - Software Engineer WSO2.

Pode ser visto um exemplo de [consumo um servico seguro utilizando php](http://www.mcorp.com.br/2010/03/consumindo-um-servico-seguro-utilizando-php/).
