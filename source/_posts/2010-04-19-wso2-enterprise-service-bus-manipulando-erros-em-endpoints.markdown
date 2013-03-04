---
author: Leonardo Saraiva
date: '2010-04-19 11:54:27'
layout: post
slug: wso2-enterprise-service-bus-manipulando-erros-em-endpoints
comments: true
status: publish
title: WSO2 Enterprise Service Bus - Manipulando erros em Endpoints
categories:
- desenvolvimento
tags:
- endpoint
- enterprise service bus
- erro
- esb
- fail-over
- falha
- manipulação
- wso2
---

A manipulação de erros em _endpoints_ é uma situação crítica e importante em
qualquer publicação da [WSO2 Enterprise Service Bus](http://wso2.org/projects/esb/java). Neste artigo, [SupunKamburugamuva](http://wso2.com/about/engineers/supun-kamburugamuva/) descreveu
como manipular os erros no nível de _endpoint_.

**Nota de tradução:** O artigo original foi escrito em inglês e pode ser lido em: [WSO2 Enterprise Service Bus - Endpoint Error Handling ](http://wso2.org/library/articles/wso2-enterprise-service-bus-endpoint-error-handling)

## WSO2 Enterprise Service Bus - Manipulando erros em _endpoints_

### Conteúdo

  * [Terminologia](#ManipulandoErrosEndpoint_Terminologia)
  * [Introdução](#ManipulandoErrosEndpoint_Introducao)
  * [Qual a importância da manipulação de erros?](#ManipulandoErrosEndpoint_Importante)
  * [Conceitos](#ManipulandoErrosEndpoint_Conceitos)
  * [Situações de _endpoint_](#ManipulandoErrosEndpoint_SituacoesEndpoint)
    * [_Active_](#ManipulandoErrosEndpoint_SituacoesEndpointActive)
    * [_Timeout_](#ManipulandoErrosEndpoint_SituacoesEndpointTimeout)
    * [_Suspended_](#ManipulandoErrosEndpoint_SituacoesEndpointSuspended)
  * [Configurações do _Leaf endpoint_](#ManipulandoErrosEndpoint_ConfiguracaoEndpoint)
    * [Exemplo de configuração](#ManipulandoErrosEndpoint_ConfiguracaoEndpointExemplo)
  * [_Fail-Over Endpoint_](#ManipulandoErrosEndpoint_FailOverEndpoint)
    * [Exemplo de configuração](#ManipulandoErrosEndpoint_FailOverEndpointExemplo)
  * [Conclusão](#ManipulandoErrosEndpoint_Conclusao)
  * [Apêndice A](#ManipulandoErrosEndpoint_ApendiceA)

### <a name="ManipulandoErrosEndpoint_Terminologia"></a>Terminologia

_Service Provider endpoint_: WSO2 Enterprise Service Bus atua como uma central
de distribuição, entregando as mensagens recebidas dos clientes aos _service
provider endpoints_.

_WSO2 Enterprise Service Bus Endpoint_: Esta é a representação do _service
provider endpoint_, omitida internamente na configuração do WSO2 Enterprise
Service Bus.

### <a name="ManipulandoErrosEndpoint_Introducao"></a>Introdução

Corporações são complexamente estruturadas e compostas por centenas de
aplicações com semânticas completamente diferentes. Algumas dessas aplicações
são desenvolvidas personalizadamente, algumas são adquiridas de terceiros e
outras podem ser a combinação de ambas; e podem ser operadas em diferentes
ambientes e sistemas. Muitas aplicações rodam em diferentes sistemas, o que
faz isso ser muito complexo. E devido a esses fatores, isto é vital a
integração entre as diferentes aplicações.

O WSO2 Enterprise Service Bus tem a capacidade de prover a tecnologia para
integrar essas aplicações, as quais podem ser definidas como o estado da arte
para [EAI](http://pt.wikipedia.org/wiki/EAI), baseadas nos princípios do
[SOA](/glossario/#SOA). Com a WSO2 Enterprise Service Bus, o processo completo
pode ser alcançado pela realização de várias tarefas na mensagem -
transformação (_transformation_), roteamento (_routing_) e troca de transporte
(_transport switching_) - antes do envio ao _service provider_.

A configuração no WSO2 Enterprise Service Bus é feita em etapas, são elas:

  * _Mediators_
  * _Proxy services_
  * _Endpoints_
  * _Tasks_

Os_ Mediators_ são componentes funcionais dentro do WSO2 Enterprise Service
Bus, eles fazem várias coisas como gravação de log (_logging_), transformação
(_XSLT transformation_), envia mensagens externas, filtros baseados em
_XPath_, etc. Então os _mediators_ são o núcleo da mensagem processada dentro
do WSO2 Enterprise Service Bus. A última etapa da mensagem dentro do WSO2
Enterprise Service Bus é o envio da mensagem de resposta para um _services
provider_. Quanto ao WSO2 Enterprise Service Bus é responsável pelo envio da
mensagem para um serviço de escuta de _endpoint_. As mensagens enviadas do
WSO2 Enterprise Service Bus podem ser muito diferentes da mensagem recebida.
Por exemplo, as mensagens recebidas podem ser _SOAP 1.1 over HTTP_. Mas WSO2
Enterprise Service Bus pode enviar a mensagem para o serviço como _SOAP 1.2
over JMS_. Neste caso o _endpoint_ exposto para o cliente é _SOAP 1.1 over
HTTP_, o atual _endpoint_ é _SOAP 1.2 over JMS_.

Um Endpoint é uma abstração do _services provider_. Uma vez que a mensagem é
enviada usando um Mediator, ele deve saber qual é o _endpoint services
provider_. O Endpoint é capaz de prover essa informação. No cenário ideal o
serviço de endpoint aceita requisições de mesmo tipo, WSO2 ESB pode ser usado
para balanceamento de carga (Load Balancer). A principal razão por trás disso
tudo é que esses endpoints tem mesmas funcionalidades e é natural vê-las como
uma coisa só.

WSO2 Enterprise Service Bus tem o conceito de construção de endpoints para
representar _endpoint services provider_. Seguindo os Endpoints construídos
sobre o WSO2 Enterprise Service Bus.

  1. Address Endpoint
  2. WSDL Endpoint
  3. Default Endpoint
  4. Load Balancing Endpoint
  5. Fail-Over Endpoint

Dos itens mencionados acima, os mais utilizados são o Address e o WSDL
Endpoints. Cada Endpoint tem seu próprio XML de configuração, escrito na
linguagem Synapse. Synapse é uma linguagem XML usada para configurar a
Enterprise Service Bus.

Até o Endpoint enviar a mensagem de resposta, pode encontrar vários erros de
transporte. Por exemplo, a conexão pode dar timeout ou pode ser fechada pelo
serviço atual.

### <a name="ManipulandoErrosEndpoint_Importante"></a>Qual a importância da manipulação de erros?

WSO2 Enterprise Service Bus é uma aplicação de longa duração e nesse tempo
falhas podem ocorrer. Retiring on transient failures enhances the fault
tolerance of a system. Para a WSO2 Enterprise Service Bus, essas falhas podem
ser falha de conexão entre o _services provider_ e a WSO2 Enterprise Service
bus, erro em alguma operação do banco de dados e assim por diante, sendo que
as falhas de comunicação são mais frequentes.

Então a manipulação de erros é a chave para o sucesso de qualquer publicação
na Enterprise Service Bus. Muitas vezes nós utilizamos TCP, as pessoas podem
perguntar, como podem ocorrem erros? O protocolo TCP é muito confiável, não é?
Mas não na vida real. Mensagens pode falhar ou se perder devido a diversas
razões na rede TCP. Esses erros são muito raros, mas podem ocorrer. Para
entender a importância da manipulação de erros vamos considerar o seguinte
cenário.

Se a WSO2 Enterprise Service Bus não estiver devidamente configurada para
aceitar erros, ocasionalmente, quando eles ocorrerem, o Endpoint será marcado
com uma falha. Isto leva para uma mensagem de falha. Por padrão, o Endpoint
será marcado como falho por um longo tempo. Os erros encontrados na WSO2
Enterprise Service Bus podem ser um problema intermitente que ocorrem uma vez
por semana, mas devido a singularidade do erro, mensagens posteriores poderão
ser perdidas. Claro que você pode configurar a WSO2 Enterprise Service Bus
para manipular estas situações e este artigo dará a você uma maior compreensão
sobre como trabalhar com Endpoints e otimizar as suas configurações.

### <a name="ManipulandoErrosEndpoint_Conceitos"></a>Conceitos

Nós chamamos Address, Default and WSDL Endpoints como Leaf Endpoints, que
enviam a mensagem. A Load Balance ou Fail-Over Endpoints usa um ou vários Leaf
Endpoints para enviar a mensagem. Então um Load Balance ou Fail-Over Endpoint
é um agrupamento lógico de Leaf Endpoints. Um Load Balance ou Fail-Over
Endpoint nunca envia uma mensagem diretamente, ao invés de enviar ela delega
aos Leaf Endpoints, dependendo da configuração e da situação (status).

Endpoint é uma abstração do servidor remoto, onde o WSO2 Enterprise Service
Bus envia a mensagem de saída. Ela pode especificar quais as propriedades
usadas para enviar a mensagem, por exemplo, pode especificar o formato - como
SOAP 1.1 - ou pode especificar a necessidade de utilizar uma política de
segurança com WS Security para responder a mensagem.

WSO2 Enterprise Service Bus Endpoint tem configurações para especificar o
comportamento diante de erros, que podem ocorrer entre a WSO2 Enterprise
Service Bus e o atual Endpoint.

Um Endpoint tem uma situação, mas antes vamos para as configurações de
Endpoint para vermos como as transições acontecem.

### <a name="ManipulandoErrosEndpoint_SituacoesEndpoint"></a>Situações do Endpoint

Em alguns momentos a situação do Endpoint pode ser Active, Timeout, Suspended
ou Off. A situação de transição do Endpoint normalmente acontece na base de
mensagens. E para colocarmos uma situação de Off num Endpoint (utilizando para
issoJMX), então esta situação não é a Situação do Diagrama de Transição. Vamos
analisar as diferentes situações do endpoint em detalhes:

  * Active: O endpoint está ativo e funcionando.
  * Timeout: Foram encontrados erros no endpoint, que passa a ser um candidato a ser suspenso, mas pode continuar enviando mensagens. Se os erros persisterem o endpoint será suspenso.
  * Suspended: Foram encontrados erros no endpoint e é enviado para a situação onde não pode enviar requisições. Ele não pode enviar mensagens e mensagens recebidas por ele resultarão em falhas.
  * Off: O endpoint não está ativo.

[!["Toda situação de transição acontece na mensagem. Por exemplo, se a duração da suspensão é expirada, na situação Suspended, o endpoint continuará na situação Suspensed até que uma nova mensagem chegue e seja bem sucedida."](http://assets.mcorp.com.br/wp-content/uploads/2010/04/state_2.png "Toda situação de transição acontece na mensagem. Por exemplo, se a duração da suspensão é expirada, na situação Suspended, o endpoint continuará na situação Suspensed até que uma nova mensagem chegue e seja bem sucedida.")](http://assets.mcorp.com.br/wp-content/uploads/2010/04/state_2.png)

Toda situação de transição acontece na mensagem. Por exemplo, se a duração da
suspensão é expirada, na situação Suspended, o endpoint continuará na situação
Suspensed até que uma nova mensagem chegue e seja bem sucedida.

#### <a name="ManipulandoErrosEndpoint_SituacoesEndpointActive"></a>Active

Quando o WSO2 Enterprise Service Bus inicializa, os endpoints estão ativos (na
situação Active) e prontos para enviar mensagens. Se o usuário não desligar os
endpoints (situação Off), será Active até que ocorra um erro.

Quando ocorrer um erro, o Endpoint poderá ser configurado como: Active,
Timeout ou Suspended. Todo erro tem um código. As configurações de Endpoint
possibilitam que você defina os erros que colocarão o Endpoint nos modos
Timeout e Suspension. Se um erro não foi definido como Timeout ou Suspended,
será ignorado.

Os erros são manipulados de três formas:

  * Endpoint na situação SUSPENDED
  * Endpoint na situação TIMEOUT
  * Ignorado e mantido no ACTIVE

Se um erro específico não possui um _timeout_ configurado, então a conexão
será fechada e o erro será tratado como TIMEOUT. Todos os outros erros terão o
Endpoint colocado como SUSPENDED.

Quando um erro ocorrer no Endpoint, será visto primeiramente se ele é um erro
para colocar na situação TIMEOUT. Caso contrário, será verificado se é para
colocar na situação SUSPENDED.

#### <a name="ManipulandoErrosEndpoint_SituacoesEndpointTimeout"></a>Timeout

Nesta situação o Endpoint pode ter na mensagem encaminhada um número máximo de
tentativas. Se as falhas persistirem e o número máximo for excedido, o
Endpoint será marcado como SUSPENDED. Mas se alguma mensagem for processada o
Endpoint será marcado como ACTIVE.

Por exemplo, vamos dizer que o número de tentativas é 3 para esta situção. Se
as próximas três mensagens são enviadas usando este Endpoint, e encontramos um
erro, o endpoint é colocado como SUSPENDED. Mas se alguma das mensagens
anteriores for bem sucedida neste Endpoint, que estava SUSPENDED, ele então
será colocado como ACTIVE.

#### <a name="ManipulandoErrosEndpoint_SituacoesEndpointSuspended"></a>Suspended

Um endpoint suspended não pode ser usado para enviar mensagens. Depois que o
endpoint é colocado nesta situação, pode ser tentado novamente após o tempo
configurado. Depois deste de passado o tempo de expiração, o WSO2 Enterprise
Service Bus tentará encaminhar as mensagens deste endpoint. Se a mensagem for
bem-sucedida, então o WSO2 Enterprise Service Bus marcará este endpoint como
ACTIVE. Se a próxima mensagem falhar, o endpoint será colocado como SUSPENDED
ou TIMEOUT dependendo do erro que ocorrer.

O próximo período é calculado usando a seguinte fórmula:

    Next suspension time period = Max (Initial Suspension duration * (progression factor try count), Maximum Duration)

Todas as variáveis da fórmula acima são valores configurados usados para
calcular o número de tentativas (contabilizadas após o endpoint ser marcado
SUSPENDED). Com a incrementação do número de tentativas (try count), o próximo
período de suspensão (next suspension time period) também será incrementado. O
incremento é vinculado a máxima duração (maximum duration).

### <a name="ManipulandoErrosEndpoint_ConfiguracaoEndpoint"></a>Configurações do Leaf Endpoint

Esta é a configuração do endereço do endpoint. Uma vez que estamos
interessados apenas nas configurações de erros, as mesmas também podem ser
aplicadas aos WSDL Endpoints. As configurações de maninpulação de erros são:

  1. timeout
  2. markForSuspension
  3. suspendOnFailure

Vamos ver as configurações individualmente.

{% gist 2907143 %}

#### Timeout

<table>
  <thead>
    <tr>
      <th>Nome</th>
      <th>Valores</th>
      <th>Default</th>
      <th>Descrição</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>duration</td>
      <td>miliseconds</td>
      <td>60000</td>
      <td>Tempo máximo de conexão. Se o endpoint remoto não responder neste tempo, ele será tratado como timeout</td>
    </tr>
    <tr>
      <td>action</td>
      <td>discard, fault, none</td>
      <td>none</td>
      <td>Tempo para descartar, invocará uma exceção (fault handler) ou responderá como tempo de execução excedido</td>
    </tr>
  </tbody>
</table>

#### markForSuspension

<table>
  <thead>
    <tr>
      <th>Nome</th>
      <th>Valores</th>
      <th>Padrão</th>
      <th>Descrição</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>errorCodes</td>
      <td>Códigos de erro separados por vírgula</td>
      <td>101504, 101505</td>
      <td>Lista de erros que envia o endpoint na situação &#8220;TIMEOUT retriesBeforeSuspension&#8221;</td>
    </tr>
    <tr>
      <td>retriesBeforeSuspension</td>
      <td>Integer</td>
      <td>0</td>
      <td>Na situação TIMEOUT o número de tentativas é igual ao número de requisições menos um e pode falhar antes do endpoint ser marcado como &#8220;SUSPENDED retryDelay&#8221;. Esta configuração é por Endpoint e não por mensagem. Muitas mensagens podem ser tentadas ao mesmo tempo e falhar, com isso o número de tentativas restantes será reduzido.</td>
    </tr>
    <tr>
      <td>retryDelay</td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
  </tbody>
</table>

#### suspendOnFailure

<table>
  <thead>
    <tr>
      <th>Nome</th>
      <th>Valores</th>
      <th>Padrão</th>
      <th>Descrição</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>errorCodes</td>
      <td>Códigos de erro separados por vírgula</td>
      <td>Todos os erros, exceto os especificados em markForSuspension</td>
      <td>Erros que enviam o endpoint para a situação SUSPENDED</td>
    </tr>
    <tr>
      <td>initialDuration</td>
      <td>miliseconds</td>
      <td>60 x 60 x 1000</td>
      <td>Depois que um endpoint fica SUSPENDED, esperará por essa quantidade de tempo antes de tentar enviar a mensagem. Todas as mensagens que forem recebidas durante este período resultarão na ativação de <em>fault sequence</em>.</td>
    </tr>
    <tr>
      <td>progressionFactor</td>
      <td>Integer</td>
      <td>1</td>
      <td>O endpoint tentará enviar as mensagens depois da <em>initialDuration</em>. Utilizando a fórmula: next duration = Max(initialDuration x progressionFactor ^ retry count, maximumDuration)</td>
    </tr>
    <tr>
      <td>maximunDuration</td>
      <td>miliseconds</td>
      <td>Long.MAX_VALUE</td>
      <td>Limite superior da duração de tentativas</td>
    </tr>
  </tbody>
</table>

#### <a name="ManipulandoErrosEndpoint_ConfiguracaoEndpointExemplo"></a>Exemplo de configuração

{% gist 2907164 %}

Aqui nós mudamos a situação TIMEOUT do endpoint para os erros 101504 e 101505.
Depois desse processo, três requisições podem falhar por um ou desses erros
antes de alterar a situação do endpoint para SUSPENDED.

Nós colocamos o endpoint em suspensão para os erros 101500, 101501, 101506,
101507 e 101508. Mas como você pode ver, nós ignoramos o erro 101503. Se o
erro 101503 ocorrer, o endpoint será marcado como ACTIVE.

Para mais informações sobre códigos de erro, ver APÊNDICE A.

### <a name="ManipulandoErrosEndpoint_FailOverEndpoint"></a>Fail-Over Endpoint

Com essa configuração, se ocorrer um erro durante o processo de transmissão da
mensagem, a mesma será perdida. A mensagem que falhou não terá uma nova
tentativa de envio. Esses erros ocorrem raramente, mas falhas em mensagens
ainda podem ocorrer. Em algumas aplicações essas falhas nas mensagens perdidas
são aceitáveis, mas algumas vezes essas falhas não são aceitáveis e o Fail-
Over endpoint é a solução ideal.

Abaixo uma configuração para fail-over endpoints. No nível de configuração, um
fail-over é um agrupamento lógico de um ou mais endpoints.

{% gist 2907546 %}

Quando uma mensagem chega a situação Fail-Over, será atráves da lista de fail-
over endpoints que escolherá a primeira situação entre ACTIVE ou TIMEOUT.
Então será enviada a mensagem usando esse endpoint. Se ocorrer um erro
enquanto a mensagem é enviada, o fail-over, através da lista de endpoints, irá
começar novamente e tentará enviar a mensagem usando o primeiro endpoint.

Alguns erros colocam o endpoint na situação TIMEOUT e outros deixam o endpoint
com a situação ACTIVE. Nesses casos as tentativas acontecem usando o mesmo
endpoint. Se ocorrer um erro com o primeiro endpoint do grupo fail-over e esse
erro não colocar o endpoint como SUSPENDED, as próximas tentativas ocorrerão
usando o mesmo endpoint.

O fail-over dá a prioridade para o primeiro endpoint que não esteja como
SUSPENDED. Então será enviada a mensagem através do primeiro endpoint do grupo
fail-over, enquanto não for marcado como SUSPENDED. Quando o primeiro endpoint
é marcado como SUSPENDED as requisições serão enviadas usando o segundo
endpoint. Quando o primeiro endpoint estiver pronto para ser utilizado
novamente, ele tentará de novo, mesmo que o segundo endpoint ainda esteja
ativo.

Se houver apenas um serviço endpoint e falhas não são toleráveis, os fail-
overs são possíveis com apenas um endpoint.

Abaixo um exemplo de fail-over com um endpoint.

#### <a name="ManipulandoErrosEndpoint_FailOverEndpointExemplo"></a>Exemplo de configuração de Fail-Over Endpoint

{% gist 2907774 %}

Nesse exemplo (Sample_First) o endpoint é marcado como TIMEOUT quando a
conexão excede o tempo máximo de duração, a conexão é fechada ou envia erros
de IO, respectivamente, os códigos de erro: 101504, 101505 e 101500. Para
todos os outros erros, será marcado como SUSPENDED. Quando esse erro ocorrer,
o fail-over tentará usando o primeiro endpoint que não estiver SUSPENDED,
neste caso é o mesmo endpoint (Sample_First). O número de tentativas inicia
com a configuração _retriesBeforeSuspension_ e será reduzida a cada mensagem
que falhar, até chegar ao zero. É importante notar que a configuração da
contagem de tentativas não é por mensagem, mas sim por endpoint.

Nesta configuração nós assumimos que os erros são raros e quando acontecem,
basta tentar novamente. Mas se ocorrem frequentemente e continuamente é
necessário atenção imediata para que voltem para a situação normal.

### <a name="ManipulandoErrosEndpoint_Conclusao"></a>Conclusão

A manipulação de erros é crucial para a publicação de endpoints. Os erros
devem ser descobertos nos testes, é recomendado executar muitos testes de
carga e melhorar a performance das configurações do endpoint preparando-o para
os variados erros que podem ocorrer.

### <a name="ManipulandoErrosEndpoint_ApendiceA"></a>Apêndice A

<table>
  <thead>
    <tr>
      <th>Código</th>
      <th>Descrição</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>101000</td>
      <td>Receiver IO error sending</td>
    </tr>
    <tr>
      <td>101001</td>
      <td>Receiver IO error receiving</td>
    </tr>
    <tr>
      <td>101500</td>
      <td>Sender IO error sending</td>
    </tr>
    <tr>
      <td>101501</td>
      <td>Sender IO error receiving</td>
    </tr>
    <tr>
      <td>101503</td>
      <td>Connection failed</td>
    </tr>
    <tr>
      <td>101504</td>
      <td>Connection timed out</td>
    </tr>
    <tr>
      <td>101505</td>
      <td>Connection closed</td>
    </tr>
    <tr>
      <td>101506</td>
      <td>HTTP protocol violation</td>
    </tr>
    <tr>
      <td>101507</td>
      <td>Connect cancel</td>
    </tr>
    <tr>
      <td>101508</td>
      <td>Connect timeout</td>
    </tr>
    <tr>
      <td>101509</td>
      <td>Send abort</td>
    </tr>
  </tbody>
</table>


### Autor

Supun Kamburugamuva, Software Engineer, WSO2, supun@wso2.com
