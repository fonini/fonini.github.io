---
id: 433
title: Convertendo varchar para time without time zone no PostgreSQL
date: 2012-03-26T14:56:51+00:00
author: fonini
layout: post
guid: http://www.fonini.net/blog/?p=433
permalink: /2012/03/26/convertendo-varchar-para-time-without-time-zone-no-postgresql/
categories:
  - Geral
  - Sem categoria
tags:
  - PostgreSQL
---
Dica rápida pra quem está precisando converter um valor em varchar para time without time zone no PostgreSQL. 

Usando a função to_timestamp(valor, formato), o valor retornado é um **timestamp with time zone**. 

Porém, basta adicionar ao final da chamada da função o tipo do retorno desejado:

{% highlight sql %}
  
to_timestamp('23:59:59', 'HH24:MI:SS')::time without time zone
  
{% endhighlight %}

Tive um problema com PHP, usando PDO com PostgreSQL e a função overlaps(). Precisava passar um valor time para a função e funcionou dessa maneira. 

Espero ajudar alguém.