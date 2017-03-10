---
id: 60
title: Repositórios úteis para Ubuntu
date: 2010-02-23T11:15:32+00:00
author: fonini
layout: post
guid: http://www.fonini.net/blog/?p=60
permalink: /2010/02/23/repositorios-uteis-para-ubuntu/
categories:
  - Linux
  - Sem categoria
tags:
  - Linux
  - Repositório
  - Ubuntu
---
Reuni alguns repositórios muito úteis para o Ubuntu, a maioria deles para Ubuntu 9.10. Todo o processo de adicionar os repositórios é feito pelo terminal (muito mais prático). Segue a lista:

<span style="font-size: 14px;"><strong>Webmin (administração de servidores baseados em Unix com interface web)</strong></span></p> 

<pre id="terminal" user="fonini" computer="valhalla">sudo sh -c "echo "deb http://download.webmin.com/download/repository sarge contrib" &gt;&gt; /etc/apt/sources.list"</pre></p> 

<span style="font-size: 14px;"><strong><br /> Emesene (mensageiro instantâneo)</strong></span></p> 

<pre id="terminal" user="fonini" computer="valhalla">sudo sh -c "echo "deb http://apt.emesene.org/ ./" &gt;&gt; /etc/apt/sources.list"</pre></p> 

<span style="font-size: 14px;"><strong><br /> QBitTorrent (cliente BitTorrent)</strong></span></p> 

<pre id="terminal" user="fonini" computer="valhalla">sudo sh -c "echo "deb http://ppa.launchpad.net/hydr0g3n/ppa/ubuntu jaunty main" &gt;&gt; /etc/apt/sources.list"
sudo apt-key adv --recv-keys --keyserver keyserver.ubuntu.com 47B4D1C4
sudo apt-get update && sudo apt-get install qbittorrent</pre></p> 

<span style="font-size: 14px;"><strong><br /> Opera (navegador)</strong></span></p> 

<pre id="terminal" user="fonini" computer="valhalla">sudo sh -c "echo "deb http://deb.opera.com/opera-beta/ stable non-free" &gt;&gt; /etc/apt/sources.list"
sudo wget -O - http://deb.opera.com/archive.key | sudo apt-key add -</pre>

<span style="font-size: 14px;"><strong><br /> XMMS (clone do Winamp para Linux)</strong></span></p> 

<pre id="terminal" user="fonini" computer="valhalla">sudo sh -c "echo "deb http://www.pvv.ntnu.no/~knuta/xmms/karmic ./" &gt;&gt; /etc/apt/sources.list"</pre></p> 

<span style="font-size: 14px;"><strong><br /> Cafuego (SecondLife, firmwares Broadcom, Inkscape...;)</strong></span></p> 

<pre id="terminal" user="fonini" computer="valhalla">wget -q -O - http://ubuntu.cafuego.net/cafuego.gpg | sudo apt-key add -
sudo sh -c "echo "deb http://ubuntu.cafuego.net/ jaunty-cafuego all" &gt;&gt; /etc/apt/sources.list"</pre>

<span style="font-size: 14px;"><strong><br /> Ubuntu Satanic (versão satânica do Ubuntu, inútil, só achei interessante)</strong></span></p> 

<pre id="terminal" user="fonini" computer="valhalla">wget -q http://ubuntusatanic.org/ubuntu-se-key.gpg -O- | sudo apt-key add -
sudo sh -c "echo "deb http://ubuntusatanic.org/hell karmic main" &gt;&gt; /etc/apt/sources.list"</pre></p> 

<span style="font-size: 14px;"><strong><br /> VirtualBox (máquina virtual)</strong></span></p> 

<pre id="terminal" user="fonini" computer="valhalla">sudo sh -c "echo "deb http://download.virtualbox.org/virtualbox/debian karmic non-free" &gt;&gt; /etc/apt/sources.list"
wget http://download.virtualbox.org/virtualbox/debian/sun_vbox.asc<br />
sudo apt-key add sun_vbox.asc</pre></p> 

<span style="font-size: 14px;"><strong><br /> DropBox (backup remoto)</strong></span></p> 

<pre id="terminal" user="fonini" computer="valhalla">sudo sh -c "echo "deb http://linux.dropbox.com/ubuntu karmic main" &gt;&gt; /etc/apt/sources.list"
gpg --keyserver pgp.mit.edu --recv-keys 3565780E</pre></p> 

<span style="font-size: 14px;"><strong><br /> Wicd (gerenciador de rede)</strong></span></p> 

<pre id="terminal" user="fonini" computer="valhalla">sudo sh -c "echo "deb http://apt.wicd.net jaunty extras" &gt;&gt; /etc/apt/sources.list"
wget -q http://apt.wicd.net/wicd.gpg -O- | sudo apt-key add -</pre></p> 

<span style="font-size: 14px;"><strong><br /> PlayOnLinux (instalador de jogos e softwares Windows para Linux)</strong></span></p> 

<pre id="terminal" user="fonini" computer="valhalla">sudo wget http://deb.playonlinux.com/playonlinux_karmic.list -O /etc/apt/sources.list.d/playonlinux.list</pre>

<span style="font-size: 14px;"><strong><br /> UbuntuGames (diversos games)</strong></span></p> 

<pre id="terminal" user="fonini" computer="valhalla">sudo sh -c "echo "deb http://archive.ubuntugames.org ubuntugames main" &gt;&gt; /etc/apt/sources.list"</pre></p> 

<span style="font-size: 14px;"><strong><br /> CompizFusion (efeitos gráficos)</strong></span></p> 

<pre id="terminal" user="fonini" computer="valhalla">sudo sh -c "echo "deb http://ppa.launchpad.net/compiz/ppa/ubuntu karmic main multiverse restricted universe" &gt;&gt; /etc/apt/sources.list"</pre>

<span style="font-size: 14px;"><strong><br /> Gwibber (cliente de redes sociais)</strong></span></p> 

<pre id="terminal" user="fonini" computer="valhalla">sudo sh -c "echo "deb http://ppa.launchpad.net/gwibber-daily/ppa/ubuntu karmic main universe restricted multiverse" &gt;&gt; /etc/apt/sources.list"</pre>

<span style="font-size: 14px;"><strong><br /> aMSN (mensageiro instantâneo)</strong></span></p> 

<pre id="terminal" user="fonini" computer="valhalla">sudo sh -c "echo "deb http://ppa.launchpad.net/amsn-daily/ppa/ubuntu karmic main" &gt;&gt; /etc/apt/sources.list"</pre>

<span style="font-size: 14px;"><strong><br /> Gnome-Do (similar ao Katapult do KDE)</strong></span></p> 

<pre id="terminal" user="fonini" computer="valhalla">sudo sh -c "echo "deb http://ppa.launchpad.net/do-core/ppa/ubuntu karmic main" &gt;&gt; /etc/apt/sources.list"</pre>

<span style="font-size: 14px;"><strong><br /> Ubuntu Tweak (diversos ajustes não disponíveis na interface gráfica)</strong></span></p> 

<pre id="terminal" user="fonini" computer="valhalla">sudo sh -c "echo "deb http://ppa.launchpad.net/tualatrix/ppa/ubuntu karmic main multiverse restricted universe" &gt;&gt; /etc/apt/sources.list"</pre>

<span style="font-size: 14px;"><strong><br /> Medibuntu (Multimídia)</strong></span></p> 

<pre id="terminal" user="fonini" computer="valhalla">sudo wget --output-document=/etc/apt/sources.list.d/medibuntu.list http://www.medibuntu.org/sources.list.d/$(lsb_release -cs).list && sudo apt-get --quiet update && sudo apt-get --yes --quiet --allow-unauthenticated install medibuntu-keyring && sudo apt-get --quiet update</pre>

<span style="font-size: 14px;"><strong><br /> SwitFox (clone do Firefox)</strong></span></p> 

<pre id="terminal" user="fonini" computer="valhalla">sudo sh -c "echo "deb http://getswiftfox.com/builds/debian unstable non-free" &gt;&gt; /etc/apt/sources.list"</pre>

<span style="font-size: 14px;"><strong><br /> Last.fm (scrobbler da Last.fm)<br /> </strong></span></p> 

<pre id="terminal" user="fonini" computer="valhalla">wget http://apt.last.fm/last.fm.repo.gpg -O- | sudo apt-key add -
sudo sh -c "echo "deb http://apt.last.fm/ debian stable" &gt;&gt; /etc/apt/sources.list"</pre>

<span style="font-size: 14px;"><strong><br /> aMule (cliente P2P)</strong></span></p> 

<pre id="terminal" user="fonini" computer="valhalla">gpg --keyserver wwwkeys.eu.pgp.net --recv 50D0AE60
gpg --armor --export 50D0AE60 | sudo apt-key add -
sudo sh -c "echo "deb http://www.vollstreckernet.de/debian/ stable amule wx" &gt;&gt; /etc/apt/sources.list"</pre>

<span style="font-size: 14px;"><strong><br /> Skype (mensageiro)</strong></span></p> 

<pre id="terminal" user="fonini" computer="valhalla">sudo sh -c "echo "deb http://download.skype.com/linux/repos/debian/ stable non-free" &gt;&gt; /etc/apt/sources.list"</pre>

<span style="font-size: 14px;"><strong><br /> Google</strong></span></p> 

<pre id="terminal" user="fonini" computer="valhalla">sudo sh -c "echo "deb http://dl.google.com/linux/deb/ stable non-free" &gt;&gt; /etc/apt/sources.list"</pre>

<span style="font-size: 14px;"><strong><br /> Wine (roda aplicativos Windows no Linux)</strong></span></p> 

<pre id="terminal" user="fonini" computer="valhalla">gpg --keyserver subkeys.pgp.net --recv 387EE263
gpg --export --armor 387EE263 | sudo apt-key add -
sudo sh -c "echo "deb http://wine.budgetdedicated.com/apt karmic main" &gt;&gt; /etc/apt/sources.list"</pre>

<span style="font-size: 14px;"><strong><br /> VLC (reproduz arquivos multimídia)</strong></span></p> 

<pre id="terminal" user="fonini" computer="valhalla">sudo add-apt-repository ppa:c-korn/vlc</pre></p>