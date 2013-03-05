---
slug: criando-servicos-com-o-wso2-parte-3-wso2-esb
publish: true
title: "Criando serviços com o WSO2 - Parte 3 - WSO2 ESB"
kind: article
created_at: 2010-10-13 00:31:33 UTC
author: Leandro Prado
layout: post
external-url: http://www.leandroprado.com.br/2010/10/criando-servicos-com-o-wso2-parte-3-wso2-esb/
categories:
- desenvolvimento
tags:
- wso2
- esb
- enterprise service bus
---

Hoje vamos finalizar o processo para criar um serviço com as ferramenta do WSO2, a última parte vamos publicar nosso serviço na BUS, dessa forma disponibilizando o serviço para nossos clientes.

No WSO2 ESB vamos criar um proxy service que será responsável por chamar nosso serviço Bussiness Service (WSO2 WSAS) que por sua vez vai chamar o nosso Data Service (WSO2 DS), essa parte é basicamente configuração não vamos codificar nenhuma linha de código.

Para expor nosso serviço na BUS vamos seguir os seguintes passos:

## 1) Criar uma Sequence

Um elemento de seqüência é usado para definir uma seqüência de mediadores que podem ser chamados mais tarde, nesse exemplo vamos criar uma sequence com um mediator de Log.

Entre na página de administração do ESB, selecione a opção Sequences.

<a href="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem1.png"><img class="size-thumbnail wp-image-668 aligncenter" title="Menu para criar uma Sequence" src="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem1.png" alt="" /></a>

Clique na opção Add Sequence

<a href="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem2.png"><img class="aligncenter size-medium wp-image-669" title="Adicionar uma Sequence" src="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem2.png" alt="" width="701" height="227" /></a>

Na tela Design Sequence, coloque o nome da sequence como RecursoHumanoSequence e agora vamos adicionar a sequência que vai ser executada, em nosso exemplo temos somente um Log, para isso clique em Add Child -&gt; Core -&gt; Log

<a href="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem3.png"><img class="aligncenter size-medium wp-image-670" title="Configurar a sequence" src="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem3.png" alt="" width="705" height="393" /></a>

Depois de configurado a sequence, clique em Save, nossa sequence será listada na tela Mediation Sequences

<a href="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem4.png"><img class="aligncenter size-medium wp-image-671" title="Listagem das sequences" src="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem4.png" alt="" width="710" height="245" /></a>

## 2) Criar um EndPoint

Um EndPoint é um destino específico de uma mensagem, também podemos ativar as estatísticas de endpoints e WSDL dos endereços.

<strong>Atenção:</strong> Para adicionar um Endpoint, vamos precisar acessar o WSAS para recuperar o endereço do Endpoint do nosso serviço, na página de administração do WSAS entre em List e no serviço RecursoHumanoServico clique na opção WSDL1.1

<a href="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem7.png"><img class="aligncenter size-medium wp-image-674" title="Recuperando o WSDL do WSAS" src="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem7.png" alt="" width="720" height="285" /></a>

O browser será aberto com o WSDL do serviço, no final está as configurações do Endpoint, copie esse endereço para que possamos colar na tela de criação do Endpoint na ESB.

<a href="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem8.png"><img class="aligncenter size-full wp-image-675" title="Recuperando o EndPoint" src="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem8.png" alt="" width="740" height="378" /></a>

Agora vamos voltar ao administrador da ESB, clique na opção Endpoints

<a href="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem5.png"><img class="aligncenter size-full wp-image-672" title="Menu para criar o EndPoint" src="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem5.png" alt="" /></a>

Na nova tela, clique em Address Endpoint

<a href="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem6.png"><img class="aligncenter size-medium wp-image-673" title="Adicionar um EndPoint" src="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem6.png" alt="" width="711" height="239" /></a>

Adicione um nome RecursoHumanoEndPoint e coloque o endereço do Endpoint que recuperamos no WSAS, clique no botão Test para verificar a comunicação entre a ESB e o WSAS

<a href="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem9.png"><img class="aligncenter size-full wp-image-676" title="Configurando o EndPoint" src="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem9.png" alt="" width="718" height="258" /></a>

Clique em Save

<a href="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem10.png"><img class="aligncenter size-full wp-image-677" title="Salvando o EndPoint" src="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem10.png" alt="" width="720" height="184" /></a>

Veja nosso Endpoint na listagem

<a href="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem11.png"><img class="aligncenter size-full wp-image-678" title="Listagem dos EndPoints" src="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem11.png" alt="" width="721" height="192" /></a>

## 3) Criar o Proxy

Clique na opção Add -&gt; Proxy Service

<a href="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem12.png"><img class="aligncenter size-full wp-image-679" title="Menu para criar um Proxy" src="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem12.png" alt="" /></a>

Temos várias opções para criar proxy, clique na opção Custom Proxy

<a href="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem13.png"><img class="aligncenter size-full wp-image-680" title="Adicionar um Custom Proxy" src="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem13.png" alt="" width="722" height="258" /></a>

Vamos configurar nosso proxy da sequinte maneira

 * Proxy Service Name: RecursoHumanoServico
 * Publishing WSDL: Specify source URL
 * WSDL URI: Coloque o endereço do WSDL do WSAS, aonde verificamos anteriormente

Depois clique em Next

<a href="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem14.png"><img class="aligncenter size-full wp-image-681" title="Configurando o Proxy" src="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem14.png" alt="" width="722" height="543" /></a>

Nessa tela vamos configurar a Sequence e o Endpoint que ja criamos anteriormente.

 * In Sequence Options: Selecione Import e na combo selecione a Sequence criada anteriormente
 * Endpoint Options: Selecione Import e na combo selecione o Endpoint criado anteriormente

Depois clique em Next

<a href="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem15.png"><img class="aligncenter size-full wp-image-682" title="Referência a Sequence e ao EndPoint" src="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem15.png" alt="" width="724" height="394" /></a>

Nessa tela não alteramos nada, deixe as duas opções marcadas None, e clique em Finish

<a href="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem16.png"><img class="aligncenter size-full wp-image-683" title="Finalizar a configuração" src="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem16.png" alt="" width="719" height="384" /></a>

Veja na listagem no nosso proxy criado.

<a href="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem17.png"><img class="aligncenter size-full wp-image-684" title="Listagem dos Proxys" src="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem17.png" alt="" width="723" height="315" /></a>

## 4) Testando o serviço

Para testar o serviço clique em Try this service, preencha o campo nome e clique no botão.

<a href="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem18.png"><img class="aligncenter size-full wp-image-685" title="Teste  do serviço" src="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem18.png" alt="" width="721" height="456" /></a>

Quando clicamos no botão fazemos o seguinte caminho:

 # A BUS recebe a requisição
 # Encaminha para o WSAS
 # Valida os dados
 # Chama o DS
 # Retorna os dados para o WSAS
 # Executa regra de negócio
 # Retorna os dados para a BUS

Vamos testar a Exception, não coloque nenhum valor para o parâmetro nome e clique no botão

<a href="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem19.png"><img class="aligncenter size-full wp-image-686" title="Teste da Exception" src="http://www.leandroprado.com.br/wp-content/uploads/2010/10/ESB_imagem19.png" alt="" width="718" height="309" /></a>

Nesse caso fizemos o seguinte caminho:

 # A BUS recebe a requisição
 # Encaminha para o WSAS
 # Valida os dados
 # Retorna erro para a BUS

Chegamos ao fim desse peque How To de como criar um serviço usando as ferramenta do WSO2, espero que possa ter esclarecido as dúvidas. Se ainda tiverem alguma dúvida ou  alguma sugestão, critica favor entre em contato!

Um Abraço!
