---
id: 66
title: Plugin Ajax Save para CKEditor 3
date: 2010-02-25T13:56:31+00:00
author: fonini
layout: post
guid: http://www.fonini.net/blog/?p=66
permalink: /2010/02/25/plugin-ajax-save-para-ckeditor-3/
categories:
  - Sem categoria
  - Web
tags:
  - CKEditor
  - Java Script
  - Plugins
---
Eu uso o CKEditor num gerador CRUD que eu desenvolvi em PHP, para gerar o painel de controle do site automaticamente através da modelagem do banco de dados. Ontem um cliente pediu um botão no CKEditor para salvar o texto sem dar refresh na página. Não encontrei nada pronto na Internet e resolvi desenvolver este plugin, o Ajax Save. O plugin adiciona um botão similar ao botão Salvar já existente no CKEditor, porém envia os dados via AJAX, ao contrário do primeiro, que somente submete o formulário onde o editor está contido. Let&#8217;s work!

Baixe o <a href="http://ckeditor.com/download" rel="externo">CKEditor</a> e extraia numa pasta de sua preferência.
  
Baixe o <a href="http://jquery.com" rel="externo">jQuery</a>.

Dentro da pasta &#8220;plugins&#8221; do CKEditor crie uma pasta chamada &#8220;ajaxsave&#8221;. Dentro da pasta &#8220;ajaxsave&#8221;, crie um arquivo chamado &#8220;plugin.js&#8221;, com o seguinte conteúdo:</p> 

[js]
  
(function(){
	  
var saveCmd ={
		  
modes : { wysiwyg:1, source:1 },
		  
exec : function( editor ){
      		  
var $form = editor.element.$.form;
			  
if ( $form ){
				  
try{
					  
editor.updateElement();
					  
content = editor.getData();

jQuery.ajax({
						  
type: "POST",
						  
url: "ckeditor/plugins/ajaxsave/save.php",
						  
data: "texto=" + content,
						  
success: function(msg){
						 	  
alert( "Dados recebidos: " + msg );
						  
}
					  
});
				  
}
				  
catch ( e ) {
            		  
//alert(e);
				  
}
			  
}
		  
}
	  
}

var pluginName = &#8216;ajaxsave&#8217;;
	  
CKEDITOR.plugins.add( pluginName,{
		  
init : function( editor ){
			  
var command = editor.addCommand( pluginName, saveCmd );
 			  
command.modes = { wysiwyg : !!( editor.element.$.form ) };
 			  
editor.ui.addButton( &#8216;AjaxSave&#8217;,{
				  
label : editor.lang.save,
				  
command : pluginName,
				  
icon: "plugins/ajaxsave/ajaxsave.png"
			  
});
		  
}
	  
});
  
})();
  
[/js]

Dentro desta mesma pasta ficará a página PHP que receberá os dados. Então, crie um arquivo chamado &#8220;save.php&#8221;, com o seguinte conteúdo:</p> 

[php]
  
echo $_POST[&#8216;texto&#8217;];
  
[/php]

Nesta mesma pasta deve ter a imagem que será usada no botão. Eu coloquei essa aqui: ![](/blog/wp-content/imagens/ajaxsave.png). O nome dela deve ser &#8220;ajaxsave.png&#8221;.

O plugin já está instalado. Agora vamos configurar o CKEditor para utilizar o plugin. Na pasta raíz do CKEditor existe um arquivo chamado &#8220;config.js&#8221;. Este arquivo é utilizado para definir as configurações globais do CKEditor. O conteúdo do meu está assim:

[js]
  
CKEDITOR.editorConfig = function( config ){
	  
config.extraPlugins = "ajaxsave";
	  
config.toolbar = [
		  
[&#8216;AjaxSave&#8217;, &#8216;Preview&#8217;],
		  
[&#8216;Cut&#8217;, &#8216;Copy&#8217;, &#8216;Paste&#8217;, &#8216;PasteText&#8217;, &#8216;PasteFromWord&#8217;, &#8216;-&#8216;, &#8216;Print&#8217;, &#8216;SpellChecker&#8217;],
		  
[&#8216;Undo&#8217;,&#8217;Redo&#8217;,&#8217;-&#8216;,&#8217;Find&#8217;,&#8217;Replace&#8217;,&#8217;-&#8216;,&#8217;SelectAll&#8217;,&#8217;RemoveFormat&#8217;],
		  
[&#8216;Bold&#8217;,&#8217;Italic&#8217;,&#8217;Underline&#8217;,&#8217;Strike&#8217;,&#8217;-&#8216;,&#8217;Subscript&#8217;],
		  
[&#8216;NumberedList&#8217;,&#8217;BulletedList&#8217;,&#8217;-&#8216;,&#8217;Outdent&#8217;,&#8217;Indent&#8217;,&#8217;Blockquote&#8217;],
		  
[&#8216;JustifyLeft&#8217;,&#8217;JustifyCenter&#8217;,&#8217;JustifyRight&#8217;,&#8217;JustifyBlock&#8217;],
		  
[&#8216;Link&#8217;,&#8217;Unlink&#8217;,&#8217;Anchor&#8217;],
		  
[&#8216;Image&#8217;,&#8217;Flash&#8217;,&#8217;Table&#8217;,&#8217;HorizontalRule&#8217;,&#8217;Smiley&#8217;,&#8217;SpecialChar&#8217;],
		  
[&#8216;Font&#8217;,&#8217;FontSize&#8217;],
		  
[&#8216;TextColor&#8217;,&#8217;BGColor&#8217;, &#8216;-&#8216;, &#8216;Source&#8217;]
	  
];
  
};
  
[/js]

Agora é só testar. Crie um arquivo chamado &#8220;index.html&#8221; dentro da pasta do CKEditor com o seguinte conteúdo:</p> 

[html]
  
<body>
  
<head>
  
<script type="text/javascript" src="ckeditor/ckeditor.js"></script>
  
<script type="text/javascript" src="jquery-1.4.2.min.js"><script>
  
</head>
  
<body>

<form method="post">
	  
<textarea name="editor"></textarea>

<script type="text/javascript">
		  
CKEDITOR.replace(&#8216;editor&#8217;);
	  
</script>
  
</form>

</body>
  
</html>
  
[/html]

Nesta página tem um <a href="http://www.fonini.net/labs/ckeditor" rel="externo">demo</a> da solução.

Abra o index.html, digite alguma coisa no editor e clique no botão do canto esquerdo superior. Um alerta deverá ser mostrado, com o conteúdo enviado via AJAX.

**Download dos arquivos**

[Plugin Ajax Save](http://www.fonini.net/labs/AjaxSave.plugin.zip)

[CKEditor, com jQuery 1.4.2 e plugin já integrado](http://www.fonini.net/labs/ckeditor.zip)

Abraço e até a próxima!</p>