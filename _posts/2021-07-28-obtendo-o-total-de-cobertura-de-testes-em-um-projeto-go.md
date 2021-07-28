---
title: "Obtendo o total de cobertura de testes em um projeto Go"
date: 2021-07-28 09:15:40 -0300
layout: post
author: fonini
permalink: /2021/07/28/obtendo-o-total-de-cobertura-de-testes-em-um-projeto-go/
tags: 
  - golang
---

Para obter a porcentagem total de cobertura de testes em um projeto Go, basta rodar os comandos abaixo:

{% highlight shell %}
go test -v -coverpkg=./... -coverprofile=cover.out ./...
go tool cover -func cover.out
{% endhighlight %}

O segundo comando irá detalhar a cobertura de testes de todos os arquivos e ao final mostrará a porcentagem total.

Se desejar mostrar somente a porcentagem, sem o restante do output, substitua o segundo comando por:

{% highlight shell %}
go tool cover -func cover.out | grep total | awk '{print $3}'
{% endhighlight %}
