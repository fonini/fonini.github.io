---
title: As 7 expressões regulares que devemos conhecer
date: 2010-02-02T10:23:16+00:00
author: fonini
layout: post
permalink: /2010/02/02/as-7-expressoes-regulares-que-devemos-conhecer/
categories:
  - Regex
  - Sem categoria
tags:
  - Expressão Regular
  - Regex
---
Hoje vou mostrar algumas expressões regulares que podem ser muito úteis. Pra quem não conhece, recomendo a leitura do Guia de Expressões Regulares Online ([http://guia-er.sourceforge.net](http://guia-er.sourceforge.net/)). Os exemplos estão em PHP, mas podem ser facilmente adaptados para qualquer linguagem que suporte regex.

**Números de telefone**

{% highlight php %}<?php
$telefone = "(54) 9613-4396";

if (preg_match('/^((?[0-9]{2})?|[-. ]?)[ ][0-9]{4}[-. ]?[0-9]{4}$/', $telefone)) {	  
	echo "Telefone válido";
}
{% endhighlight %}

**CEP** 

{% highlight php %}<?php
$cep = "99150-000";
  
if (preg_match('/^[0-9]{5,5}([- ]?[0-9]{4})?$/', $cep)) {
	echo "CEP válido";
}
{% endhighlight %} 

**Comentários em várias linhas** 

{% highlight php %}<?php
$comentario = "/*comentario bla bla bla*/";

if (preg_match('/^[(/*)+.+(*/)]$/', $comentario)) {	  
	echo "Comentário válido";
}
{% endhighlight %}


**Datas (padrão brasileiro)** 

{% highlight php %}<?php  
$data = "12/04/1990";

if (preg_match('/^d{1,2}/d{1,2}/d{4}$/', $data)) {	  
	echo "Data válida";
}  
{% endhighlight %}

**Cores hexadecimais** 

{% highlight php %}<?php
$cor = "#666666";

if (preg_match('/^#(?:(?:[a-fd]{3}){1,2})$/i', $cor)) {  
	echo "Cor válida";
}
{% endhighlight %} 

**Endereços IP** 

{% highlight php %}<?php
$ip = "255.255.255.0";

if (preg_match('^(?:25[0-5]|2[0-4]d|1dd|[1-9]d|d)(?:[.](?:25[0-5]|2[0-4]d|1dd|[1-9]d|d)){3}$', $ip)) {	  
	echo "IP válido";
}
{% endhighlight %} 

**E-mails** 

{% highlight php %}<?php  
$email = "contato@email.net";

if (preg_match('/^[^0-9][a-zA-Z0-9_]+([.][a-zA-Z0-9_]+)*[@][a-zA-Z0-9_]+([.][a-zA-Z0-9_]+)*[.][a-zA-Z]{2,4}$/', $email)) {
	echo "E-mail válido";
}
{% endhighlight %}