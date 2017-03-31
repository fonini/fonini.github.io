---
title: Como instalar o plugin de UML no NetBeans 6.8
date: 2010-03-11T09:00:46+00:00
author: fonini
layout: post
permalink: /2010/03/11/como-instalar-o-plugin-de-uml-no-netbeans-6-8/
categories:
  - Geral
  - Sem categoria
tags:
  - Plugins
---
O NetBeans tinha um plugin de UML muito massa nas versões mais antigas, mas tiraram nas últimas versões. Depois de alguma procura na internet, consegui encontrar uma forma de instalar o plugin na versão 6.8. Provavelmente essa técnica também funcionará nas próximas versões da IDE.

Abra o NetBeans e vá em Ferramentas/Plugins. Vá na aba Configurações e clique em Adicionar. Escolha um nome para o provedor de atualizações e coloque o seguinte endereço no campo URL: 

{% highlight html %}
http://ea.ddns.com.br:8090/netbeans6.8/UML/catalog.xml
{% endhighlight %}

Se o plugin não aparecer imediatamente na aba Plugins Disponíveis clique em Recarregar Catálogo. Quando ele aparecer, basta selecionar e instalar.

Abraço e até a próxima!