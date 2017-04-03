---
title: Como remover a voz das músicas no Linux
date: 2010-02-08T13:32:06+00:00
author: fonini
layout: post
permalink: /2010/02/08/como-remover-a-voz-das-musicas-no-linux/
tags:
  - Linux
  - Ubuntu
---
Fui a procura de um software para Linux capaz de remover a voz da música em tempo de execução. Uma das únicas opções que encontrei foi o software [xmms](http://xxms.org), clone do Winamp para a plataforma Linux. Esse software possui um plugin chamado Removedor de Voz que "tenta" remover a voz da música. Depende muito da música. Um dos melhores exemplos que eu encontrei foi Primeiros Erros do Capital Inicial, onde realmente remove a voz sem maiores perdas no restante do áudio.

Abaixo, o processo de instalação do xmms no Ubuntu 9.10:

Adicione a seguinte entrada em seu arquivo sources.list (ou no menu Sistema/Administração/Canais de Software):

{% highlight shell %}deb http://www.pvv.ntnu.no/~knuta/xmms/karmic ./{% endhighlight %}

Feito isso, digite no terminal:

{% highlight shell %}sudo apt-get install xmms{% endhighlight %}

Para executar o programa, novamente no terminal:

{% highlight shell %}xmms{% endhighlight %}

Habilite o plugin Removedor de Voz no menu Opções/Preferências/Plugins de Efeitose clique em Ativar Plugin. As músicas já serão tocadas sem a voz.

Obs: Foi meio chato aqui pra executar esse programa. Tive que fechar todos os programas que fizessem uso da placa de som.
  
Se você usa outras versões do Ubuntu, use os repositórios disponíveis <a href="http://www.pvv.ntnu.no/~knuta/xmms/" rel="externo">aqui</a>.

Abraços e até a próxima