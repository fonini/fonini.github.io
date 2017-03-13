---
id: 60
title: Repositórios úteis para Ubuntu
date: 2010-02-23T11:15:32+00:00
author: fonini
layout: post
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

**Webmin (administração de servidores baseados em Unix com interface web)**

{% highlight shell %}sudo sh -c 'echo "deb http://download.webmin.com/download/repository sarge contrib" >> /etc/apt/sources.list'{% endhighlight %}

**Emesene (mensageiro instantâneo)**

{% highlight shell %}sudo sh -c 'echo "deb http://apt.emesene.org/ ./" >> /etc/apt/sources.list'{% endhighlight %}

**QBitTorrent (cliente BitTorrent)**

{% highlight shell %}sudo sh -c 'echo "deb http://ppa.launchpad.net/hydr0g3n/ppa/ubuntu jaunty main" >> /etc/apt/sources.list'
sudo apt-key adv --recv-keys --keyserver keyserver.ubuntu.com 47B4D1C4
sudo apt-get update && sudo apt-get install qbittorrent{% endhighlight %}

**Opera (navegador)**

{% highlight shell %}sudo sh -c 'echo "deb http://deb.opera.com/opera-beta/ stable non-free" >> /etc/apt/sources.list'
sudo wget -O - http://deb.opera.com/archive.key | sudo apt-key add -{% endhighlight %}

**XMMS (clone do Winamp para Linux)**

{% highlight shell %}sudo sh -c 'echo "deb http://www.pvv.ntnu.no/~knuta/xmms/karmic ./" >> /etc/apt/sources.list'{% endhighlight %}

**Cafuego (SecondLife, firmwares Broadcom, Inkscape...;)**

{% highlight shell %}wget -q -O - http://ubuntu.cafuego.net/cafuego.gpg | sudo apt-key add -
sudo sh -c 'echo "deb http://ubuntu.cafuego.net/ jaunty-cafuego all" >> /etc/apt/sources.list'{% endhighlight %}

**Ubuntu Satanic (versão satânica do Ubuntu, inútil, só achei interessante)**

{% highlight shell %}wget -q http://ubuntusatanic.org/ubuntu-se-key.gpg -O- | sudo apt-key add -
sudo sh -c 'echo "deb http://ubuntusatanic.org/hell karmic main" >> /etc/apt/sources.list'{% endhighlight %}

**VirtualBox (máquina virtual)**

{% highlight shell %}sudo sh -c 'echo "deb http://download.virtualbox.org/virtualbox/debian karmic non-free" >> /etc/apt/sources.list'
wget http://download.virtualbox.org/virtualbox/debian/sun_vbox.asc
sudo apt-key add sun_vbox.asc{% endhighlight %}

**DropBox (backup remoto)**

{% highlight shell %}sudo sh -c 'echo "deb http://linux.dropbox.com/ubuntu karmic main" >> /etc/apt/sources.list'
gpg --keyserver pgp.mit.edu --recv-keys 3565780E{% endhighlight %}

**Wicd (gerenciador de rede)**

{% highlight shell %}sudo sh -c 'echo "deb http://apt.wicd.net jaunty extras" >> /etc/apt/sources.list'
wget -q http://apt.wicd.net/wicd.gpg -O- | sudo apt-key add -{% endhighlight %}

**PlayOnLinux (instalador de jogos e softwares Windows para Linux)**

{% highlight shell %}sudo wget http://deb.playonlinux.com/playonlinux_karmic.list -O /etc/apt/sources.list.d/playonlinux.list{% endhighlight %}

**UbuntuGames (diversos games)**

{% highlight shell %}sudo sh -c 'echo "deb http://archive.ubuntugames.org ubuntugames main" >> /etc/apt/sources.list'{% endhighlight %}

**CompizFusion (efeitos gráficos)**

{% highlight shell %}sudo sh -c 'echo "deb http://ppa.launchpad.net/compiz/ppa/ubuntu karmic main multiverse restricted universe" >> /etc/apt/sources.list'{% endhighlight %}

**Gwibber (cliente de redes sociais)**

{% highlight shell %}sudo sh -c 'echo "deb http://ppa.launchpad.net/gwibber-daily/ppa/ubuntu karmic main universe restricted multiverse" >> /etc/apt/sources.list'{% endhighlight %}

**aMSN (mensageiro instantâneo)**

{% highlight shell %}sudo sh -c 'echo "deb http://ppa.launchpad.net/amsn-daily/ppa/ubuntu karmic main" >> /etc/apt/sources.list'{% endhighlight %}

**Gnome-Do (similar ao Katapult do KDE)**

{% highlight shell %}sudo sh -c 'echo "deb http://ppa.launchpad.net/do-core/ppa/ubuntu karmic main" >> /etc/apt/sources.list'{% endhighlight %}

**Ubuntu Tweak (diversos ajustes não disponíveis na interface gráfica)**

{% highlight shell %}sudo sh -c 'echo "deb http://ppa.launchpad.net/tualatrix/ppa/ubuntu karmic main multiverse restricted universe" >> /etc/apt/sources.list'{% endhighlight %}

**Medibuntu (Multimídia)**

{% highlight shell %}sudo wget --output-document=/etc/apt/sources.list.d/medibuntu.list http://www.medibuntu.org/sources.list.d/$(lsb_release -cs).list && sudo apt-get --quiet update && sudo apt-get --yes --quiet --allow-unauthenticated install medibuntu-keyring && sudo apt-get --quiet update{% endhighlight %}

**SwitFox (clone do Firefox)**

{% highlight shell %}sudo sh -c 'echo "deb http://getswiftfox.com/builds/debian unstable non-free" >> /etc/apt/sources.list'{% endhighlight %}

**Last.fm (scrobbler da Last.fm)**

{% highlight shell %}wget http://apt.last.fm/last.fm.repo.gpg -O- | sudo apt-key add -
sudo sh -c 'echo "deb http://apt.last.fm/ debian stable" >> /etc/apt/sources.list'{% endhighlight %}

**aMule (cliente P2P)**

{% highlight shell %}gpg --keyserver wwwkeys.eu.pgp.net --recv 50D0AE60
gpg --armor --export 50D0AE60 | sudo apt-key add -
sudo sh -c 'echo "deb http://www.vollstreckernet.de/debian/ stable amule wx" >> /etc/apt/sources.list'{% endhighlight %}

**Skype (mensageiro)**

{% highlight shell %}sudo sh -c 'echo "deb http://download.skype.com/linux/repos/debian/ stable non-free" >> /etc/apt/sources.list'{% endhighlight %}

**Google**

{% highlight shell %}sudo sh -c 'echo "deb http://dl.google.com/linux/deb/ stable non-free" >> /etc/apt/sources.list'{% endhighlight %}

**Wine (roda aplicativos Windows no Linux)**

{% highlight shell %}gpg --keyserver subkeys.pgp.net --recv 387EE263
gpg --export --armor 387EE263 | sudo apt-key add -
sudo sh -c 'echo "deb http://wine.budgetdedicated.com/apt karmic main" >> /etc/apt/sources.list'{% endhighlight %}

**VLC (reproduz arquivos multimídia)**

{% highlight shell %}sudo add-apt-repository ppa:c-korn/vlc{% endhighlight %}