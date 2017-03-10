---
id: 35
title: Como remover a voz das músicas no Linux
date: 2010-02-08T13:32:06+00:00
author: fonini
layout: post
guid: http://www.fonini.net/blog/?p=35
permalink: /2010/02/08/como-remover-a-voz-das-musicas-no-linux/
categories:
  - Linux
  - Sem categoria
tags:
  - Linux
  - Ubuntu
---
Um dia desses eu estava assistindo o <a href="http://vimeo.com/8777801" rel="externo">vídeo em Tributo ao Jimmy &#8220;The Rev&#8221; Sullivan</a>, fantástico (ex) baterista da banda Avenged Sevenfold, quando me deparei com um trecho de uma música que eu nunca tinha ouvido antes. Procurei em todas as músicas que eu tenho e nada. Finalmente reparei que o trecho do vídeo é estranho pois na música original tem voz naquela parte e no vídeo não tinha.

Então fui a procura de um software para Linux capaz de remover a voz da música em tempo de execução. Uma das únicas opções que encontrei foi o software [xmms](http://xxms.org), clone do Winamp para a plataforma Linux. Esse software possui um plugin chamado Removedor de Voz que &#8220;tenta&#8221; remover a voz da música. Depende muito da música, a música do Avenged Sevenfold (Sidewinder) que eu queria até removeu a voz, mas a bateria foi junto. Um dos melhores exemplos que eu encontrei foi Primeiros Erros do Capital Inicial, onde realmente remove a voz sem maiores perdas no restante do áudio.

Abaixo, o processo de instalação do xmms no Ubuntu 9.10:

Adicione a seguinte entrada em seu arquivo sources.list (ou no menu Sistema/Administração/Canais de Software):

<pre>deb http://www.pvv.ntnu.no/~knuta/xmms/karmic ./</pre>

Feito isso, digite no terminal:

<pre id="terminal" user="fonini" computer="valhalla">sudo apt-get install xmms</pre>

Para executar o programa, novamente no terminal:

<pre id="terminal" user="fonini" computer="valhalla">xmms</pre>

Habilite o plugin Removedor de Voz no menu Opções/Preferências/Plugins de Efeitose clique em Ativar Plugin. As músicas já serão tocadas sem a voz.

Obs: Foi meio chato aqui pra executar esse programa. Tive que fechar todos os programas que fizessem uso da placa de som.
  
Se você usa outras versões do Ubuntu, use os repositórios disponíveis <a href="http://www.pvv.ntnu.no/~knuta/xmms/" rel="externo">aqui</a>.

Abraços e até a próxima