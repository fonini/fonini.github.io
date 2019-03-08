---
title: "Plugin do OneSignal no Ionic AppFlow"
date: 2019-03-08 11:33:08 -0300
layout: post
author: fonini
permalink: /2019/03/08/plugin-do-onesignal-no-ionic-appflow/
tags: 
  - ionic
  - onesignal
---

Ao compilar apps no Ionic AppFlow, podem ocorrer erros EACCES quando utilizamos o plugin do OneSignal.

Para corrigir, basta dar permissão nos scripts do CocoaPods:

{% highlight shell %}
git update-index --chmod=+x run_pods.sh
git update-index --chmod=+x update_pods.sh
{% endhighlight %}
