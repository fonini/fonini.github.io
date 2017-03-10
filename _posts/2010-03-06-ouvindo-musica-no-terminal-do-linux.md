---
id: 77
title: Ouvindo música no terminal do Linux
date: 2010-03-06T08:39:37+00:00
author: fonini
layout: post
guid: http://www.fonini.net/blog/?p=77
permalink: /2010/03/06/ouvindo-musica-no-terminal-do-linux/
categories:
  - Linux
  - Sem categoria
tags:
  - Terminal
---
Se tem uma coisa que eu gosto no Linux é o terminal. Não existem palavras pra descrever o terminal. As liberdades e funcionalidades que ele nos proporciona são imensas. Uma coisa que eu particularmente acho muito massa é a possibilidade de ouvir música através do terminal.

Vou dar algumas dicas de como fazer isso. O tutorial abrange dois softwares: mpg123 e mp3blaster. Vamos lá!

<span style="font-size: 14px;"><strong>mpg123<br /></strong></span>

Um dos softwares utilizados é o mpg123. Se você não tiver instalado na máquina, instale com o seguinte comando.</p> 

<pre id="terminal" user="fonini" computer="valhalla">sudo apt-get install mpg123</pre></p> 

Para ouvir a sua música, navegue até a pasta onde ela está e rode o seguinte comando:</p> 

<div class="terminal">
  <pre id="terminal" user="fonini" computer="valhalla">mpg123 sua_musica.mp3</pre></p> 
  
  <p>
    Para deixar o terminal livre para uso enquanto ouve a música, aperte CTRL + Z para parar o processo e em seguida rode o comando bg:
  </p></p> 
  
  <pre id="terminal" user="fonini" computer="valhalla">bg</pre></p> 
  
  <p>
    O terminal ficará parecido com esse:
  </p></p> 
  
  <pre id="terminal" user="fonini" computer="valhalla">bg
[1]+ mpg123 Avantasia - Reach Out for the Light.mp3 &</pre></p> 
  
  <p>
    A música ficará tocando em background e o terminal ficará livre para uso. Para parar a execução, execute os seguintes procedimentos:
  </p></p> 
  
  <pre id="terminal" user="fonini" computer="valhalla">jobs //mostra seus processos rodando em background, com o número de identificação
fg 1 //traz o processo de volta. Mude o número pelo do seu processo</pre></p> 
  
  <p>
    Para encerrar a reprodução, pressione CTRL+C ou CTRL+SHIFT+C.
  </p>
  
  <p>
  </p>
  
  <p>
    Você também pode ouvir uma pasta inteira com o seguinte comando:
  </p></p> 
  
  <pre id="terminal" user="fonini" computer="valhalla">mpg123 /home/usuario/pasta/*</pre></p> 
  
  <p>
    O software aceita vários argumentos. Os principais são:
  </p>
  
  <p>
    <strong>-g 70:</strong> Ajusta o volume (gain). Esse número varia de 0 até 100<br /> <strong>-n 3000:</strong> Decodifica somente 3000 frames<br /> <strong>-Z:</strong> Reprodução aleatória<br /> <strong>-q:</strong> Não mostra tags ID3 da música
  </p>
  
  <p>
    Para ver mais opções digite:
  </p></p> 
  
  <pre id="terminal" user="fonini" computer="valhalla">mpg123 --help</pre></p> 
  
  <p>
    <span style="font-size: 14px;"><strong></p> 
    
    <p>
      mp3blaster<br /></strong></span>
    </p>
    
    <p>
      Outro software, muito mais elaborado, contando com uma pequena interface em modo texto é o mp3blaster. Você pode instalar com o seguinte comando:
    </p></p> 
    
    <pre id="terminal" user="fonini" computer="valhalla">sudo apt-get install mp3blaster</pre></p> 
    
    <p>
      O software aceita uma música ou diretório como parâmetro inicial. Se não informar nada, o programa exibe a interface, bastante intuitiva pelo fato de ser em modo texto.
    </p>
    
    <p>
      Se você tiver problemas ao tocar alguma música ou receber a mensagem "<strong>Failed to open sound device</strong>", experimente fechar todos os aplicativos que estiverem usando o dispositivo de áudio no momento.
    </p>
    
    <p>
      Abraço e até a próxima!
    </p></p>