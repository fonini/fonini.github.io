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
<\[iI\]\[mM\]\[gG\]\[a-zA-Z0-9s=".\]\*((src)=s\*(?:"(\[^"]\*)"|'[^']\*'))[a-zA-Z0-9s=".]\*/\*>(?:</[iI\]\[mM\][gG]>)*
{% endhighlight %}
  
[Testar](http://regexpal.com/?flags=&regex=%3C[iI][mM][gG][a-zA-Z0-9s%3D%22.]*%28%28src%29%3Ds*%28%3F%3A%22%28[^%22]*%29%22|%27[^%27]*%27%29%29[a-zA-Z0-9s%3D%22.]*%2F*%3E%28%3F%3A%3C%2F[iI][mM][gG]%3E%29*&input=%3Cimg%20src%3D%22teste.jpg%22%20%2F%3E) 



**Encontra tudo que está entre as tags especificadas. Mais tags podem ser adicionadas**
{% highlight regex %}
<(script|style)[^>]\*?>(?:.|n)\*?</s\*1s\*>
{% endhighlight %}
[Testar](http://regexpal.com/?flags=&regex=%3C%28script|style%29[^%3E]*%3F%3E%28%3F%3A.|n%29*%3F%3C%2Fs*1s*%3E&input=%3Chtml%3E%0A%3Cscript%3E%0Aalert%28%27bla%27%29%3B%0A%3C%2Fscript%3E%0A%3C%2Fhtml%3E) 



**Útil para remover tags HTML**
{% highlight regex %}
<[^>]*>
{% endhighlight %}
  
[Testar](http://regexpal.com/?flags=&regex=%3C[^%3E]*%3E&input=%3Cp%3ETexto%3C%2Fp%3E) 



**Encontra extensões de arquivos**
{% highlight regex %}
.([A-Za-z0-9]{2,5}($|b?))
{% endhighlight %}
  
[Testar](http://regexpal.com/?flags=m&regex=.%28[A-Za-z0-9]{2%2C5}%28%24|b%3F%29%29&input=Baixe%20o%20arquivo%20teste.zip)

Se alguém tiver sugestões para mais expressões regulares, comente ou entre em contato.

Abraço e até a próxima!