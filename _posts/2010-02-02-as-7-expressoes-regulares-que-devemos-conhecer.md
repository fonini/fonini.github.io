---
id: 25
title: As 7 expressões regulares que devemos conhecer
date: 2010-02-02T10:23:16+00:00
author: fonini
layout: post
guid: http://www.fonini.net/blog/?p=25
permalink: /2010/02/02/as-7-expressoes-regulares-que-devemos-conhecer/
categories:
  - Regex
  - Sem categoria
tags:
  - Expressão Regular
  - Regex
---
Hoje vou mostrar algumas expressões regulares que podem ser muito úteis. Pra quem não conhece, recomendo a leitura do Guia de Expressões Regulares Online ([http://guia-er.sourceforge.net](http://guia-er.sourceforge.net/)). Os exemplos estão em PHP, mas podem ser facilmente adaptados para qualquer linguagem que suporte regex.

**<span style="font-size: 14px;">Números de telefone<br /> </span>**</p> 

[php]
  
$telefone = "(54) 9613-4396";
  
if (preg_match(&#8216;/^((?\[0-9]{2})?|[-. ]?)[ \]\[0-9\]{4}[-. ]?[0-9]{4}$/&#8217;, $telefone)) {
	  
echo "Telefone válido";
  
}
  
[/php]

**<span style="font-size: 14px;">CEP<br /> </span>**</p> 

[php]
  
$cep = "99150-000";
  
if (preg_match(&#8216;/^[0-9]{5,5}([- ]?[0-9]{4})?$/&#8217;, $cep)) {
	  
echo "CEP válido";
  
}
  
[/php]</p> 

**<span style="font-size: 14px;">Comentários em várias linhas<br /> </span>**</p> 

[php]
  
$comentario = "/\* comentario bla bla bla\*/";
  
if (preg_match(&#8216;/^[(/\*)+.+(\*/)]$/&#8217;, $comentario)) {
	  
echo "Comentário válido";
  
}
  
[/php]

**<span style="font-size: 14px;"><br /> </span>**

**<span style="font-size: 14px;">Datas (padrão brasileiro)<br /> </span>**</p> 

[php]
  
$data = "12/04/1990";
  
if (preg_match(&#8216;/^d{1,2}/d{1,2}/d{4}$/&#8217;, $data)) {
	  
echo "Data válida";
  
}
  
[/php]

**<span style="font-size: 14px;"><br /> </span>**

**<span style="font-size: 14px;">Cores hexadecimais<br /> </span>**</p> 

[php]
  
$cor = "#666666";
  
if (preg_match(&#8216;/^#(?:(?:[a-fd]{3}){1,2})$/i&#8217;, $cor)) {
  
echo "Cor válida";
  
}
  
[/php]</p> 

**<span style="font-size: 14px;">Endereços IP<br /> </span>**</p> 

[php]
  
$ip = "255.255.255.0";
  
if (preg_match(&#8216;^(?:25\[0-5]|2[0-4]d|1dd|[1-9]d|d)(?:[.\](?:25[0-5]|2[0-4]d|1dd|[1-9]d|d)){3}$&#8217;, $ip)) {
	  
echo "IP válido";
  
}
  
[/php]</p> 

**<span style="font-size: 14px;">E-mails<br /> </span>**</p> 

[php]
  
$email = "contato@fonini.net";
  
if (preg\_match(&#8216;/^\[^0-9\]\[a-zA-Z0-9\_\]+(\[.\]\[a-zA-Z0-9\_\]+)\*\[@\]\[a-zA-Z0-9\_\]+(\[.\]\[a-zA-Z0-9_\]+)\*\[.\]\[a-zA-Z\]{2,4}$/&#8217;,
  
$email)) {
	  
echo "E-mail válido";
  
}
  
[/php]