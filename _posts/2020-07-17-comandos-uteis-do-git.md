---
title: "Comandos úteis do git"
date: 2020-07-17 13:53:40 -0300
layout: post
author: fonini
permalink: /2020/07/17/comandos-uteis-do-git/
tags: 
  - git
---

#### Desfazer o último commit, preservando as alterações nos arquivos

{% highlight shell %}
git reset --soft HEAD~1
{% endhighlight %}


#### Desfazer o primeiro commit, preservando as alterações nos arquivos

{% highlight shell %}
git update-ref -d HEAD
{% endhighlight %}


#### Desfazer o último commit, **não** preservando as alterações nos arquivos

{% highlight shell %}
git reset --hard HEAD~1
{% endhighlight %}


#### Criar branch a partir do stash

{% highlight shell %}
git stash branch testchanges
{% endhighlight %}