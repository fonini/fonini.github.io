---
id: 102
title: Ajustes para o Ubuntu 10.04 Lucid Lynx
date: 2010-06-08T10:50:39+00:00
author: fonini
layout: post
guid: http://www.fonini.net/blog/?p=102
permalink: /2010/06/08/ajustes-para-o-ubuntu-10-04-lucid-lynx/
categories:
  - Linux
  - Sem categoria
tags:
  - Linux
  - Ubuntu
---
Aqui estão alguns ajustes que tive que fazer na minha instalação do Ubuntu 10.04 para deixar do jeito que eu queria. Compartilho aqui para o caso de alguém mais ter essas mesmas dúvidas. 

**Posição dos botões na barra de título**
  
O novo padrão adotado pela Canonical é posicionar os botões de fechar, maximizar e restaurar no lado esquerdo da janela. Felizmente, pra não quem não está acostumado com esta mudança, há uma maneira de voltar os botões ? posição original. Para isso, abra um terminal e digite:

<pre id="terminal" computer="valhalla" user="fonini">gconf-editor</pre>

Na janela que irá abrir, navegue em **apps/metacity/general** e altere o valor do campo **button_layout** para o mesmo que está na imagem abaixo e feche o programa para efetivar as alterações.

![](/blog/wp-content/imagens/gconf-editor.png)

**Applet de volume**
  
Outra mudança que eu notei (pode ser apenas um bug) é que o applet de volume não aparece mais na barra superior do Gnome. Para corrigir este problema, devemos adicionar o applet de volume aos aplicativos de sessão, que serão iniciados juntamente com o sistema. Para isso, vá em Sistema/Preferências/Aplicativos de sessão e clique em Adicionar, preenchendo com um nome escolhido por você e o seguinte comando: **/usr/bin/gnome-volume-control-applet**. Dessa forma, o aplicativo irá iniciar juntamente com o Gnome e sempre estará disponível.

**Barra de navegação nas pastas**
  
Antigamente existia um botão que permitia alterar a barra de navegação das pastas do modo gráfico para o modo texto, mas ele também sumiu na nova versão. Para alternar para a barra de navegação em modo texto, abra um terminal e digite:

<pre id="terminal" computer="valhalla" user="fonini">gconftool-2 --type=Boolean --set /apps/nautilus/preferences/always_use_location_entry true</pre>

**Reiniciar o X com CTRL+ALT+Backspace**
  
Para habilitar esta opção, vá em Sistema/Preferências/Teclado. Clique na aba Disposições e no botão Opções. Procure &#8220;Key sequence to kill the X Server&#8221; e marque a opção CTRL+ALT+Backspace.

**Caracteres inválidos no plugin Lyrics do Rhythmbox**
  
A nova versão do Rhythmbox inclui um plugin para buscar letras de músicas no Terra. Porém, os apóstrofos vem bagunçados. Para corrigir isso, execute os seguintes procedimentos:

<pre id="terminal" computer="valhalla" user="fonini">sudo gedit /usr/lib/rhythmbox/plugins/lyrics/TerraParser.py</pre>

Procure por esta linha **lyrics = re.sub(&#8216;<\[Bb\]\[Rr\]/>&#8216;, &#8221;, lyrics)** e adicione a seguinte linha abaixo dela: **lyrics = lyrics.replace(&#8216;&#039;&#8217;, &#8221;&#8217;)**. Salve o arquivo e reinicie o Rhythmbox.

Bom, esses foram os ajustes que eu precisei fazer na minha nova instalação do Ubuntu 10.04 Lucid Lynx. Espero que sejam úteis para alguém. Abraços e até a próxima!