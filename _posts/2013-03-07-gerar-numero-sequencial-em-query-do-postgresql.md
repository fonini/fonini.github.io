---
id: 449
title: Gerar número sequencial em query do PostgreSQL
date: 2013-03-07T17:20:08+00:00
author: fonini
layout: post
guid: http://www.fonini.net/blog/?p=449
permalink: /2013/03/07/gerar-numero-sequencial-em-query-do-postgresql/
categories:
  - Geral
  - Sem categoria
tags:
  - PostgreSQL
---
Dica rápida para quem precisa gerar um número sequencial para cada registro retornado por uma query no PostgreSQL:

[sql]
  
SELECT row\_number() OVER (PARTITION by 0) as \_seq, id, FROM pessoa
  
[/sql]

A sequência retornada começa em 1. Se quiser que ela comece em 0, basta adaptar a consulta:

[sql]
  
SELECT row\_number() OVER (PARTITION by 0) &#8211; 1 as \_seq, id, nome FROM pessoa
  
[/sql]

Caso você utilize uma cláusula ORDER BY, os números gerados provavelmente estarão fora de ordem. Para corrigir este problema, basta repetir a cláusula ORDER BY dentro da função OVER, ficando como no exemplo abaixo:

[sql]
  
SELECT row\_number() OVER (PARTITION by 0 ORDER BY data) &#8211; 1 as \_seq,
  
id, nome FROM pessoa
  
ORDER BY data
  
[/sql]