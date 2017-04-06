---
title: "Criar novo post no Jekyll via terminal"
date: 2017-04-06 09:03:25 -0300
layout: post
author: fonini
permalink: /2017/04/06/criar-novo-post-no-jekyll-via-terminal/
tags:
  - Linux
  - Jekyll
  - Shell
---

Criei o shell script abaixo pra facilitar a criação de posts no Jekyll. Este post foi o batismo de fogo do script.

Adicione o script ao seu .bashrc ou crie um .sh e coloque no $PATH.

Para criar um novo post:

{% highlight shell %}
create-post "Meu novo post"
{% endhighlight %}

Ou simplesmente:

{% highlight shell %}
create-post
{% endhighlight %}

O script irá pedir alguns dados e criará o arquivo .md.

Você deve rodar o script na pasta raíz do seu blog ou dentro da pasta _posts.

<script src="https://gist.github.com/fonini/e44faaacc77188742d21d92e452ce689.js"></script>