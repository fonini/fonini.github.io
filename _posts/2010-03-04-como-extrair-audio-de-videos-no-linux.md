---
id: 73
title: Como extrair áudio de vídeos no Linux
date: 2010-03-04T09:55:41+00:00
author: fonini
layout: post
guid: http://www.fonini.net/blog/?p=73
permalink: /2010/03/04/como-extrair-audio-de-videos-no-linux/
categories:
  - Linux
  - Sem categoria
tags:
  - Linux
---
Eu estava assistindo um clipe muito foda da banda Holiness, de Erechim/RS, pertinho daqui e resolvi extrair o áudio do clipe para ouvir enquanto o CD não aparece por aqui. A propósito, recomendo a banda a todos que gostam de um bom metal com vocais femininos ?

Tentei num site que prometia extrair áudio de vídeos do YouTube, mas a qualidade é horrenda.

A solução foi no bom e velho terminal, com o mplayer. Se você não tiver o mplayer instalado, faça-o com o seguinte comando:</p> 

<pre id="terminal" user="fonini" computer="valhalla">sudo apt-get install mplayer</pre></p> 

Em seguida, vá até a pasta onde está o vídeo e execute um dos seguintes comandos:</p> 

<pre id="terminal" user="fonini" computer="valhalla">mplayer -dumpaudio video.avi -dumpfile audio.mp3</pre></p> 

ou</p> 

<pre id="terminal" user="fonini" computer="valhalla">mplayer -vo null -hardframedrop -ao pcm:file=audio.wav video.mp4</pre></p> 

No primeiro caso a extração é extremamente rápida, quase instantânea, mas pelo menos aqui o áudio extraído de um arquivo .mp4 ficou corrompido. No segundo caso demorou, mas funcionou. Porém, o arquivo resultante ficou com 60 MB, necessitando mais uma conversão para MP3 :S

Grande abraço e até a próxima!</p>