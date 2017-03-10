---
id: 33
title: 'php.js:  Funções do PHP escritas em JavaScript'
date: 2010-02-05T14:45:05+00:00
author: fonini
layout: post
guid: http://www.fonini.net/blog/?p=33
permalink: /2010/02/05/php-js-funcoes-do-php-escritas-em-javascript/
categories:
  - Sem categoria
  - Web
tags:
  - Java Script
  - PHP
---
Recentemente comentei com o [@edipofederle](http://www.twitter.com/edipofederle) no Twitter que gostaria que existisse algo similar a função include() do PHP no JavaScript. Foi ai que eu descobri o [php.js](http://www.phpjs.org). O php.js é um projeto onde vários programadores (atualmente 254) estão escrevendo funções do PHP (atualmente 438) em JavaScript, facilitando muito a vida de quem conhece PHP mas não conhece bem JavaScript. As funções possuem sintaxes idênticas as do PHP, tornando o trabalho ainda mais fácil.

O mais legal do projeto é que você pode &#8220;compilar&#8221; sua própria versão do php.js, escolhendo as funções que você vai usar ou usando um dos pacotes já prontos no site do projeto.

Resolvi testar algumas funções e elas funcionam mesmo. Basta incluir o arquivo no seu código HTML e usar as funções. Aqui estão alguns exemplos que eu testei:</p> 

[js]
  
echo(checkdate(02, 29, 2010));
  
//Checa se a data é valida.
  
//Retornou false

echo(md5(&#8216;Jonnas&#8217;));
  
//Retorna o hash MD5 de uma string.
  
//Retornou: cbab5e5bde68b3fe1043d43ba94fef5c

array = new Array(&#8216;php&#8217;, &#8216;javascript&#8217;, &#8216;xhtml&#8217;);
  
echo(count(array));
  
//Conta a quantidade de elementos de um array.
  
//Retornou: 3

print_r(sort(array));
  
//Ordena o array e mostra todos os elemtos
  
//Retornou: Array ( [0] => javascript [1] => php [2] => xhtml )

echo(round(3,14159265));
  
Arredonda um nº em ponto flutuante
  
//Retornou: 3

echo(implode(&#8216;/&#8217;, array));
  
//Junta todos os elementos do array com uma barra, retornando uma string
  
//Retornou: php/javascript/xhtml
  
[/js]

Se você dispõe de tempo e vontade você pode ajudar o projeto escrevendo novas funções e melhorando as existentes.

Um abraço e até a próxima