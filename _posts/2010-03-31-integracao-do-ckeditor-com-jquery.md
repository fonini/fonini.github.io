---
id: 91
title: Integração do CKEditor com jQuery
date: 2010-03-31T08:39:08+00:00
author: fonini
layout: post
permalink: /2010/03/31/integracao-do-ckeditor-com-jquery/
categories:
  - Sem categoria
  - Web
tags:
  - CKEditor
  - Java Script
  - jQuery
---
O jQuery é uma biblioteca fantástica. O CKEditor é o editor mais completo. Por que não juntar os dois? Este tutorial mostra como fazer isso. Um dos grandes ganhos desta integração é que fica muito fácil manipular o "baixo nível" do CKEditor, principalmente se for salvar o conteúdo do editor com AJAX.

Pra começar, baixe a última versão do <a href="http://www.jquery.com" rel="externo nofollow">jQuery</a>. Baixe o <a href="http://www.ckeditor.com" rel="externo nofollow">CKEditor</a>. Extraia o CKEditor para uma pasta e coloque o jQuery na mesma pasta. O CKEditor já vem com um mecanismo que permite essa integração. Ele está localizado na pasta "adapters/jquery.js" e deve ser incluído no HTML da página.

**Instalação básica**

{% highlight html %}
<script type="text/javascript" src="jquery-1.4.2.min.js"></script>
<script type="text/javascript" src="ckeditor/ckeditor.js"></script>
<script type="text/javascript" src="ckeditor/adapters/jquery.js"></script>

<script type="text/javascript">	  
$(document).ready(function(){
  $('#editor').ckeditor();  
});
</script>

<form method="post">	  
  <textarea name="editor" id="editor"></textarea>  
</form>
{% endhighlight %}

**Instalação com parâmetros**

O CKEditor também aceita dois parâmetros: uma função de callback e os parâmetros de configuração do editor. Veja o exemplo:

{% highlight html %}
<script type="text/javascript">
$(document).ready(function(){
  $('#editor').ckeditor(function(){
      $('#resposta').html('<span style="color:red; font-weight: bold">CKEditor carregado!</span>');
  },{
    width: 780,
    height: 350
  });
});
</script>

<textarea name="editor" id="editor"></textarea>
<div id="resposta"></div>
{% endhighlight %}


Quando o editor for carregado no exemplo acima, a DIV resposta receberá algum texto. No segundo parâmetros, passamos a largura e altura do editor. Você pode consultar a <a href="http://docs.cksource.com/ckeditor_api/symbols/CKEDITOR.config.html" rel="externo nofollow">documentação da API</a> para conhecer as opções de configuração.


**Manipulando o editor**

Você também pode trabalhar com várias instâncias do editor na mesma página, setar e recuperar valores. Veja um exemplo:

{% highlight js %}
$(document).ready(function(){
  $('#editor').ckeditor(function(){
    $('#resposta').html('<span style="color:red; font-weight: bold">CKEditor carregado!</span>');

    var editor = $('#editor').ckeditorGet();

    // Capturando o conteúdo do editor

    var data = $('#editor').val();

    // Adicionando conteúdo ao editor
    $('#editor').val('<a href="https://fonini.github.io">fonini.github.io</a>');
  }, {
    width: 780,
    height: 350
  });
});{% endhighlight %}

Abraço e até a próxima!