---
id: 37
title: Expressões regulares para trabalhar com HTML
date: 2010-02-09T10:37:20+00:00
author: fonini
layout: post
guid: http://www.fonini.net/blog/?p=37
permalink: /2010/02/09/expressoes-regulares-para-trabalhar-com-html/
categories:
  - Regex
  - Sem categoria
  - Web
tags:
  - Expressão Regular
  - Regex
---
Reuni algumas expressões regulares úteis para trabalhar com HTML.

**Encontra comentários HTML  
** 

<!-;[sS]\*?-;[ tnr]\*>
  
<a href="http://regexpal.com/?flags=&regex=%3C!--[sS]*%3F--[%20tnr]*%3E&input=%3Chtml%3E%0A%3C!--%20comentario%20--%3E%0A%3C%2Fhtml%3E" rel="externo">Testar</a></p> 



**Captura o atributo href de links  
** 

href[s]\*=[s]\*"[^n"]*"
  
<a href="http://regexpal.com/?flags=&regex=href[s]*%3D[s]*%22[^n%22]*%22&input=%3Ca%20href%3D%22http%3A%2F%2Fwww.fonini.net%22%3EJonnas%20Fonini%3C%2Fa%3E" rel="externo">Testar</a></p> 



**Encontra todos os atributos de uma tag. Ex: src, name, value.
  
** 

(?:[w]\*) \*= \*"(?:(?:(?:(?:(?:\W)\*\W)\*[^"]\*)\W)\*[^"]\*")
  
<a href="http://regexpal.com/?flags=&regex=%28%3F%3A[w]*%29%20*%3D%20*%22%28%3F%3A%28%3F%3A%28%3F%3A%28%3F%3A%28%3F%3A\W%29*\W%29*[^%22]*%29\W%29*[^%22]*%22%29&input=%3Cimg%20src%3D%22imagem.jpg%22%20alt%3D%22Teste%22%20width%3D%2210px%22%20height%3D%2250px%22%20%2F%3E" rel="externo">Testar</a></p> 



**Encontra tags <h1> até <h6>  
** 

<h([1-6])>([^<]*)</h([1-6])>
  
<a href="http://regexpal.com/?flags=&regex=%3Ch%28[1-6]%29%3E%28[^%3C]*%29%3C%2Fh%28[1-6]%29%3E&input=%3Ch1%3ETitulo%3C%2Fh1%3E%0Abla%20bla%20bla%0A%3Ch3%3EOutro%20titulo%3C%2Fh3%3E" rel="externo">Testar</a></p> 



**Encontra tags <a> válidas  
** 

^<a[^>]\*([^"]\*)[^>]*>([ 0-9a-zA-Z]+)</a>$
  
<a href="http://regexpal.com/?flags=&regex=^%3Ca[^%3E]*%28[^%22]*%29[^%3E]*%3E%28[%200-9a-zA-Z]%2B%29%3C%2Fa%3E%24&input=%3Ca%20href%3D%22http%3A%2F%2Fwww.fonini.net%22%3EJonnas%20Fonini%3C%2Fa%3E" rel="externo">Testar</a></p> 



**Encontra todas as URL's de um texto  
** 

(http://|https://)([a-zA-Z0-9]+.[a-zA-Z0-9-]+|[a-zA-Z0-9-]+).[a-zA-Z.]{2,6}(/[a-zA-Z0-9.?=/#%&+-]+|/|)
  
<a href="http://regexpal.com/?flags=&regex=%28http%3A%2F%2F|https%3A%2F%2F%29%28[a-zA-Z0-9]%2B.[a-zA-Z0-9-]%2B|[a-zA-Z0-9-]%2B%29.[a-zA-Z.]{2%2C6}%28%2F[a-zA-Z0-9.%3F%3D%2F%23%25%26%2B-]%2B|%2F|%29&input=http%3A%2F%2Fwww.fonini.net%0Ahttp%3A%2F%2Fwww.pmvilamaria.com.br" rel="externo">Testar</a></p> 



**Encontra todas as imagens  
** 

<\[iI\]\[mM\]\[gG\]\[a-zA-Z0-9s=".\]\*((src)=s\*(?:"(\[^"]\*)"|'[^']\*'))[a-zA-Z0-9s=".]\*/\*>(?:</[iI\]\[mM\][gG]>)*
  
<a href="http://regexpal.com/?flags=&regex=%3C[iI][mM][gG][a-zA-Z0-9s%3D%22.]*%28%28src%29%3Ds*%28%3F%3A%22%28[^%22]*%29%22|%27[^%27]*%27%29%29[a-zA-Z0-9s%3D%22.]*%2F*%3E%28%3F%3A%3C%2F[iI][mM][gG]%3E%29*&input=%3Cimg%20src%3D%22teste.jpg%22%20%2F%3E" rel="externo">Testar</a></p> 



**Encontra tudo que está entre as tags especificadas. Mais tags podem ser adicionadas  
** 

<(script|style)[^>]\*?>(?:.|n)\*?</s\*1s\*>  
<a href="http://regexpal.com/?flags=&regex=%3C%28script|style%29[^%3E]*%3F%3E%28%3F%3A.|n%29*%3F%3C%2Fs*1s*%3E&input=%3Chtml%3E%0A%3Cscript%3E%0Aalert%28%27bla%27%29%3B%0A%3C%2Fscript%3E%0A%3C%2Fhtml%3E" rel="externo">Testar</a></p> 



**Útil para remover tags HTML  
** 

<[^>]*>
  
<a href="http://regexpal.com/?flags=&regex=%3C[^%3E]*%3E&input=%3Cp%3ETexto%3C%2Fp%3E" rel="externo">Testar</a></p> 



**Encontra extensões de arquivos  
** 

.([A-Za-z0-9]{2,5}($|b?))
  
<a href="http://regexpal.com/?flags=m&regex=.%28[A-Za-z0-9]{2%2C5}%28%24|b%3F%29%29&input=Baixe%20o%20arquivo%20teste.zip" rel="externo">Testar</a>

Se alguém tiver sugestões para mais expressões regulares, comente ou entre em contato.

Abraço e até a próxima!