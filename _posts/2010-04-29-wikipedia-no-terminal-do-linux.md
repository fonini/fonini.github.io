---
id: 100
title: Wikipédia no terminal do Linux
date: 2010-04-29T10:32:37+00:00
author: fonini
layout: post
guid: http://www.fonini.net/blog/?p=100
permalink: /2010/04/29/wikipedia-no-terminal-do-linux/
categories:
  - Linux
  - Sem categoria
tags:
  - Terminal
---
Tem louco pra tudo. É possível ver trechos de artigos da Wikipedia através de um lookup DNS em um servidor criado por <a href="https://dgl.cx/" rel="externo nofollow">David Leadbeater</a>. Por exemplo, para ler um trecho do artigo sobre Linux, digite o comando abaixo no terminal:</p> 

<pre id="terminal" computer="valhalla" user="fonini">dig +short txt Linux.wp.dg.cx</pre></p> 

Se você não tiver o dig pode fazer a consulta através do host:</p> 

<pre id="terminal" computer="valhalla" user="fonini">host -t txt Linux.wp.dg.cx</pre></p> 

Claro que isso não possui muita utilidade, pois somente são retornados 430 bytes. Outro problema é que, para consultas como por exemplo Power Metal, você deve inserir um underline entre as palavras, como é feito na Wikipédia.

Você também pode fazer um alias através do seguinte comando:</p> 

<pre id="terminal" computer="valhalla" user="fonini">wiki() { dig +short txt $1.wp.dg.cx; }</pre></p> 

E procurar da seguinte maneira:</p> 

<pre id="terminal" computer="valhalla" user="fonini">wiki Power_metal</pre></p> 

Abraço e até a próxima!</p>