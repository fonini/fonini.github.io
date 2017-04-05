---
title: Descobrindo subdomínios com Nmap
date: 2017-04-05T09:40:00+00:00
author: fonini
layout: post
permalink: /2017/04/05/descobrir-subdominios-nmap
tags:
  - Linux
  - Nmap
---

Esta dica serve para você (tentar) descobrir todos os subdomínios que pertencem a um domínio.

{% highlight shell %}
nmap -script dns-brute -v -sn twitter.com
{% endhighlight %}