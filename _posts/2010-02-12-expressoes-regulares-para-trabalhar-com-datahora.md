---
title: Expressões regulares para trabalhar com data/hora
date: 2010-02-12T10:37:20+00:00
author: fonini
layout: post
permalink: /2010/02/12/expressoes-regulares-para-trabalhar-com-datahora/
tags:
  - Expressão Regular
  - Regex
---
Mais um post da série sobre regex (Veja os anteriores aqui: [Expressões regulares para trabalhar com HTML](/2010/02/09/expressoes-regulares-para-trabalhar-com-html/) e [Expressões regulares para trabalhar com números](/2010/02/11/expressoes-regulares-para-trabalhar-com-numeros/)). Reuni algumas expressões regulares úteis para trabalhar com data e hora.

**Valida data no formato HH:MM** 
{% highlight regex %}
^(0-10-9|20-3):(0-50-9)$
{% endhighlight %}
  
<a href="http://regexpal.com/?flags=&regex=^%28[0-1][0-9]|[2][0-3]%29%3A%28[0-5][0-9]%29%24&input=12%3A30" rel="externo">Testar</a>

**Variação da anterior, porém não é necessário o separador** 
{% highlight regex %}
^(20|21|22|23|[0-1]d)[0-5]d$
{% endhighlight %}
  
<a href="http://regexpal.com/?flags=&regex=^%2820|21|22|23|[0-1]d%29[0-5]d%24&input=1540" rel="externo">Testar</a>

**Valida horas, com ou sem AM/PM. Os segundos não são obrigatórios**
{% highlight regex %}
^(((0]?1-9]|1[0-2])(:|.)[0-50-9\((:|.)0-5]0-9])?( )?(AM|am|aM|Am|PM|pm|pM|Pm))|(([0]?[0-9]|1[0-9]|2[0-3])(:|.)[0-50-9\((:|.)0-50-9)?))$
{% endhighlight %}
  
<a href="http://regexpal.com/?flags=&regex=^%28%28%28[0]%3F[1-9]|1[0-2]%29%28%3A|.%29[0-5][0-9]%28%28%3A|.%29[0-5][0-9]%29%3F%28%20%29%3F%28AM|am|aM|Am|PM|pm|pM|Pm%29%29|%28%28[0]%3F[0-9]|1[0-9]|2[0-3]%29%28%3A|.%29[0-5][0-9]%28%28%3A|.%29[0-5][0-9]%29%3F%29%29%24&input=03%3A40%20AM" rel="externo">Testar</a>

**Valida datas no formato dd/mm/yyyy hh:mm:ss**
{% highlight regex %}
^((((31/(0?13578]|1[02]))|((29|30)/(0?[1,3-9]|1[0-2])))/(1[6-9]|[2-9]d)?d{2})|(29/0?2/(((1[6-9]|[2-9]d)?(0[48]|[2468048|1357926)|((16|2468048|357926)00))))|(0?[1-9]|1d|2[0-8])/((0?[1-9])|(1[0-2]))/((1[6-9]|[2-9]d)?d{2})) (20|21|22|23|[0-1]?d):[0-5]?d:[0-5]?d$
{% endhighlight %}
	  
<a href="http://regexpal.com/?flags=&regex=^%28%28%28%2831%2F%280%3F[13578]|1[02]%29%29|%28%2829|30%29%2F%280%3F[1%2C3-9]|1[0-2]%29%29%29%2F%281[6-9]|[2-9]d%29%3Fd{2}%29|%2829%2F0%3F2%2F%28%28%281[6-9]|[2-9]d%29%3F%280[48]|[2468][048]|[13579][26]%29|%28%2816|[2468][048]|[3579][26]%2900%29%29%29%29|%280%3F[1-9]|1d|2[0-8]%29%2F%28%280%3F[1-9]%29|%281[0-2]%29%29%2F%28%281[6-9]|[2-9]d%29%3Fd{2}%29%29%20%2820|21|22|23|[0-1]%3Fd%29%3A[0-5]%3Fd%3A[0-5]%3Fd%24&input=12%2F04%2F1990%2014%3A00%3A50" rel="externo">Testar</a>

**Valida datas entre 1/1/1900 até 31/12/2099**
{% highlight regex %}
(^((((01-9])|(1-20-9)|(3[0-1]))|([1-9]))x2F(((0[1-9])|(1[0-2]))|([1-9]))x2F(([0-9]{2})|(((19)|([2([0]{1})))([0-9]{2}))))$)
{% endhighlight %}
	  
<a href="http://regexpal.com/?flags=&regex=%28^%28%28%28%280[1-9]%29|%28[1-2][0-9]%29|%283[0-1]%29%29|%28[1-9]%29%29x2F%28%28%280[1-9]%29|%281[0-2]%29%29|%28[1-9]%29%29x2F%28%28[0-9]{2}%29|%28%28%2819%29|%28[2]%28[0]{1}%29%29%29%28[0-9]{2}%29%29%29%29%24%29&input=12%2F04%2F1990" rel="externo">Testar</a>

**Valida data e hora ou somente hora ou somente data. Data no formato m/d/y**
{% highlight regex %}
^(?=d)(?:(?:(?:(?:(?:0?13578]|1[02])(/|-|.)31)1|(?:(?:0?[1,3-9]|1[0-2])(/|-|.)(?:29|30)2))(?:(?:1[6-9]|[2-9]d)?d{2})|(?:0?2(/|-|.)293(?:(?:(?:1[6-9]|[2-9]d)?(?:0[48]|[2468048|1357926)|(?:(?:16|2468048|357926)00))))|(?:(?:0?[1-9])|(?:1[0-2]))(/|-|.)(?:0?[1-9]|1d|2[0-8])4(?:(?:1[6-9]|[2-9]d)?d{2}))($| (?=d)))?(((0?[1-9]|1[012])(:[0-5]d){0,2}( [AP]M))|([01]d|2[0-3])(:[0-5]d){1,2})?$
{% endhighlight %}
	  
<a href="http://regexpal.com/?flags=&regex=^%28%3F%3Dd%29%28%3F%3A%28%3F%3A%28%3F%3A%28%3F%3A%28%3F%3A0%3F[13578]|1[02]%29%28%2F|-|.%2931%291|%28%3F%3A%28%3F%3A0%3F[1%2C3-9]|1[0-2]%29%28%2F|-|.%29%28%3F%3A29|30%292%29%29%28%3F%3A%28%3F%3A1[6-9]|[2-9]d%29%3Fd{2}%29|%28%3F%3A0%3F2%28%2F|-|.%29293%28%3F%3A%28%3F%3A%28%3F%3A1[6-9]|[2-9]d%29%3F%28%3F%3A0[48]|[2468][048]|[13579][26]%29|%28%3F%3A%28%3F%3A16|[2468][048]|[3579][26]%2900%29%29%29%29|%28%3F%3A%28%3F%3A0%3F[1-9]%29|%28%3F%3A1[0-2]%29%29%28%2F|-|.%29%28%3F%3A0%3F[1-9]|1d|2[0-8]%294%28%3F%3A%28%3F%3A1[6-9]|[2-9]d%29%3Fd{2}%29%29%28%24|%20%28%3F%3Dd%29%29%29%3F%28%28%280%3F[1-9]|1[012]%29%28%3A[0-5]d%29{0%2C2}%28%20[AP]M%29%29|%28[01]d|2[0-3]%29%28%3A[0-5]d%29{1%2C2}%29%3F%24&input=04%2F12%2F1990%2014%3A30%3A45" rel="externo">Testar</a>

**Valida dias da semana em inglês, resumidos ou não**
{% highlight regex %}
^(Sun|Mon|(T(ues|hurs))|Fri)(day|.)?$|Wed(.|nesday)?$|Sat(.|urday)?$|T((ue?)|(hu?r?)).?$
{% endhighlight %}
	  
<a href="http://regexpal.com/?flags=&regex=^%28Sun|Mon|%28T%28ues|hurs%29%29|Fri%29%28day|.%29%3F%24|Wed%28.|nesday%29%3F%24|Sat%28.|urday%29%3F%24|T%28%28ue%3F%29|%28hu%3Fr%3F%29%29.%3F%24&input=Sunday" rel="externo">Testar</a>

**Valida datas no formato MMM dd, yyyy**
{% highlight regex %}
^(?:(((Jan(uary)?|Ma(r(ch)?|y)|Jul(y)?|Aug(ust)?|Oct(ober)?|Dec(ember)?) 31)|((Jan(uary)?|Ma(r(ch)?|y)|Apr(il)?|Ju((ly?)|(ne?))|Aug(ust)?|Oct(ober)?|(Sept|Nov|Dec)(ember)?) (0?1-9]|([12]d)|30))|(Feb(ruary)? (0?[1-9]|1d|2[0-8]|(29(?=, ((1[6-9]|[2-9]d)(0[48]|[2468048|1357926)|((16|2468048|357926)00))))))), ((1[6-9]|[2-9]d)d{2}))
{% endhighlight %}
	  
<a href="http://regexpal.com/?flags=&regex=^%28%3F%3A%28%28%28Jan%28uary%29%3F|Ma%28r%28ch%29%3F|y%29|Jul%28y%29%3F|Aug%28ust%29%3F|Oct%28ober%29%3F|Dec%28ember%29%3F%29%2031%29|%28%28Jan%28uary%29%3F|Ma%28r%28ch%29%3F|y%29|Apr%28il%29%3F|Ju%28%28ly%3F%29|%28ne%3F%29%29|Aug%28ust%29%3F|Oct%28ober%29%3F|%28Sept|Nov|Dec%29%28ember%29%3F%29%20%280%3F[1-9]|%28[12]d%29|30%29%29|%28Feb%28ruary%29%3F%20%280%3F[1-9]|1d|2[0-8]|%2829%28%3F%3D%2C%20%28%281[6-9]|[2-9]d%29%280[48]|[2468][048]|[13579][26]%29|%28%2816|[2468][048]|[3579][26]%2900%29%29%29%29%29%29%29%2C%20%28%281[6-9]|[2-9]d%29d{2}%29%29&input=April%2012%2C%201990" rel="externo">Testar</a>

**Encontra nomes de meses em inglês**
{% highlight regex %}
^(?:J(anuary|u(ne|ly))|February|Ma(rch|y)|A(pril|ugust)|(((Sept|Nov|Dec)em)|Octo)ber)$
{% endhighlight %}
	  
<a href="http://regexpal.com/?flags=&regex=^%28%3F%3AJ%28anuary|u%28ne|ly%29%29|February|Ma%28rch|y%29|A%28pril|ugust%29|%28%28%28Sept|Nov|Dec%29em%29|Octo%29ber%29%24&input=September" rel="externo">Testar</a>

**Valida datas no formato dd/mm/yyyy**
{% highlight regex %}
^(((01-9]|[12]d|3[01])/(0[13578]|1[02])/(d{2}))|((0[1-9]|[12]d|30)/(0[13456789]|1[012])/(d{2}))|((0[1-9]|1d|2[0-8])/02/(d{2}))|(29/02/((0[48]|[2468048|1357926)|(00))))$
{% endhighlight %}
	  
<a href="http://regexpal.com/?flags=&regex=^%28%28%280[1-9]|[12]d|3[01]%29%2F%280[13578]|1[02]%29%2F%28d{2}%29%29|%28%280[1-9]|[12]d|30%29%2F%280[13456789]|1[012]%29%2F%28d{2}%29%29|%28%280[1-9]|1d|2[0-8]%29%2F02%2F%28d{2}%29%29|%2829%2F02%2F%28%280[48]|[2468][048]|[13579][26]%29|%2800%29%29%29%29%24&input=12%2F04%2F90" rel="externo">Testar</a>

**Encontra fusos horários**
{% highlight regex %}
[-+]((0[0-9]|1[0-3]):([03]0|45)|14:00)
{% endhighlight %}
	  
<a href="http://regexpal.com/?flags=&regex=[-%2B]%28%280[0-9]|1[0-3]%29%3A%28[03]0|45%29|14%3A00%29&input=-03%3A00" rel="externo">Testar</a>

**Valida datas no formato mm/dd/yyyy ou mm-dd-yyyy**
{% highlight regex %}
^(((((((0?13578])|(1[02]))[.-/]?((0?[1-9])|([12]d)|(3[01])))|(((0?[469])|(11))[.-/]?((0?[1-9])|([12]d)|(30)))|((0?2)[.-/]?((0?[1-9])|(1d)|(2[0-8]))))[.-/]?(((19)|(20))?([dd))))|((0?2).-/]?(29)[.-/]?(((19)|(20))?(([02468048)|(1357926)))))$
{% endhighlight %}
	  
<a href="http://regexpal.com/?flags=&regex=^%28%28%28%28%28%28%280%3F[13578]%29|%281[02]%29%29[.-%2F]%3F%28%280%3F[1-9]%29|%28[12]d%29|%283[01]%29%29%29|%28%28%280%3F[469]%29|%2811%29%29[.-%2F]%3F%28%280%3F[1-9]%29|%28[12]d%29|%2830%29%29%29|%28%280%3F2%29[.-%2F]%3F%28%280%3F[1-9]%29|%281d%29|%282[0-8]%29%29%29%29[.-%2F]%3F%28%28%2819%29|%2820%29%29%3F%28[d][d]%29%29%29%29|%28%280%3F2%29[.-%2F]%3F%2829%29[.-%2F]%3F%28%28%2819%29|%2820%29%29%3F%28%28[02468][048]%29|%28[13579][26]%29%29%29%29%29%24&input=12%2F31%2F2009" rel="externo">Testar</a>

**Encontra meses válidos**
{% highlight regex %}
^((0?[1-9])|(1[0-2]))$
{% endhighlight %}
	  
<a href="http://regexpal.com/?flags=&regex=^%28%280%3F[1-9]%29|%281[0-2]%29%29%24&input=1" rel="externo">Testar</a>

É isso ai. Abraço e até a próxima!