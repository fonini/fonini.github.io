---
title: Transformando BBCode em XHTML com PHP e Regex
date: 2010-02-10T10:51:28+00:00
author: fonini
layout: post
permalink: /2010/02/10/transformando-bbcode-em-xhtml-com-php-e-regex/
tags:
  - Expressão Regular
  - Função
  - PHP
  - Regex
---
Atendendo a sugestão do amigo [@Eldius](http://twitter.com/Eldius), da galera do [#soudev](http://search.twitter.com/search?q=%23soudev) do [Twitter](http://twitter.com/fonini), criei uma função que converte texto em BBCode para XHTML, usando PHP e Regex. A função não é lá das mais elegantes, mas cumpre o prometido, lembrando que o BBCode deve estar escrito corretamente para que ela funcione.

{% highlight php %}<?php
function bbcode($str){
	$str = preg_replace("@\[b\](.+?)[/b]@i", '<strong>$1</strong>', $str);
	$str = preg_replace("@\[i\](.+?)[/i]@i", '<em>$1</em>', $str);  
	$str = preg_replace("@\[u\](.+?)[/u]@i", '<span style="text-decoration:underline">$1</span>', $str);
	$str = preg_replace("@\[s\](.+?)[/s]@i", '<span style="text-decoration:line-through">$1</span>', $str);
	$str = preg_replace("@\[img\](.+?)[/img]@i", '<img src="$1" alt="" />', $str);
	$str = preg_replace("@\[url\](.+?)[/url]@i", '[$1]($1)', $str);  
	$str = preg_replace("@\[url=(.+?)\](.+?)[/url]@i", '[$2]($1)', $str);  
	$str = preg_replace("@\[email\](.+?)[/email]@i", '[$1](mailto:$1)', $str);  
	$str = preg_replace("@\[email=(.+?)\](.+?)[/email]@i", '[$2](mailto:$1)', $str);  
	$str = preg_replace("@\[size=(.+?)\](.+?)[/size]@i", '<span style="font-size:$1px">$2</span>', $str);
	$str = preg_replace("@\[color=(.+?)\](.+?)[/color]@i", '<span style="color:$1">$2</span>', $str);
	$str = preg_replace("@[\*(?:s\*)]s\*([^[]\*)@i", '<li>$1</li>', $str);
	$str = preg_replace("@\[list(?:s\*)\]((.|n)\*?)[/list(?:s*)]@", '<ul>$1</ul>', $str);  
	$str = preg_replace("@\[list=1(?:s\*)\]((.|n)\*?)[/list(?:s*)]@", '<ol>$1</ol>', $str);  
	$str = preg_replace("@\[list=a(?:s\*)\]((.|n)\*?)[/list(?:s*)]@", '<ol style="list-style-type:lower-alpha">$1</ol>', $str);  
	$str = preg_replace("@\[list=i(?:s\*)\]((.|n)\*?)[/list(?:s*)]@", '<ol style="list-style-type:lower-roman">$1</ol>' ,$str);  
	$str = preg_replace("@\[list=I(?:s\*)\]((.|n)\*?)[/list(?:s*)]@", '<ol style="list-style-type:upper-roman">$1</ol>' ,$str);  
	$str = preg_replace("@\[list=A(?:s\*)\]((.|n)\*?)[/list(?:s*)]@", '<ol style="list-style-type:upper-alpha">$1</ol>' ,$str); 
	$str = preg_replace("@\[quote=(.+?)\](.+?)[/quote]@i", '$1 disse: <blockquote>$2</blockquote>', $str);  
	$str = preg_replace("@\[quote\](.+?)[/quote]@i", 'Citação: <blockquote>$1</blockquote>', $str);  
	$str = str_replace("n", '<br />', $str);  
	$str = preg_replace("@\[align=(.+?)\](.+?)[/align]@i", '<div style="text-align:$1">$2</div>', $str);  
	$str = preg_replace("@\[center\](.+?)[/center]@i", '<div style="text-align:center">$1</div>', $str);  
	$str = preg_replace("@\[code\](.+?)[/code]@i", '<pre>$1</pre>', $str);  
	$str = str_replace("[br]", '<br />', $str);

	return($str);
}

$string = '[b]Texto em negrito[/b][br][quote=Jonnas]Isso é BBCode[/quote] [br] [url=http://www.php.net][img]http://static.php.net/www.php.net/images/php.gif[/img][/url]';

echo bbcode($string);  
{% endhighlight %}

Essa função engloba os BBCodes mais conhecidos. Segue a lista abaixo:

**[b]** = Negrito

**[i]** = Itálico

**[u]** = Sublinhado

**[s]** = Texto riscado

**[img]** = Imagem

**[url]** = Link

**[email]** = E-mail

**[size]** = Tamanho do texto

**[color]** = Cor do texto

**[list=a]**, **[list=1]**, etc = Listas

**[quote]** = Citação

**[align]** = Alinhamento do texto

**[center]** = Centraliza o texto

**[code]** = Código

**[br]** = Quebra de página
  
Mais informações sobre BBCode podem ser encontradas [aqui](http://www.phpbb.com/community/faq.php?mode=bbcode) e [aqui](http://pt.wikipedia.org/wiki/BBCode)

Esse código também pode ser modificado facilmente para ser usado em conjunto com o [SyntaxHighlighter](http://alexgorbatchev.com/wiki/SyntaxHighlighter), um script para colorir o código, tornando a visualização mais amigável. Para isso, basta substituir a linha 25 por esta:

{% highlight php %}<?php	  
$str = preg_replace("@\[code=(.+?)\](.+?)[/code]@i", '<pre class="brush: $1">$2</pre>', $str);
{% endhighlight %}

Aí é usar de acordo com a nomenclatura do próprio script. Um código em PHP ficaria assim:

{% highlight bbcode %}
[code language="php"]$nome = "Jonnas";[/code]
{% endhighlight %}

Caso você encontre algum bug ou tem alguma sugestão, não deixe de entrar em contato.

Abraço e até a próxima!