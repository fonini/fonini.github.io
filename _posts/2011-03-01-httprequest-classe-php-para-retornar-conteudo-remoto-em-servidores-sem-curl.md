---
title: HTTPRequest, classe PHP para retornar conteúdo remoto em servidores sem cURL
date: 2011-03-01T19:49:14+00:00
author: fonini
layout: post
permalink: /2011/03/01/httprequest-classe-php-para-retornar-conteudo-remoto-em-servidores-sem-curl/
tags:
  - PHP
---
Ataquei de freelancer recentemente, tendo que desenvolver um site. O cliente já havia contratado um popular provedor de acesso ? internet da região para hospedar o site. Nada além do apocalipse poderia acontecer. Vou explicar. Os provedores da região na qual resido deveriam se preocupar um pouco mais em oferecer acesso de qualidade e deixar o ramo de hospedagem de aplicações web para quem realmente entende. O maldito servidor estava simplesmente "pelado", extensões importantes faltando e metade dos recursos úteis desabilitados.

Aonde já se viu um servidor sem cURL? Pois é, ainda fiz uma última tentativa para obter conteúdo remoto (previsão do tempo, infelizmente ainda é uma triste realidade por aqui o cliente exigir isso no site) usando file_get_contents(), mas adivinhem: allow_url_fopen desabilitado.

Felizmente existem os sockets! Dei uma fuçada na net, juntei alguns snippets e criei uma classe para facilitar o serviço. Podem conferir o código e outras informações no meu [Github](https://github.com/fonini/HTTPRequest).

Grande abraço!