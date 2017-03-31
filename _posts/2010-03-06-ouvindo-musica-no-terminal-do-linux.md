---
title: Ouvindo música no terminal do Linux
date: 2010-03-06T08:39:37+00:00
author: fonini
layout: post
permalink: /2010/03/06/ouvindo-musica-no-terminal-do-linux/
categories:
  - Linux
  - Sem categoria
tags:
  - Terminal
---
Se tem uma coisa que eu gosto no Linux é o terminal. Não existem palavras pra descrever o terminal. As liberdades e funcionalidades que ele nos proporciona são imensas. Uma coisa que eu particularmente acho muito massa é a possibilidade de ouvir música através do terminal.

Vou dar algumas dicas de como fazer isso. O tutorial abrange dois softwares: mpg123 e mp3blaster. Vamos lá!

**mpg123**

Um dos softwares utilizados é o mpg123. Se você não tiver instalado na máquina, instale com o seguinte comando. 

{% highlight shell %}sudo apt-get install mpg123{% endhighlight %}

Para ouvir a sua música, navegue até a pasta onde ela está e rode o seguinte comando: 

{% highlight shell %}mpg123 sua_musica.mp3{% endhighlight %}   

Para deixar o terminal livre para uso enquanto ouve a música, aperte CTRL + Z para parar o processo e em seguida rode o comando bg:   

{% highlight shell %}bg{% endhighlight %} 
  
O terminal ficará parecido com esse:  
{% highlight shell %}bg
[1]+ mpg123 Avantasia - Reach Out for the Light.mp3 &{% endhighlight %} 

A música ficará tocando em background e o terminal ficará livre para uso. Para parar a execução, execute os seguintes procedimentos:

{% highlight shell %}jobs //mostra seus processos rodando em background, com o número de identificação
fg 1 //traz o processo de volta. Mude o número pelo do seu processo{% endhighlight %} 

Para encerrar a reprodução, pressione CTRL+C ou CTRL+SHIFT+C.

Você também pode ouvir uma pasta inteira com o seguinte comando:
     
{% highlight shell %}mpg123 /home/usuario/pasta/*{% endhighlight %} 

O software aceita vários argumentos. Os principais são:

**-g 70:** Ajusta o volume (gain). Esse número varia de 0 até 100

**-n 3000:** Decodifica somente 3000 frames

**-Z:** Reprodução aleatória

**-q:** Não mostra tags ID3 da música

Para ver mais opções digite:

{% highlight shell %}mpg123 --help{% endhighlight %} 

**mp3blaster**

Outro software, muito mais elaborado, contando com uma pequena interface em modo texto é o mp3blaster. Você pode instalar com o seguinte comando:

{% highlight shell %}sudo apt-get install mp3blaster{% endhighlight %} 

O software aceita uma música ou diretório como parâmetro inicial. Se não informar nada, o programa exibe a interface, bastante intuitiva pelo fato de ser em modo texto.

Se você tiver problemas ao tocar alguma música ou receber a mensagem "**Failed to open sound device**", experimente fechar todos os aplicativos que estiverem usando o dispositivo de áudio no momento.

Abraço e até a próxima!    