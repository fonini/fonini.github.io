---
title: 'php.js:  Funções do PHP escritas em JavaScript'
date: 2010-02-05T14:45:05+00:00
author: fonini
layout: post
permalink: /2010/02/05/php-js-funcoes-do-php-escritas-em-javascript/
tags:
  - Java Script
  - PHP
---
Recentemente comentei com o [@edipofederle](http://www.twitter.com/edipofederle) no Twitter que gostaria que existisse algo similar a função include() do PHP no JavaScript. Foi ai que eu descobri o [php.js](http://www.phpjs.org). O php.js é um projeto onde vários programadores (atualmente 254) estão escrevendo funções do PHP (atualmente 438) em JavaScript, facilitando muito a vida de quem conhece PHP mas não conhece bem JavaScript. As funções possuem sintaxes idênticas as do PHP, tornando o trabalho ainda mais fácil.

O mais legal do projeto é que você pode "compilar" sua própria versão do php.js, escolhendo as funções que você vai usar ou usando um dos pacotes já prontos no site do projeto.

Resolvi testar algumas funções e elas funcionam mesmo. Basta incluir o arquivo no seu código HTML e usar as funções. Aqui estão alguns exemplos que eu testei:

{% highlight js %}
//Checa se a data é valida.
echo(checkdate(02, 29, 2010));
//Retornou false

//Retorna o hash MD5 de uma string.
echo(md5('Jonnas'));
//Retornou: cbab5e5bde68b3fe1043d43ba94fef5c

//Conta a quantidade de elementos de um array.
array = new Array('php', 'javascript', 'xhtml');
echo(count(array));
//Retornou: 3

//Ordena o array e mostra todos os elemtos
print_r(sort(array));
//Retornou: Array ( [0] => javascript [1] => php [2] => xhtml )

//Arredonda um nº em ponto flutuante
echo(round(3,14159265));
//Retornou: 3
{% endhighlight %}

Se você dispõe de tempo e vontade você pode ajudar o projeto escrevendo novas funções e melhorando as existentes.

Um abraço e até a próxima