---
title: Tutorial de programação com Brainfuck
date: 2010-04-29T09:32:42+00:00
author: fonini
layout: post
permalink: /2010/04/29/tutorial-de-programacao-com-brainfuck/
tags:
  - Nerd
---
Brainfuck é uma linguagem de programação esotérica, praticamente sem fins práticos, criada em 1993. Extremamente minimalista, possui apenas 8 comandos, com os quais é possível fazer inúmeras coisas. Não se deixe enganar pela sintaxe complicada e baixo número de comandos, esta linguagem é capaz de resolver qualquer problema computável. É uma excelente linguagem para treinar a sua lógica e, é claro, fazer jus ao nome da linguagem.

**Comandos**

<table border="0" cellpadding="1" cellspacing="1" style="width: 100%; height: 169px; border:1px solid #000">
  <tr>
    <td>
      .
    </td>
    
    <td>
      Imprime o caractere ASCII refente ao valor inteiro da célula atual
    </td>
  </tr>
  
  <tr>
    <td>
      ,
    </td>
    
    <td>
      Armazena o valor da próxima tecla a ser pressionada na célula atual
    </td>
  </tr>
  
  <tr>
    <td>
      +
    </td>
    
    <td>
      Incrementa em 1 o valor da célula atual
    </td>
  </tr>
  
  <tr>
    <td>
      -;
    </td>
    
    <td>
      Decrementa em 1 o valor da célula atual
    </td>
  </tr>
  
  <tr>
    <td>
      >
    </td>
    
    <td>
      Avança o ponteiro para a próxima célula
    </td>
  </tr>
  
  <tr>
    <td>
      <
    </td>
    
    <td>
      Retrocede o ponteiro para a célula anterior
    </td>
  </tr>
  
  <tr>
    <td>
      [
    </td>
    
    <td>
      Executa os comandos enquanto o valor da célula atual não for 0
    </td>
  </tr>
  
  <tr>
    <td>
      ]
    </td>
    
    <td>
      Fim do bloco de repetição
    </td>
  </tr>
</table>

**Compiladores**

Existem diversos compiladores para a linguagem, inclusive existe um nos repositórios do Ubuntu, o bf. Eu optei por compilar a versão em Assembly disponível [aqui](http://www.muppetlabs.com/~breadbox/software/tiny/bf.asm.txt). Após escrever o seu código-fonte, o compilador criará um executável binário.

**Codificando**

O brainfuck trabalha com células de memória, ou seja, cada caracter que você usar deverá estar armazenado em uma célula (ou não, no caso de usar sempre a mesma célula, mostrar o valor e sobrescrever, como eu faço no exemplo abaixo). Suponha que você queira mostrar a letra "j" em brainfuck. Você deverá armazenar 106 na célula (digitando 106 sinais de + ou criando um loop), que é o valor equivalente a "j" em ASCII. O código abaixo escreve "jonnas" na tela:

{% highlight brainfuck %}+++++++++++ Posição 1 recebe 11 e será a controladora do loop abaixo
	Enquanto o valor da primeira posição for maior que 0
	[
	- Decrementa o valor da posição 1
	> Avança para a posição 2
	+++++++++++ Posição 2 recebe 11
	< Volta para a posição 1
	]
	> Avança novamente para a posição 2
	--------------- . Decrementa 15 e imprime
	+++++ . Incrementa 5 e imprime
	- . Decrementa 1 e imprime
	. Apenas imprime novamente
	------------- . Decrementa 13 e imprime
	++++++++++++++++++ . Incrementa 18 e imprime
{% endhighlight %}

Apesar de parecer complicado, o processo é simples. A primeira linha armazena 11 na célula 1, que será o número de vezes que o loop executará. Enquanto a posição 1 não for 0, decrementamos a posição 1, avançamos para a posição 2, incrementamos seu valor em 11 e voltamos para a posição 1. Ao final do loop, o valor da posição 1 será 0 e da posição 2 será 121.
  
Como o valor da letra "j" em ASCII é 106, decrementamos 15 da posição 2 e mostramos. Para mostrar a letra "o", cujo valor é 111, devemos incrementar 5 na posição 2 e mostrar e assim sucessivamente até mostrar o nome inteiro. Veja abaixo uma versão do código sem comentários:

{% highlight brainfuck %}+++++++++++
[
	-
	>
	+++++++++++
	<
]
>
--------------- .
+++++ .
- .
.
------------- .
++++++++++++++++++ .
{% endhighlight %}

A versão do código em uma única linha é essa:

{% highlight brainfuck %}+++++++++++[->+++++++++++<]>---------------.+++++.-..-------------.++++++++++++++++++.{% endhighlight %}

Partindo daí, pode-se resolver inúmeros problemas em brainfuck e aprimorar a lógica cada vez mais.

Abraço e até a próxima!