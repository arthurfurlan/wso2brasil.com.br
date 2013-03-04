---
author: Leonardo Saraiva
date: '2009-12-22 10:43:15'
layout: post
slug: instalando-wso2-enterprise-service-bus-eclipse-tools-no-ubuntu-karmic-koala-9-10
comments: true
status: publish
title: Instalando WSO2 Enterprise Service Bus Eclipse Tools no Ubuntu Karmic Koala (9.10)
categories:
- desenvolvimento
tags:
- '9.10'
- debian
- eclipse
- esb
- karmic koala
- libstdc
- libstdc++5
- libstdc++6
- mozilla
- plugin
- ubuntu
- wso2
- wtp
---

Com o lançamento do [WSO2 Enterprise Service Bus Eclipse Tools](http://wso2.org/projects/tools/esb/esb-authoring) (v1.0.0-beta),
cansado de ficar utilizando a interface web para gerenciar os "esqueminhas" da
ESB, resolvei testar o plugin.

Mas como nem tudo são flores, após eu [instalar o plugin](http://wso2.org/project/tools/esb/esb-authoring/1.0.0/docs/install_guide.html) e tentar criar um novo _endpoint_,
recebi o erro abaixo:

    Unhandled event loop exception XPCOM error -2147467259

[![](http://assets.mcorp.com.br/wp-content/uploads/2009/12/wso2-plugin-esb-eclipse-error-300x184.png)](http://assets.mcorp.com.br/wp-content/uploads/2009/12/wso2-plugin-esb-eclipse-error.png)

Com isso, passei um certo tempo procurando na internet, até descobrir que o
erro é causado por falta da biblioteca **libstdc++5**, que no Ubuntu Karmic
Koala (9.10) foi atualizada para **libstdc++6**. Versão que é incompátivel com
a visualização embarcada do Mozilla que o [Eclipse WTP](http://www.eclipse.org/webtools/) utiliza.

Então, para resolver o problema, primeiro passo que tentei foi:

    $ sudo apt-get install libstdc++5
    Reading package lists... Done
    Building dependency tree
    Reading state information... Done
    Package libstdc++5 is not available, but is referred to by another package.
    This may mean that the package is missing, has been obsoleted, or
    is only available from another source
    E: Package libstdc++5 has no installation candidate

Só que não resolveu, a maneira que encontrei foi procurar a biblioteca para
download, encontrei no site do Debian:

    wget http://ftp.br.debian.org/debian/pool/main/g/gcc-3.3/libstdc++5_3.3.6-18_i386.deb

E instalei:

    sudo dpkg -i libstdc++5_3.3.6-18_i386.deb

E com esses passos, tudo funciona normalmente...

[![](http://assets.mcorp.com.br/wp-content/uploads/2009/12/wso2-plugin-esb-eclipse-running-300x222.png)](http://assets.mcorp.com.br/wp-content/uploads/2009/12/wso2-plugin-esb-eclipse-running.png)
