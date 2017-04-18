---
title: Expressões regulares para trabalhar com HTML
date: 2010-02-09T10:37:20+00:00
author: fonini
layout: post
permalink: /2010/02/09/expressoes-regulares-para-trabalhar-com-html/
tags:
  - Expressão Regular
  - Regex
---
Reuni algumas expressões regulares úteis para trabalhar com HTML.

**Encontra comentários HTML**
{% highlight regex %}
/<!--(.*?)-->/
{% endhighlight %}
  
[Testar](https://regex101.com/r/y0kBAz/1) 



**Captura o atributo href de links**
{% highlight regex %}
/href="([^\'\"]+)/g
{% endhighlight %}
  
[Testar](https://regex101.com/r/MQttC7/1/) 



**Encontra todos os atributos de uma tag. Ex: src, name, value.**
{% highlight regex %}
/(?:[\w]*) *= *"(?:(?:(?:(?:(?:\\\W)*\\\W)*[^"]*)\\\W)*[^"]*")/gim
{% endhighlight %}
  
[Testar](https://regex101.com/r/WLBAqV/1) 



**Encontra tags <h1> até <h6>**
{% highlight regex %}
<h([1-6])>([^<]*)<\/h([1-6])>
{% endhighlight %}
  
[Testar](https://regex101.com/r/hzXKOm/1/) 



**Encontra tags &lt;a&gt; válidas**
{% highlight regex %}
<a[^>]*([^"]*)[^>]*>([ 0-9a-zA-Z]+)<\/a>
{% endhighlight %}
  
[Testar](https://regex101.com/r/LxDpGQ/1) 



**Encontra todas as URLs de um texto**
{% highlight regex %}
(http:\/\/|https:\/\/)([a-zA-Z0-9]+.[a-zA-Z0-9-]+|[a-zA-Z0-9-]+).[a-zA-Z.]{2,6}(\/[a-zA-Z0-9.?=\/#%&+-]+|\/|)
{% endhighlight %}
  
[Testar](https://regex101.com/r/DH8zYx/1) 



**Encontra todas as imagens**
{% highlight regex %}
<img([\w\W]+?)\/?>
{% endhighlight %}
  
[Testar](https://regex101.com/r/8Mw5F0/1)

**Útil para remover tags HTML**
{% highlight regex %}
<[^>]*>
{% endhighlight %}
  
[Testar](https://regex101.com/r/FQWTEW/1)