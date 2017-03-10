---
id: 23
title: Problema do ícone de atualizações no Ubuntu 9.10
date: 2010-02-02T09:18:23+00:00
author: fonini
layout: post
permalink: /2010/02/02/problema-do-icone-de-atualizacoes-no-ubuntu-9-10/
categories:
  - Linux
  - Sem categoria
tags:
  - Linux
  - Ubuntu
---
Notei há um tempo atrás que o ícone que avisa quando existem atualizações disponíveis para o Ubuntu nunca mais tinha dado as caras na minha máquina. Após uma rápida procura na internet encontrei a solução para o problema. Digite os comando abaixo no terminal:

{% highlight bash %}gconftool -s --type bool /apps/update-notifier/auto_launch false
killall update-notifier
update-notifier &
disown
{% endhighlight %}

Pronto. Agora o sistema irá avisar novamente quando houverem atualizações disponíveis.