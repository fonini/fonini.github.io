---
title: "Atualizar biblioteca do Kodi via terminal"
date: 2017-04-17 08:33:31 -0300
layout: post
author: fonini
permalink: /2017/04/17/atualizar-biblioteca-do-kodi-via-terminal/
tags: 
  - Linux
  - Kodi
---

O comando abaixo é usado para atualizar a biblioteca do Kodi com novos filmes. Primeiro, é necessário [habilitar o web server do Kodi](http://kodi.wiki/view/Webserver#Enabling_the_webserver){:target="_blank"}, caso ainda não esteja habilitado.

{% highlight shell %}
curl -H "Content-Type:application/json" -X POST -d '{"jsonrpc": "2.0", "id": "scan", "method": "VideoLibrary.Scan", "params": {"directory":"/media/MEU-HD/Filmes/"}}' "http://10.0.0.107:8080/jsonrpc"
{% endhighlight %}

Veja outros métodos na [documentação oficial](http://kodi.wiki/view/JSON-RPC_API){:target="_blank"}.