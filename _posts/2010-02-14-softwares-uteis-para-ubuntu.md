---
title: Softwares úteis para Ubuntu
date: 2010-02-14T14:23:49+00:00
author: fonini
layout: post
permalink: /2010/02/14/softwares-uteis-para-ubuntu/
categories:
  - Linux
  - Sem categoria
tags:
  - Linux
  - Repositório
  - Software Livre
  - Ubuntu
---
Criei essa lista para reunir alguns softwares essenciais para Ubuntu, tanto para desenvolvimento, como para diversão.

**Filezilla**
  
Um dos melhores clientes de FTP que já usei. Rápido, estável e bastante customizável.
  
Para instalar:

{% highlight shell %}sudo apt-get install filezilla{% endhighlight %}

**Guake Terminal**
  
Esse é o meu preferido. Um terminal que está sempre ao alcance, bastando teclar F12 (ou outra tecla de sua preferência). Pode-se mudar o nível de transparência do terminal, bem como customizar fontes, cores e colocar uma imagem de fundo.
  
Para instalar:

{% highlight shell %}sudo apt-get install guake{% endhighlight %}

**Kiki**
  
Programa muito útil para criar e testar expressões regulares
  
Para instalar:

{% highlight shell %}sudo apt-get install kiki{% endhighlight %}

**Inkscape**
  
Excelente editor de gráficos vetoriais. Uso bastante quando aqueles clientes chatos enviam logotipos em formato .cdr. Vale lembrar que esse software dá um banho legal no concorrente pago Corel Draw.
  
Para instalar:

{% highlight shell %}sudo apt-get install inkscape{% endhighlight %}

**Thunderbird**
  
Cliente de e-mail da Mozilla. Não precisa dizer mais nada.
  
Para instalar:

{% highlight shell %}sudo apt-get install thunderbird{% endhighlight %}

**WebHTTrack Website Copier**
  
Um daqueles programas que são o terror das empresas de hospedagem. Esse software permite que um site inteiro seja copiado para seu computador, gerando um trafego enorme no servidor onde o site está hospedado.
  
Para instalar:

{% highlight shell %}sudo apt-get install webhttrack<br />{% endhighlight %}

**EasyTag**

Para fãs de música paranóicos (como eu), esse software permite editar as tags ID3 de arquivos de áudio para manter tudo sua coleção de músicas organizada.
  
Para instalar:

{% highlight shell %}sudo apt-get install easytag{% endhighlight %}

**PulseAudio Equalizer**

Equalizador de 15 bandas para o PulseAudio, com várias configurações pré-definidas e bastante versátil.
  
Para instalar:

{% highlight shell %}wget http://dl.dropbox.com/u/1113424/webupd8/pulseaudio-equalizer_2.4_all2.deb<br />
sudo dpkg -i&nbsp; pulseaudio-equalizer_2.4_all2.deb{% endhighlight %}

**Ubuntu Tweak**
  
Esse programa permite realizar várias modificações no sistema, sendo que algumas não estão disponíveis em lugar nenhum, exceto no terminal.
  
Para instalar:

{% highlight shell %}wget http://launchpad.net/ubuntu-tweak/0.5.x/0.5.1/+download/ubuntu-tweak_0.5.1-1~karmic1_all.deb
sudo dpkg -i ubuntu-tweak_0.5.1-1~karmic1_all.deb{% endhighlight %}

**Wine**
  
Muito útil para executar programas feitos para Windows.
  
Para instalar:

{% highlight shell %}sudo apt-get install wine{% endhighlight %}

**Winetricks**
  
Complemento para o Wine. Permite que você instale facilmente dll's e outros complementos necessários para que alguns softwares interpretados pelo Wine funcionem.
  
Para instalar:

{% highlight shell %}sudo apt-get install zenity
wget http://www.kegel.com/wine/winetricks
chmod +x winetricks
sudo mv winetricks /usr/bin{% endhighlight %}

**Codecs**
  
O procedimento a seguir instala vários codecs muito úteis para reproduzir vários formato de áudio e vídeo
  
Para instalar:

{% highlight shell %}sudo wget http://www.medibuntu.org/sources.list.d/$(lsb_release&nbsp; -cs).list
--output-document=/etc/apt/sources.list.d/medibuntu.list &&
sudo apt-get -q update &&
sudo apt-get --yes -q --allow-unauthenticated install medibuntu-keyring &&
sudo apt-get -q update
sudo apt-get install w32codecs libdvdcss2 ubuntu-restricted-extras{% endhighlight %}