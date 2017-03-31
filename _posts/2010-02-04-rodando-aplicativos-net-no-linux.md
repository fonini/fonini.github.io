---
title: Rodando aplicativos .NET no Linux
date: 2010-02-04T14:50:31+00:00
author: fonini
layout: post
permalink: /2010/02/04/rodando-aplicativos-net-no-linux/
categories:
  - Linux
  - Sem categoria
tags:
  - Linux
  - Ubuntu
---
Hoje precisei fazer algo que não me agrada muito: rodar um software via Wine (Wine Is Not an Emulator). Tratava-se de um software para Windows, mas dá muita preguiça reiniciar a máquina para entrar no Windows (faz meses que não faço isso, somente tenho Windows para rodar o Digital Drums, um software que simula uma bateria musical).

Executei o dito cujo do programa, mas percebi que era necessário o Microsoft .NET Framework 2.0 para o mesmo funcionar. Putz! E agora? Meio a contragosto de instalar tanta porcaria no meu Linux, me obriguei a instalar o .NET.

Siga com atenção os passos abaixo. É necessário ter o Wine instalado na máquina.

Antes de mais nada, faça backup do arquivo system.reg, que se encontra na pasta /home/usuario/.wine/. É importante fazer backup desse arquivo, pois caso a instalação falhe (como aconteceu comigo, por falta de espaço na partição) você precisará remover todas as entradas que contenham a palavra .NET para conseguir instalar o framework (e se arrependerá de ter nascido caso isso aconteça).

Feito isso, digite os comandos abaixo no terminal:

{% highlight shell %}wget http://www.kegel.com/wine/winetricks
sh winetricks corefonts vcrun6
sh winetricks dotnet20{% endhighlight %}

Se tudo correr bem, aparecerá o instalador do .NET, ai é só prosseguir com a instalação em modo gráfico e finalizar o processo.

Abraços e até a próxima!