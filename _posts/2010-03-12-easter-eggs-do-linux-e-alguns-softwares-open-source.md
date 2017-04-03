---
title: Easter Eggs do Linux (e alguns softwares Open Source)
date: 2010-03-12T09:22:07+00:00
author: fonini
layout: post
permalink: /2010/03/12/easter-eggs-do-linux-e-alguns-softwares-open-source/
tags:
  - Linux
  - Terminal
---
Qual nerd que não gosta de Easter Eggs? São brincadeiras engraçadas (ou no mínimo curiosas) embutidas em alguns softwares, para você dar uma relaxada naqueles momentos em que tudo parece dar errado ou seu cérebro está fundindo.

Reuni uma lista com os Easter Eggs mais conhecidos do Linux e de alguns outros softwares Open Source. Have fun!



**Código fonte do kernel**

No terminal, digite:

{% highlight shell %}grep -R fuck /usr/src/linux-headers-2.6.31-20/*{% endhighlight %}

Substitua a palavra "fuck" por outras e também lembre de substituir a versão do kernel pela versão que você está usando. Você pode fazer isso pressionando TAB após digitar até linux-headers ou através do comando "uname -r".



**Documentação em distribuições Debian-like**

No terminal, digite:

{% highlight shell %}zgrep "The.*Release" /usr/share/doc/dpkg/changelog.Debian.gz{% endhighlight %}

**Vim (Vi improved)**

{% highlight shell %}vim{% endhighlight %}
Digite :help 42 e verá uma referência ao Guia do Mochileiro das Galáxias

**Data Discordiana**

{% highlight shell %}ddate{% endhighlight %}
Este comando exibe a data de hoje no [Calendário Discordiano](http://pt.wikipedia.org/wiki/Calend%C3%A1rio_discordiano). Você também pode passar outra data por parâmetro.

**Cowsay**

{% highlight shell %}sudo apt-get install cowsay
cowsay 'Alguma coisa'
cowsay -f head-in.cow ouch //esse é massa
{% endhighlight %}

**Aptitude**

{% highlight shell %}aptitude moo
aptitude -v moo
aptitude -v -v moo
aptitude -v -v -v moo
aptitude -v -v -v -v moo
aptitude -v -v -v -v -v moo
aptitude -v -v -v -v -v -v moo{% endhighlight %}
      
**Yes**

Não achei muita graça nesse, é só um loop infinito no terminal. Você também pode passar algum texto por parâmetro.
{% highlight shell %}yes
yes 1234567890{% endhighlight %}

Pressione CTRL+C quando seu computador estiver quase derretendo.

**sl**

Quantas vezes na correria acabamos errando e ditando "sl" ao invés de "ls". Podemos instalar o programa sl e ao digitar errado seremos avisados por meio de animações no terminal, e segundo a man page desse aplicativo a função dele é alertar os desatentos que erram o comando "ls".
        
{% highlight shell %}sudo apt-get install sl
sl
sl -a
sl -F
sl -l
man sl  //manual do programa{% endhighlight %}

**apt-get**

Digite o comando abaixo e verifique a última linha do manual.

{% highlight shell %}apt-get -h{% endhighlight %}

**Mozilla Firefox**

Os easter eggs do Firefox são os mais famosos, e não podem ser deixados de lado. Na barra de endereços digite:

about:mozilla
about:robots

**Open Office (funcionam também no BrOffice.org)**

Abra uma planilha e ponha a seguinte linha na célula A1 para jogar o jogo da velha:

=GAME(A2:C4;"TicTacToe")

Ponha a linha abaixo em qualquer célula e pressione Enter

=ANTWORT("Das Leben, das Universum und der ganze Rest")

O comando abaixo permite a você jogar um game baseado em StarWars

=GAME("StarWars")

O comando abaixo mostra uma foto da equipe de desenvolvedores do aplicativo:

=STARCALCTEAM()

Agora abra o editor de textos e digite a linha abaixo, seguida de F3 e veja uma foto do time de desenvolvedores

StarWriterTeam

**Gnome**

Pressione ALT+F2 e digite "free the fish" (sem aspas) na tela que irá aparecer. Você verá um peixe passeando pela sua tela. No início eu achei legal, mas chegou uma hora que eu fiquei com muita raiva do peixe. Para matá-lo, abra o terminal e digite:

{% highlight shell %}pkill gnome-panel{% endhighlight %}

Você também pode jogar com o peixinho. Tecle novamente ALT+F2 e digite "gegls from outer space" (sem aspas).

**Perl**

Não chega a ser um Easter Egg, mas é uma data histórica para todos nós. O dia em que Linus Torvalds começou a escrever o kernel do Linux. Digite no terminal:

{% highlight shell %}perl -e 'print localtime(672274793). "\n";'{% endhighlight %}

**GParted**

Como usuário comum, digite o comando abaixo no terminal e veja a mensagem de alerta:
{% highlight shell %}gparted{% endhighlight %}