---
title: "Baixando MP3 em alta qualidade do YouTube"
date: 2019-03-27 16:38:53 -0300
layout: post
author: fonini
permalink: /2019/03/27/baixando-mp3-em-alta-qualidade-do-youtube/
tags: 
  - tools
---

Baixe o youtube-dl em [youtube-dl.org](https://youtube-dl.org).
O áudio será baixado com o cover do vídeo e os metadados.

{% highlight shell %}
youtube-dl.exe -f 251 --extract-audio --audio-format mp3 --audio-quality 320k --add-metadata LINK_DO_VIDEO
{% endhighlight %}
