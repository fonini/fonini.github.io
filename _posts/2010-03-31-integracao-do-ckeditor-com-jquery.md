---
id: 91
title: Integração do CKEditor com jQuery
date: 2010-03-31T08:39:08+00:00
author: fonini
layout: post
guid: http://www.fonini.net/blog/?p=91
permalink: /2010/03/31/integracao-do-ckeditor-com-jquery/
socialize_text:
  - 'If you enjoyed this post, please consider <a href="#comments">leaving a comment</a> or <a href="http://www.fonini.net/blog/feed" title="Syndicate this site using RSS">subscribing to the <abbr title="Really Simple Syndication">RSS</abbr> feed</a> to have future articles delivered to your feed reader.'
socialize:
  - 1,2,8,24,17,18
categories:
  - Sem categoria
  - Web
tags:
  - CKEditor
  - Java Script
  - jQuery
---
O jQuery é uma biblioteca fantástica. O CKEditor é o editor mais completo. Por quê não juntar os dois? Este tutorial mostra como fazer isso. Um dos grandes ganhos desta integração é que fica muito fácil manipular o "baixo nível" do CKEditor, principalmente se for salvar o conteúdo do editor com AJAX.

Pra começar, baixe a última versão do <a href="http://www.jquery.com" rel="externo nofollow">jQuery</a>. Baixe o <a href="http://www.ckeditor.com" rel="externo nofollow">CKEditor</a>. Extraia o CKEditor para uma pasta e coloque o jQuery na mesma pasta. O CKEditor já vem com um mecanismo que permite essa integração. Ele está localizado na pasta "adapters/jquery.js" e deve ser incluído no HTML da página.

<span style="font-size: 14px;"><strong><br />Instalação básica<br /></strong></span></p> 

[xml]
	  
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
  
[/xml]

<span style="font-size: 14px;"><strong></p> 

<p>
  Instalação com parâmetros<br /></strong></span>
</p>

<p>
  O CKEditor também aceita dois parâmetros: uma função de callback e os parâmetros de configuração do editor. Veja o exemplo:
</p></p> 

<p>
  [html]<br /> <script type="text/javascript"><br /> $(document).ready(function(){<br /> $('#editor').ckeditor(function(){<br /> $('#resposta').html('<span style="color:red; font-weight: bold">CKEditor carregado!</span>');<br /> },<br /> {<br /> width: 780,<br /> height: 350<br /> });<br /> });<br /> </script>
</p>

<p>
  <textarea name="editor" id="editor"></textarea>
</p>

<p>
  <div id="resposta"></div><br /> [/html]
</p>

<p>
  Quando o editor for carregado no exemplo acima, a DIV resposta receberá algum texto. No segundo parâmetros, passamos a largura e altura do editor. Você pode consultar a <a href="http://docs.cksource.com/ckeditor_api/symbols/CKEDITOR.config.html" rel="externo nofollow">documentação da API</a> para conhecer as opções de configuração.
</p></p> 

<p>
  <span style="font-size: 14px;"><strong>Manipulando o editor<br /></strong></span>
</p>

<p>
  Você também pode trabalhar com várias instâncias do editor na mesma página, setar e recuperar valores. Veja um exemplo:
</p></p> 

<p>
  {% highlight js %}<br /> $(document).ready(function(){<br /> $('#editor').ckeditor(function(){<br /> $('#resposta').html('<span style="color:red; font-weight: bold">CKEditor carregado!</span>');
</p>

<p>
  var editor = $('#editor').ckeditorGet();
</p>

<p>
  // Capturando o conteúdo do editor<br /> var data = $('#editor').val();<br /> // Adicionando conteúdo ao editor<br /> $('#editor').val('<a href="http://www.fonini.net">www.fonini.net</a>');<br /> },<br /> {<br /> width: 780,<br /> height: 350<br /> });<br /> });<br /> {% endhighlight %}
</p>

<p>
  <span style="font-size: 14px;"><strong><br />Demo<br /></strong></span>
</p>

<p>
  Veja um demo online, clicando <a href="http://www.fonini.net/labs/ckeditor/jquery" rel="externo nofollow">aqui</a>.
</p>

<p>
  Abraço e até a próxima!
</p>