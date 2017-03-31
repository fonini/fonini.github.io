---
title: Wikipédia no terminal do Linux
date: 2010-04-29T10:32:37+00:00
author: fonini
layout: post
permalink: /2010/04/29/wikipedia-no-terminal-do-linux/
categories:
  - Linux
  - Sem categoria
tags:
  - Terminal
---
Tem louco pra tudo. É possível ver trechos de artigos da Wikipedia através de um lookup DNS em um servidor criado por <a href="https://dgl.cx/" rel="externo nofollow">David Leadbeater</a>. Por exemplo, para ler um trecho do artigo sobre Linux, digite o comando abaixo no terminal:

{% highlight shell %}dig +short txt Linux.wp.dg.cx{% endhighlight %}

Se você não tiver o dig pode fazer a consulta através do host:

{% highlight shell %}host -t txt Linux.wp.dg.cx{% endhighlight %}

Claro que isso não possui muita utilidade, pois somente são retornados 430 bytes. Outro problema é que, para consultas como por exemplo Power Metal, você deve inserir um underline entre as palavras, como é feito na Wikipédia.

Você também pode fazer um alias através do seguinte comando:

{% highlight shell %}wiki() { dig +short txt $1.wp.dg.cx; }{% endhighlight %}

E procurar da seguinte maneira:

{% highlight shell %}wiki Power_metal{% endhighlight %}

Abraço e até a próxima!