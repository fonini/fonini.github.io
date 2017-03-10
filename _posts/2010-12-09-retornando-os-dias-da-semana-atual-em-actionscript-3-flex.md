---
id: 126
title: Retornando os dias da semana atual em ActionScript 3 / Flex
date: 2010-12-09T09:51:35+00:00
author: fonini
layout: post
guid: http://www.fonini.net/blog/?p=126
permalink: /2010/12/09/retornando-os-dias-da-semana-atual-em-actionscript-3-flex/
categories:
  - Sem categoria
  - Web
tags:
  - Action Script 3
  - Flex
  - Função
---
Final de ano, projetos da empresa indo a milhão, últimas provas do semestre&#8230;é, não tá fácil, a correria tá desgraçada. Passei aqui pra remover as teias de aranha do blog e compartilhar esta função que pode ser útil para alguém. Infelizmente perdi a fonte de onde encontrei esta função, mas lembro que ela tinha um erro no retorno (já corrigido por mim). A função original só retornava os dias úteis da semana, mas o que eu precisava era dos dias da semana inteira, começando no domingo. Com algumas modificações, aí está o resultado.  
Essa função é bastante útil para se colocar num helper (que sabe numa dessas crio um e publico o código).



[as3]
  
public function getCurrentWeekDays():Array{
	  
var output:Array = new Array();
	  
var formattedDate:String;
	  
var date:Date = new Date();

date.setDate(date.getDate() &#8211; date.getDay() &#8211; 1);

for (var i:int = 0; i < 7; i++) {
		  
date.setDate(date.getDate() + 1);

formattedDate = (date.getDate() < 10) ? "0" +
  
date.getDate().toString() : date.getDate().toString();
		  
formattedDate += "/";
		  
formattedDate += (date.getMonth() + 1 < 10) ? "0" +
  
(date.getMonth() + 1).toString() : (date.getMonth() + 1).toString();

output[i] = formattedDate;
	  
}
	  
return output;
  
}[/as3]

E para usar:

[as3]
  
var diasSemana:Array = getCurrentWeekDays();[/as3]

Os dias serão retornados no seguinte formato: 05/11, 06/11, 07/11. A função pode ser facilmente adaptada para também retornar o ano ou retornar a data em outro formato.

É isso aí pessoal, esse é o último post do ano. Ano que vem prometo posts mais freqüentes.
  
Um Feliz Natal para todos e um Ano Novo repleto de realizações, muito café, código e eterno aprendizado.

Grande abraço a todos!