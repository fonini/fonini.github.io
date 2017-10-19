---
title: "Lendo a temperatura da Raspberry Pi"
date: 2017-10-19 16:58:04
layout: post
author: fonini
permalink: /2017/10/19/lendo-a-temperatura-da-raspberry-pi/
tags: 
  - Linux,Raspberry
---

Utilize o seguinte comando:

{% highlight shell %}
cat /sys/class/thermal/thermal_zone0/temp
{% endhighlight %}

Para formatar a saída em graus Celsius, utilize o seguinte comando:

{% highlight shell %}
awk '{printf("%.1f °C\n",$1/1e3)}' /sys/class/thermal/thermal_zone0/temp
{% endhighlight %}