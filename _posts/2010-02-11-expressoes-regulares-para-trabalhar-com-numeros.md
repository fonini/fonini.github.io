---
title: Expressões regulares para trabalhar com números
date: 2010-02-11T13:33:25+00:00
author: fonini
layout: post
permalink: /2010/02/11/expressoes-regulares-para-trabalhar-com-numeros/
tags:
  - Expressão Regular
  - Regex
---
Continuando a série sobre expressões regulares iniciada [aqui](/2010/02/09/expressoes-regulares-para-trabalhar-com-html/), reuni algumas expressões regulares úteis para trabalhar com números. 

**Encontra números inteiros, incluindo negativos**
{% highlight regex %}
^[-+]?\d*$
{% endhighlight %}
  
[Testar](https://regex101.com/r/xuU4g7/1)

**Encontra números inteiros e de ponto flutuante (float, double), incluindo negativos** 
{% highlight regex %}
^[-+]?\d*.?\d*$
{% endhighlight %}
  
[Testar](https://regex101.com/r/M2eNjY/1)

**Encontra qualquer número real** 
{% highlight regex %}
^[-+]?\d+(.\d+)?$
{% endhighlight %}
  
[Testar](https://regex101.com/r/Exvj3m/1)

**Encontra representações de dinheiro em dólar** 
{% highlight regex %}
^\$(\d{1,3}(,\d{3})*|(\d+))(.\d{2})?$
{% endhighlight %}
  
[Testar](https://regex101.com/r/puNaar/1)

**Encontra representações de dinheiro em reais** 
{% highlight regex %}
^R\$ ?([1-9]{1}[\d]{0,2}(.[\d]{3})*(,[\d]{0,2})?|[1-9]{1}[\d]{0,}(,[\d]{0,2})?|0(,[\d]{0,2})?|(,[\d]{1,2})?)$
{% endhighlight %}
  
[Testar](https://regex101.com/r/68kVEp/1)

**Encontra inteiros positivos**
{% highlight regex %}
^\d+$
{% endhighlight %}
  
[Testar](https://regex101.com/r/9kvUSQ/1)

**Encontra porcentagens, positivas ou negativas, com 2 casas decimais** 
{% highlight regex %}
^-?[0-9]{0,2}(.[0-9]{1,2})?$|^-?(100)(.[0]{1,2})?$
{% endhighlight %}
  
[Testar](http://regexpal.com/?flags=&#038;regex=^-%3F[0-9]{0%2C2}%28.[0-9]{1%2C2}%29%3F%24|^-%3F%28100%29%28.[0]{1%2C2}%29%3F%24&#038;input=67.43)

**Encontra inteiros entre 0 ou 000 até 255** 
{% highlight regex %}
^(\[01]?[0-9]?[0-9]|2[0-4\]\[0-9\]|25[0-5])$
{% endhighlight %}
  
[Testar](http://regexpal.com/?flags=&#038;regex=^%28[01]%3F[0-9]%3F[0-9]|2[0-4][0-9]|25[0-5]%29%24&#038;input=255)

**Encontra inteiros entre 0 ou 000 até 127** 
{% highlight regex %}
^(0?\[0-9]?[0-9]|1[0-1\]\[0-9\]|12[0-7])$
{% endhighlight %}
  
[Testar](http://regexpal.com/?flags=&#038;regex=^%280%3F[0-9]%3F[0-9]|1[0-1][0-9]|12[0-7]%29%24&#038;input=50)

**Encontra inteiros entre 0 e 999** 
{% highlight regex %}
^(\[0-9]|[1-9\]\[0-9\]|\[1-9\]\[0-9\][0-9])$
{% endhighlight %}
  
[Testar](http://regexpal.com/?flags=&#038;regex=^%28[0-9]|[1-9][0-9]|[1-9][0-9][0-9]%29%24&#038;input=666)

**Encontra inteiros entre 1 e 999** 
{% highlight regex %}
^(\[1-9]|[1-9\]\[0-9\]|\[1-9\]\[0-9\][0-9])$
{% endhighlight %}
  
[Testar](http://regexpal.com/?flags=&#038;regex=^%28[1-9]|[1-9][0-9]|[1-9][0-9][0-9]%29%24&#038;input=100)

**Encontra números de cartão de crédito de 13 até 16 dígitos** 
{% highlight regex %}
b(?:d[ -]*?){13,16}b
{% endhighlight %}
  
[Testar](http://regexpal.com/?flags=&#038;regex=b%28%3F%3Ad[%20-]*%3F%29{13%2C16}b&#038;input=0123456789012345) 

Não deixe de entrar em contato caso tenha alguma dúvida ou sugestões para os próximos posts.

Abraço e até a próxima!