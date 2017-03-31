---
id: 341
title: Converter arquivos .ts para .mp4
date: 2017-03-31T08:09:10+00:00
author: fonini
layout: post
permalink: /2017/03/31/converter-ts-para-mp4-linux
categories:
  - Sem categoria
  - Linux
---

Essa dica é para converter arquivos .ts para .mp4 no Linux.

No Ubuntu e sistemas Debian-like, basta instalar o avconv:

{% highlight shell %}
sudo apt-get install libav-tools
{% endhighlight %}

Em outras distribuições, instale o ffmpeg.

{% highlight shell %}
sudo apt-get install ffmpeg
{% endhighlight %}

São praticamente iguais, pois o avconv é um fork do ffmpeg.

Feito isso, abra o terminal, vá até a pasta do arquivo e digite o seguinte comando:

{% highlight shell %}
avconv -i origem.ts saida.mp4
{% endhighlight %}

Você também pode converter todos os arquivos .ts que estão na pasta com o seguinte comando:

{% highlight shell %}
for i in *.ts; do avconv -i "$i" "`echo $i | sed -e "s/.ts/.mp4/g"`"; done
{% endhighlight %}