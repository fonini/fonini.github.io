---
id: 9
title: Encurtando URLs com PHP usando a API do Bit.ly
date: 2010-01-28T14:34:02+00:00
author: fonini
layout: post
guid: http://www.fonini.net/blog/?p=9
permalink: /2010/01/28/encurtando-urls-com-a-api-do-bitly/
categories:
  - Sem categoria
  - Web
tags:
  - PHP
---
Este é o primeiro post do site e espero que gostem. Hoje vamos aprender como encurtar URL&#8217;s com PHP usando a API do <a href="http://www.bit.ly" rel="externo">Bit.ly</a>. O Bit.ly é um dos serviços de redução de URL&#8217;s mais populares da internet, tanto que o Twitter também usa esse serviço em sua página. Para começar você deve possuir a biblioteca cURL instalada em seu servidor e também deve criar uma conta no Bit.ly, onde será fornecida uma API Key que será usada nesse script. Criei esse código primeiramente pra usar aqui no site e resolvi disponibilizar para vocês. Segue o código:

Vamos supor que a URL a ser encurtada é a do Google: http://www.google.com.br

[php]$cURL = curl_init(&#8216;http://api.bit.ly/shorten?version=2.0.1&longUrl=http://www.google.com.br&login=SeuNomeDeUsuario&apiKey=
  
SuaAPIKeyFornecidaPeloBitLy&#8217;);
  
//Inicia o cURL passando o endereço que será requisitado

curl\_setopt($cURL, CURLOPT\_RETURNTRANSFER, true);
  
//Seta a opção CURLOPT_RETURNTRANSFER como true, assim, a resposta será retornada
  
//e não impressa na tela

$resultado = curl_exec($cURL);
  
//Armazena a resposta (em formato JSON) na variável $resultado

curl_close($cURL);
  
//Fecha o cURL

$link = json_decode($resultado, true);
  
//Decodifica o objeto JSON para um array, armazenando na variável $link

echo $link\[&#8216;results&#8217;\]\[&#8216;http://www.google.com.br&#8217;\][&#8216;shortUrl&#8217;];
  
//Aqui estão os índices do array que você deverá acessar para localizar a URL encurtada[/php]

Use a função print_r($link) para ver as outras opções retornadas pela API.

Espero que tenham gostado e até a p?oxima

Abraço,
  
Jonnas Fonini