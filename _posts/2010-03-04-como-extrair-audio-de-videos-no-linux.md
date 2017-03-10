---
id: 73
title: Como extrair áudio de vídeos no Linux
date: 2010-03-04T09:55:41+00:00
author: fonini
layout: post
permalink: /2010/03/04/como-extrair-audio-de-videos-no-linux/
categories:
  - Linux
  - Sem categoria
tags:
  - Linux
---
Eu estava assistindo um clipe resolvi extrair o áudio.

Tentei num site que prometia extrair áudio de vídeos do YouTube, mas a qualidade é horrenda.

A solução foi no bom e velho terminal, com o mplayer. Se você não tiver o mplayer instalado, faça-o com o seguinte comando:

{% highlight shell %}sudo apt-get install mplayer{% endhighlight %}

Em seguida, vá até a pasta onde está o vídeo e execute um dos seguintes comandos:

{% highlight shell %}mplayer -dumpaudio video.avi -dumpfile audio.mp3{% endhighlight %}

ou

{% highlight shell %}mplayer -vo null -hardframedrop -ao pcm:file=audio.wav video.mp4{% endhighlight %}

No primeiro caso a extração é extremamente rápida, quase instantânea, mas pelo menos aqui o áudio extraído de um arquivo .mp4 ficou corrompido. No segundo caso demorou, mas funcionou. Porém, o arquivo resultante ficou com 60 MB, necessitando mais uma conversão para MP3 :S

Grande abraço e até a próxima!