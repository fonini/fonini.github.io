---
title: "Convertendo certificados Let's Encrypt standalone para webroot"
date: 2020-01-02 15:58:54 -0300
layout: post
author: fonini
permalink: /2020/01/02/convertendo-certificados-lets-encrypt-standalone-para-webroot/
tags: 
  - ssl
  - linux
---

Converter todos os certificados Let's Encrypt obtidos no modo standalone para o modo webroot.

{% highlight shell %}
sudo certbot renew -a webroot --force-renewal --webroot-path /var/www
{% endhighlight %}