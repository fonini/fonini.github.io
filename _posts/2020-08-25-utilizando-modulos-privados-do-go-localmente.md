---
title: "Utilizando módulos privados do Go localmente"
date: 2020-08-25 16:37:46 -0300
layout: post
author: fonini
permalink: /2020/08/25/utilizando-modulos-privados-do-go-localmente/
tags: 
  - go
  - git
---

Colocar no .bashrc ou .bash_profile a seguinte variável:

{% highlight shell %}
export GOPRIVATE="gitlab.com/seu_grupo_privado"
{% endhighlight %}