---
author: Leonardo Saraiva
date: '2010-04-20 21:47:45'
layout: post
slug: instalando-o-wso2-web-services-framework-for-php-2-0-0
comments: true
status: publish
title: Instalando o WSO2 Web Services Framework for PHP (2.0.0)
categories:
- desenvolvimento
tags:
- c
- cmm
- dll
- framework
- libxml2
- linux
- nusoap
- openssl
- pecl
- php
- soap
- ubuntu
- web services
- windows
- wsf
- wso2
---

![](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wsf-php.gif)Como eu disse anteriormente, em [Consumindo um serviço seguro utilizando PHP](http://www.mcorp.com.br/2010/03/consumindo-um-servico-seguro-utilizando-php/), vou mostrar uma das maneiras para instalar o framework que o pessoal do
WSO2 disponibiliza para criação e consumo de serviços em PHP, conhecido como:
[WSO2 Web Services Framework _for PHP_](http://wso2.org/downloads/wsf/php).

Na página de [downloads do WSO2 Web Services Framework _for PHP_](http://wso2.org/downloads/wsf/php), é possível escolher entre 3 opções
de instalação, então exemplificar a fundo apenas uma e colocar uma breve
descrição das outras.

## Binary Distribution

É o framework já compilado e com a DLL dentro que serve para as pessoas que a
utilizarão em ambientes Windows, não terá muito trabalho, apenas colocar a DLL
na pasta correta e configurar o seu _php.ini_. Essa é a opção mais prática -
na minha opinião - para Windows (deixarei essa para uma próxima, não tenho
ambiente para isso - ainda).

## PECL Distribution

Em teoria é a mais fácil de todas. Mas por que "em teoria"? Passei dois dias
realizando diversas configurações na minha máquina para que isso funcionasse
corretamente, perguntei no [fórum](http://wso2.org/forum/thread/9553) se
alguém poderia me ajudar a solucionar, mas desisti. Parti para a maneira
"clássica", o famoso [CMM](/glossario/#CMM), que descrevo abaixo.

## Source Distribution

Essa versão é o [código-fonte do WSO2 Web Services Framework _for
PHP_](https://wso2.org/repos/wso2/trunk/wsf/php/) (aberto, hein!) e aqui temos
duas opções de download, com apenas uma diferença mínima: o compactador. Uma
foi compactada utilizando ZIP e outra TAR/GZ. E ambas será necessário
compilação, com os bons e velhos comandos: _./configure_, _make && make
install_.

Mas, chega de papo, vamos por a mão na "massa".

### Instalando as dependências

As dependências para funcionamento do framework, não são muitas:

  * [WSO2 Web Services Framework _for C_](http://wso2.org/downloads/wsf/c)
  * PHP 5.1.1 ou superior
  * Bibliotecas libxml2 e OpenSSL

### WSO2 Web Services Framework _for C_

Para quem tá acostumado, são os velhos conhecidos, bastando baixar a última
versão (no meu caso a 2.0.0):

    wget http://dist.wso2.org/products/wsf/c/2.0.0/wso2-wsf-c-src-2.0.0.tar.gz
    tar xfvz wso2-wsf-c-src-2.0.0.tar.gz
    cd wso2-wsf-c-src-2.0.0
    ./configure
    make
    sudo make install

### PHP 5.1.1 ou superior

Não vou entrar nos méritos de instalação do PHP, pois imagino que isso esteja
mais do que documentado na internet por aí a fora (para os preguiçosos -
google: [instalação do php no ubuntu](http://www.google.com.br/#hl=pt-BR&source=hp&q=instala%C3%A7%C3%A3o+do+php+no+ubuntu&btnG=Pesquisa+Google&meta=&aq=f&aqi=&aql=&oq=instala%C3%A7%C3%A3o+do+php+no+ubuntu&gs_rfai=&fp=fbe0f18c81cbb156)).

### Bibliotecas libxml2 e OpenSSL

O comando para instalar as dependências é:

    sudo apt-get install libxml2 openssl

E com todas as dependências já instaladas e funcionando, podemos utilizar um
_phpinfo()_; para conferir:

[![](http://assets.mcorp.com.br/wp-content/uploads/2010/04/config-php-libxml2-openssl-300x187.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/04/config-php-libxml2-openssl.png)


### Compilação do WSF/PHP

#### CMM

E agora, a instalação propriamente dita, utilizando novamente os pacotes da
versão 2.0.0:

    wget http://dist.wso2.org/products/wsf/php/2.0.0/wso2-wsf-php-src-2.0.0.tar.gz
    ./configure
    make
    sudo make install

#### 1, 2, 3, testando...

Estamos quase chegando lá...

Vamos copiar dois arquivos do diretório _samples_ (um cliente e um servidor)
para o diretório do servidor web (no meu caso: _/var/www/samples_) e ver se
tudo funcionou:

    sudo mkdir -p /var/www/samples/
    sudo cp samples/math_* /var/www/samples/.

Indo ao navegador, basta abrir o endereço [http://localhost/samples/math_client.php](http://localhost/samples/math_client.php) e conferir tudo funcionando:

[![](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wsf-php-sample-math-300x176.png)](http://assets.mcorp.com.br/wp-content/uploads/2010/04/wsf-php-sample-math.png)


### Conclusão

Ainda não consigo avaliar até onde é válido ou interessante utilizar esse
framework, não pesquisei a fundo ainda o funcionamento e as vantagens dele
sobre as implementações como [SOAP](http://www.php.net/soap) (nativa do PHP)
[NuSOAP](http://nusoap.sourceforge.net/).

Mas o fato de ser uma instalação que não pode ser feita em "qualquer"
servidor, ainda mais no Brasil onde as empresas de hospedagens normalmente não
instalam extensões de terceiros e o preço para ter um servidor próprio não é
tão acessível, pode acabar ficando inviável.

Realizarei testes mais profundos para verificar as verdadeiras vantagens dessa
abordagem na implementação dos serviços, só que - novamente - ficará para um
outro post.

