---
title: Palíndromos em C ANSI
date: 2010-02-04T13:53:48+00:00
author: fonini
layout: post
permalink: /2010/02/04/palindromos-em-c-ansi/
categories:
  - Geral
  - Sem categoria
tags:
  - C
---
Nunca esqueço de uma prova de Programação I, do 2º semestre da faculdade, onde uma das questões consistia em fazer uma função que verificasse se a palavra passada por referência é um palíndromo, uma palavra que pode ser lida tanto da esquerda para a direita, quanto da direita para a esquerda. Lembro que não fui bem sucedido na época (rsrs), mas tá ai a dita função, escrita em C ANSI.

{% highlight c %}
#include <stdio.h>
#include <string.h>

int ehPalindromo(char *string){    
	char *s2 = string + strlen(string) - 1;

	if (!*string){
		return 1;
	}

	while(*string++ == *s2-- && *string);

	return !*string && *(--string) == *(++s2);
}

int main(){
	char string[255];

	printf("Palavra: ");
	gets(string);
	printf("%s %s n", string, ehPalindromo(string) ? "eh palindromo" : "nao eh palindromo");

	return(0);
}
{% endhighlight %}