---
title: Converter links HTML para Markdown
date: 2017-04-03T16:40:00+00:00
author: fonini
layout: post
permalink: /2017/04/03/converter-links-html-markdown
tags:
  - Linux
  - Markdown
  - Jekyll
  - Wordpress
---

Esta dica foi usada neste blog após uma conversão de Wordpress para Jekyll. O conversor acabou deixando os links no formato HTML.

Rodei o código abaixo na pasta _posts do blog em Jekyll. Faça backup dos seus arquivos antes de executar.

{% highlight shell %}
sed -i -- 's/<a href=["]\([^"]*\)["][^>]*>\([^<]*\)<\/a>/[\2](\1)/igm' *.md
{% endhighlight %}

{% highlight html %}
<!--Exemplo-->

<!--antes-->
<a href="https://github.com/fonini" rel="nofollow">Meu Github</a>

<!--depois-->
[Meu Github](https://github.com/fonini)
{% endhighlight %}