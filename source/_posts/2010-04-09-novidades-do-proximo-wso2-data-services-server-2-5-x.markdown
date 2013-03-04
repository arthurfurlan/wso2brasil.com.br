---
author: Leonardo Saraiva
date: '2010-04-09 13:24:27'
layout: post
slug: novidades-do-proximo-wso2-data-services-server-2-5-x
comments: true
status: publish
title: Novidades do próximo WSO2 Data Services Server (2.5.x)
categories:
- desenvolvimento
tags:
- batch mode
- boxcarring
- data services
- dss
- eventing
- jmx
- lançamento
- wip services
- wsdl
- wso2
- wso2 carbon
---

A versão RC2 do WSO2 Data Services Server 2.5.0 nos mostrou que está com novas
opções e funcionalidades muito úteis, algumas que estavam até fazendo falta.
Claro que a adoção do WSO2 Carbon 3.0, traz várias diferenças nos recursos e
interface em toda a suíte. Mas vamos partir para o que interessa.

  * [Dashboard](#Dashboard)
  * [Carbon Data Sources](#CarbonDataSources)
  * [Array type](#ArrayType)
  * [Default values in input mappings](#DefaultValuesInputMappings)
  * [Data Validation Logic](#DataValidationLogic)
  * [WIP services](#WIPServices)
  * [Contract first](#ContractFirst)
  * [Batch mode](#BatchMode)
  * [Boxcarring](#Boxcarring)
  * [Eventing](#Eventing)
  * [Binary Input/Output data](#BinaryData)
  * [JMX](#JMX)
  * [Query Properties](#QueryProperties)
  * [Conclusão](#Conclusao)

## <a name=""></a>Dashboard

Com a atualização para o WSO2 Carbon 3.0, foi implantando um _Dashboard_ que
pode conter informações variadas. Essas informações podem ser personalizadas
utilizando _gadgets_. Aliás, essa atualização pode ser notada em toda a suíte
que utilizam o novo Carbon.

## <a name=""></a>Carbon Data Sources

[![](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wso2ds-2.5.0-r2-CarbonDataSources-01-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wso2ds-2.5.0-r2-CarbonDataSources-01.png)
[![](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wso2ds-2.5.0-r2-CarbonDataSources-02-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wso2ds-2.5.0-r2-CarbonDataSources-02.png)

Agora ficará muito mais fácil gerenciar conexões às várias base de dados. Com
_Carbon Data Sources_, será possível apontar no [Data Service](/glossario/#DataServices) qual _data source_ utilizar, e cada
ambiente (teste, desenvolvimento, homologação ou produção) terão suas próprias
configurações, bastará manter o mesmo nome.

## <a name=""></a>Array Type

[![](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wso2ds-2.5.0-r2-ArrayType-01-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wso2ds-2.5.0-r2-ArrayType-01.png)
[![](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wso2ds-2.5.0-r2-ArrayType-02-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wso2ds-2.5.0-r2-ArrayType-02.png)

Poderemos ter entradas do tipo _array_ ou _scalar_, onde essas entradas podem
conter valores de diferentes tipos, como: _string_, _integer_, _real_,
_double_, _numeric_, _tinyint_, _smallint_, _bigint_, _date_, _time_,
_timestamp_, _bit_, _oracle ref cursor_ ou _binary_.

## <a name=""></a>Default values in input mappings

[![](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wso2ds-2.5.0-r2-DefaultValuesInputMappings-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wso2ds-2.5.0-r2-DefaultValuesInputMappings.png)

No caso do tipo de entrada _scalar_, poderá ser indicado um valor padrão para
a entrada.

## <a name=""></a>Data Validation Logic

[![](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wso2ds-2.5.0-r2-DataValidationLogic-01-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wso2ds-2.5.0-r2-DataValidationLogic-01.png)
[![](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wso2ds-2.5.0-r2-DataValidationLogic-02-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wso2ds-2.5.0-r2-DataValidationLogic-02.png)

Os dados de entrada poderão ser validados utlizando alguns validadores
padrões:

  * **Long Range**: com mínimo e máximo de opção;
  * **Double Range**: com mínimo e máximo de opção;
  * **Length**: com mínimo e máximo de opção;
  * **Pattern**: com pattern de opção;
  * **Custom**: com a classe de opção.

## <a name=""></a>WIP Services

[![](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wip_dbs-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wip_dbs.png)
[![](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wip_service_list-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wip_service_list.png)

Os serviços que ainda não estão finalizados, estão passando por correção ou
qualquer outro motivo, poderão ser marcados como: "Work in progress". Isso
evitará erros e os clientes não conseguirão consumir o serviço.

## <a name=""></a>Contract first

[![](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wsdl_upload-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wsdl_upload.png)
[![](http://assets.mcorp.com.br/wp-content/uploads/2010/04/dummy_data_source-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/04/dummy_data_source.png)

Com essa funcionalidade, criar _data services_ poderá fica ainda mais simples.
Basta adicionar um contrato (WSDL) com todas as definições e ele criará um
_WIP Service_ para você, sendo necessário apenas você configurar conexões e
preencher as _queries_.

## <a name=""></a>Batch mode

[![](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wso2ds-2.5.0-r2-BatchMode-01-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wso2ds-2.5.0-r2-BatchMode-01.png)
[![](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wso2ds-2.5.0-r2-BatchMode-02-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wso2ds-2.5.0-r2-BatchMode-02.png)

Um recurso bastante interessante implementado é o _Batch Mode_, esse recurso
implementa automaticamente, em todos os métodos que realizam alguma função de
escrita no banco de dados (_INSERT_, _DELETE_ e _UPDATE_), o recurso de
invocar uma única vez o serviço, mas realizando operações em vários objetos de
uma única vez, como - por exemplo - um inserir uma listagem de pessoas.

## <a name=""></a>Boxcarring

[![](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wso2ds-2.5.0-r2-Boxcarring-01-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wso2ds-2.5.0-r2-Boxcarring-01.png)
[![](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wso2ds-2.5.0-r2-Boxcarring-02-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wso2ds-2.5.0-r2-Boxcarring-02.png)

Implementação importante para essa nova versão, _boxcarring_ nada mais é que o
suporte a transações nos serviços, pelas informações coletadas, essa transação
pode ser de dois tipos: _SOAP_ ou _Transport_.

## <a name=""></a>Eventing

Será um recurso que dará a opção de implementarmos eventos em cima de
determinadas operações, funciona basicamente como uma _trigger_ de banco de
dados.

## <a name=""></a>Binary Input/Output Data

Será possível utilizar dados binários (tipo Base64) tanto para enviar, quanto
para receber.

[![](http://assets.mcorp.com.br/wp-content/uploads/2010/04/binary-input-mapping-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/04/binary-input-mapping.png)
[![](http://assets.mcorp.com.br/wp-content/uploads/2010/04/binary-output-mapping-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/04/binary-output-mapping.png)


## <a name=""></a>JMX

O WSO2 Data Services Server proverá informações dos serviços publicados,
utilizando Java Management Extensions (JMX).

## <a name=""></a>Query Properties

[![](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wso2ds-2.5.0-r2-QueryProperties-01-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wso2ds-2.5.0-r2-QueryProperties-01.png)
[![](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wso2ds-2.5.0-r2-QueryProperties-02-150x150.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wso2ds-2.5.0-r2-QueryProperties-02.png)

As _queries_ podem ter algumas propriedades específicas na execução, ajudando
na questão de performance e limitações.

## <a name=""></a>Conclusão

Essas novas versões que estão para sair, da suíte WSO2 Carbon (3.0) e WSO2
Data Services Server (2.5.0), evoluíram bastante comparativamente as suas
sucessoras. E o que é bem importante, não foi necessária nenhuma alteração
para os serviços que rodam na versão 2.2.1 do WSO2 Data Services Server
funcionarem nessa _release_, diferentemente da atualização da versão 2.0.x
para a 2.2.x.

Os tópicos que não documentei ainda, provavelmente consiga documentar nas
próximas _releases_, ou quando achar aonde estão esses recursos, a não ser que
as alterações sejam internas e não fiquem visuais pra nós. Caso queira ajudar
a encontrar e documentar todas as alterações, pode acessar o
[repositório](http://builder.wso2.org/~carbon/releases/carbon/3.0.0/) com os
_builders_ (com gerações quase que diárias).

Minha ideia é também exemplificar como utilizar cada uma delas futuramente,
para que não fique dúvidas de como utilizar esses novos recursos. Então, fique
ligado nas atualizações pelo _feed_.

