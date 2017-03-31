---
title: Expressões regulares variadas
date: 2010-02-19T09:55:00+00:00
author: fonini
layout: post
permalink: /2010/02/19/expressoes-regulares-variadas/
categories:
  - Regex
  - Sem categoria
tags:
  - Expressão Regular
  - Regex
---
Mais um post da série sobre expressões regulares. Os outros posts de regex podem ser encontrados [aqui](/2010/02/12/expressoes-regulares-para-trabalhar-com-datahora/), [aqui](/2010/02/11/expressoes-regulares-para-trabalhar-com-numeros/) e [aqui](/2010/02/09/expressoes-regulares-para-trabalhar-com-html/).

**Valida número do ISBN (International Standard Book Number)**
{% highlight regex %}
ISBNx20(?=.{13}$)d{1,5}([- ])d{1,7}1d{1,6}1(d|X)$
{% endhighlight %}

<a href="http://regexpal.com/?flags=&regex=ISBNx20%28%3F%3D.{13}%24%29d{1%2C5}%28[-%20]%29d{1%2C7}1d{1%2C6}1%28d|X%29%24&input=ISBN%20972-1-02783-9" rel="externo">Testar</a> 

**Valida formato do CNPJ**
{% highlight regex %}
d{2}.?d{3}.?d{3}/?d{4}-?d{2} 
{% endhighlight %}

<a href="http://regexpal.com/?flags=&regex=d{2}.%3Fd{3}.%3Fd{3}%2F%3Fd{4}-%3Fd{2}&input=89.432.343%2F0001-22" rel="externo">Testar</a>

**Limitar o tamanho de uma string em 50 caracteres  ** 
{% highlight regex %}
^(.|n){0,50}$ 
{% endhighlight %}

<a href="http://regexpal.com/?flags=&regex=^%28.|n%29{0%2C50}%24&input=Bla%20teste%20uahsuhaushua%20regex%20%C3%A9%20legal%20jonnas%20fonini" rel="externo">Testar</a> 

**Valida formato de temperaturas Celsius e Fahrenheit**

{% highlight regex %}
^([+-]?[0-9]+)([CF])$
{% endhighlight %}
  
<a href="http://regexpal.com/?flags=&regex=^%28[%2B-]%3F[0-9]%2B%29%28[CF]%29%24&input=70F" rel="externo">Testar</a>

**Valida nomes de dispositivos no Linux (mude a parte do "eth" para validar outros dispositivos)**
{% highlight regex %}
^(eth[0-9]$)|(^eth[0-9]:[1-9]$)
{% endhighlight %}
  
<a href="http://regexpal.com/?flags=&regex=^%28eth[0-9]%24%29|%28^eth[0-9]%3A[1-9]%24%29&input=eth0" rel="externo">Testar</a>

**Valida nomes de domínios**
{% highlight regex %}
^(a-zA-Z0-9([a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?.)+[a-zA-Z]{2,6}$
{% endhighlight %}
  
<a href="http://regexpal.com/?flags=&regex=^%28[a-zA-Z0-9]%28[a-zA-Z0-9-]{0%2C61}[a-zA-Z0-9]%29%3F.%29%2B[a-zA-Z]{2%2C6}%24&input=fonini.github.io" rel="externo">Testar</a>


**Valida e-mails de TLD's (Top Level Domains) específicos**
{% highlight regex %}
^[A-Z0-9._%+-]+@[A-Z0-9.-]+.(?:|com|org|net|gov|[A-Z]{2})$
{% endhighlight %}
  
<a href="http://regexpal.com/?flags=im&regex=^[A-Z0-9._%25%2B-]%2B%40[A-Z0-9.-]%2B.%28%3F%3A|com|org|net|gov|[A-Z]{2}%29%24&input=contato%email.net%0Ateste%40teste.biz" rel="externo">Testar</a>

**Localiza tags HTML vazias**
{% highlight regex %}
<(A-ZA-Z0-9\*)[^>]\*>s*</1>
{% endhighlight %}
  
<a href="http://regexpal.com/?flags=&regex=%3C%28[a-z][a-z0-9]*%29[^%3E]*%3Es*%3C%2F1%3E&input=%3Cdiv%3E%3Cp%3E%3C%2Fp%3E%3C%2Fdiv%3E" rel="externo">Testar</a>

**Localiza variáveis e valores de arquivos INI** 
{% highlight regex %}
^([^=rn]+)=(.*)
{% endhighlight %}
  
<a href="http://regexpal.com/?flags=m&regex=^%28[^%3Drn]%2B%29%3D%28.*%29&input=valor1%3D20%3B%0Avalor2%3D30%3B" rel="externo">Testar</a>

**Encontra linhas duplicadas**
{% highlight regex %}
^(.*)(r?n1)+$
{% endhighlight %}
  
<a href="http://regexpal.com/?flags=m&regex=^%28.*%29%28r%3Fn1%29%2B%24&input=linha%0Ateste%0Ateste%0A" rel="externo">Testar</a>

**Localiza rótulos de discos do Windows. Ex: C:**
{% highlight regex %}
^([a-z]):
{% endhighlight %}
  
<a href="http://regexpal.com/?flags=m&regex=^%28[a-zA-Z]%29%3A&input=C%3Ateste" rel="externo">Testar</a>