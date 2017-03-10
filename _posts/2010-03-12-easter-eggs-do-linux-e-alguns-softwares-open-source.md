---
id: 85
title: Easter Eggs do Linux (e alguns softwares Open Source)
date: 2010-03-12T09:22:07+00:00
author: fonini
layout: post
guid: http://www.fonini.net/blog/?p=85
permalink: /2010/03/12/easter-eggs-do-linux-e-alguns-softwares-open-source/
categories:
  - Linux
  - Sem categoria
tags:
  - Linux
  - Terminal
---
Qual nerd que não gosta de Easter Eggs? São brincadeiras engraçadas (ou no mínimo curiosas) embutidas em alguns softwares, para você dar uma relaxada naqueles momentos em que tudo parece dar errado ou seu cérebro está fundindo.

Reuni uma lista com os Easter Eggs mais conhecidos do Linux e de alguns outros softwares Open Source. Have fun!



<span style="font-size: 14px;"><strong>Código fonte do kernel</strong></span>

No terminal, digite:</p> 

<pre id="terminal" user="fonini" computer="valhalla">grep -R fuck /usr/src/linux-headers-2.6.31-20/*</pre></p> 

Substitua a palavra &#8220;fuck&#8221; por outras e também lembre de substituir a versão do kernel pela versão que você está usando. Você pode fazer isso pressionando TAB após digitar até linux-headers ou através do comando &#8220;uname -r&#8221;.



<span style="font-size: 14px;"><strong>Documentação em distribuições Debian-like</strong></span>

No terminal, digite:</p> 

<pre id="terminal" user="fonini" computer="valhalla">zgrep "The.*Release" /usr/share/doc/dpkg/changelog.Debian.gz</pre></p> 

<span style="font-size: 14px;"><strong></p> 

<p>
  Vim (Vi improved)</strong></span>
</p></p> 

<pre id="terminal" user="fonini" computer="valhalla">vim</pre></p> 

<p>
  Digite :help 42 e verá uma referência ao Guia do Mochileiro das Galáxias
</p>

<p>
  <span style="font-size: 14px;"><strong></p> 
  
  <p>
    Data Discordiana</strong></span>
  </p></p> 
  
  <pre id="terminal" user="fonini" computer="valhalla">ddate</pre></p> 
  
  <p>
    Este comando exibe a data de hoje no <a href="http://pt.wikipedia.org/wiki/Calend%C3%A1rio_discordiano" rel="externo nofollow">Calendário Discordiano</a>. Você também pode passar outra data por parâmetro.
  </p>
  
  <p>
    <span style="font-size: 14px;"><strong></p> 
    
    <p>
      Cowsay</strong></span>
    </p></p> 
    
    <pre id="terminal" user="fonini" computer="valhalla">sudo apt-get install cowsay
cowsay 'Alguma coisa'
cowsay -f head-in.cow ouch //esse é massa
</pre></p> 
    
    <p>
      <span style="font-size: 14px;"><strong></p> 
      
      <p>
        Aptitude</strong></span>
      </p></p> 
      
      <pre id="terminal" user="fonini" computer="valhalla">aptitude moo
aptitude -v moo
aptitude -v -v moo
aptitude -v -v -v moo
aptitude -v -v -v -v moo
aptitude -v -v -v -v -v moo
aptitude -v -v -v -v -v -v moo</pre></p> 
      
      <p>
        <span style="font-size: 14px;"><strong></p> 
        
        <p>
          Yes</strong></span>
        </p>
        
        <p>
          Não achei muita graça nesse, é só um loop infinito no terminal. Você também pode passar algum texto por parâmetro.
        </p></p> 
        
        <pre id="terminal" user="fonini" computer="valhalla">yes
yes 1234567890</pre></p> 
        
        <p>
          Pressione CTRL+C quando seu computador estiver quase derretendo.
        </p>
        
        <p>
          <span style="font-size: 14px;"><strong></p> 
          
          <p>
            sl</strong></span>
          </p>
          
          <p>
            Quantas vezes na correria acabamos errando e ditando &#8220;sl&#8221; ao invés de &#8220;ls&#8221;. Podemos instalar o programa sl e ao digitar errado seremos avisados por meio de animações no terminal, e segundo a man page desse aplicativo a função dele é alertar os desatentos que erram o comando &#8220;ls&#8221;.
          </p></p> 
          
          <pre id="terminal" user="fonini" computer="valhalla">sudo apt-get install sl
sl
sl -a
sl -F
sl -l
man sl  //manual do programa</pre></p> 
          
          <p>
            <span style="font-size: 14px;"><strong></p> 
            
            <p>
              Apt-get</strong></span>
            </p>
            
            <p>
              Digite o comando abaixo e verifique a última linha do manual.
            </p></p> 
            
            <pre id="terminal" user="fonini" computer="valhalla">apt-get -h</pre></p> 
            
            <p>
              <span style="font-size: 14px;"><strong><br />Mozilla Firefox</strong></span>
            </p>
            
            <p>
              Os easter eggs do Firefox são os mais famosos, e não podem ser deixados de lado. Na barra de endereços digite:
            </p>
            
            <p>
              about:mozilla<br />about:robots
            </p>
            
            <p>
              <span style="font-size: 14px;"><strong></p> 
              
              <p>
                Open Office (funcionam também no BrOffice.org)</strong></span>
              </p>
              
              <p>
                Abra uma planilha e ponha a seguinte linha na célula A1 para jogar o jogo da velha:
              </p>
              
              <p>
                =GAME(A2:C4;&#8221;TicTacToe&#8221;)
              </p></p> 
              
              <p>
                Ponha a linha abaixo em qualquer célula e pressione Enter
              </p>
              
              <p>
                =ANTWORT(&#8220;Das Leben, das Universum und der ganze Rest&#8221;)
              </p></p> 
              
              <p>
                O comando abaixo permite a você jogar um game baseado em StarWars
              </p>
              
              <p>
                =GAME(&#8220;StarWars&#8221;)
              </p></p> 
              
              <p>
                O comando abaixo mostra uma foto da equipe de desenvolvedores do aplicativo:
              </p>
              
              <p>
                =STARCALCTEAM()
              </p>
              
              <p>
                Agora abra o editor de textos e digite a linha abaixo, seguida de F3 e veja uma foto do time de desenvolvedores
              </p>
              
              <p>
                StarWriterTeam
              </p>
              
              <p>
                <span style="font-size: 14px;"><strong></p> 
                
                <p>
                  Gnome<br /></strong></span>
                </p>
                
                <p>
                  Pressione ALT+F2 e digite &#8220;free the fish&#8221; (sem aspas) na tela que irá aparecer. Você verá um peixe passeando pela sua tela. No início eu achei legal, mas chegou uma hora que eu fiquei com muita raiva do peixe ? Para matá-lo, abra o terminal e digite:
                </p></p> 
                
                <pre id="terminal" user="fonini" computer="valhalla">pkill gnome-panel</pre></p> 
                
                <p>
                  Você também pode jogar com o peixinho. Tecle novamente ALT+F2 e digite &#8220;gegls from outer space&#8221; (sem aspas).
                </p>
                
                <p>
                  <span style="font-size: 14px;"><strong></p> 
                  
                  <p>
                    Perl<br /></strong></span>
                  </p>
                  
                  <p>
                    Não chega a ser um Easter Egg, mas é uma data histórica para todos nós. O dia em que Linus Torvalds começou a escrever o kernel do Linux. Digite no terminal:
                  </p></p> 
                  
                  <pre id="terminal" user="fonini" computer="valhalla">perl -e 'print localtime(672274793). "n";'</pre></p> 
                  
                  <p>
                    <span style="font-size: 14px;"><strong></p> 
                    
                    <p>
                      GParted<br /></strong></span>
                    </p>
                    
                    <p>
                      Como usuário comum, digite o comando abaixo no terminal e veja a mensagem de alerta:
                    </p></p> 
                    
                    <pre id="terminal" user="fonini" computer="valhalla">gparted</pre></p> 
                    
                    <p>
                    </p>