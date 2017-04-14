---
title: "Baixar todos os vídeos e imagens de uma página da internet no Linux"
date: 2017-04-14 15:45:00 -0300
layout: post
author: fonini
permalink: /2017/04/14/linux-baixar-todos-os-videos-e-imagens-de-uma-pagina-da-internet/
tags:
  - Linux
  - Shell
---

Adicione ou retire as extensões dos arquivos conforme desejar.
O parâmetro -R especifica arquivos que devem ser ignorados.

{% highlight shell %}
wget -A jpg,jpeg,mp4,webm,png,gif -R video.png,video -r -l 1 -nc -e robots=off url_da_pagina
{% endhighlight %}