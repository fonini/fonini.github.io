---
id: 404
title: 'Convertendo de UTF-8 para ISO-8859-1 em Java: A solução definitiva'
date: 2012-02-29T14:54:19+00:00
author: fonini
layout: post
guid: http://www.fonini.net/blog/?p=404
permalink: /2012/02/29/convertendo-de-utf-8-para-iso-8859-1-em-java-a-solucao-definitiva/
categories:
  - Sem categoria
  - Web
tags:
  - Charset
  - Java
---
Recentemente enfrentei problemas em um aplicativo Android que desenvolvi, o qual se comunica com o banco de dados de um dos sistemas da empresa, codificado em ISO-8859-1 (Firebird) através de um web service. 

Os dados eram gravados de forma errada, muitas vezes truncavam e as vezes apareciam caracteres estranhos. 

Depois de algumas tentativas, cheguei até a seguinte solução: 



[java]
  
public static String convertUTF8toISO(String str) {
	  
String ret = null;
	  
try {
		  
ret = new String(str.getBytes("ISO-8859-1"), "UTF-8");
	  
}
	  
catch (java.io.UnsupportedEncodingException e) {
		  
return null;
	  
}
	  
return ret;
  
}
  
[/java]

Adicione o método acima ? sua classe de utilidades e acabe com os seus problemas. 

Abraço. 

&nbsp;