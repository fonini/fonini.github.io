---
id: 66
title: Plugin Ajax Save para CKEditor 3
date: 2010-02-25T13:56:31+00:00
author: fonini
layout: post
permalink: /2010/02/25/plugin-ajax-save-para-ckeditor-3/
categories:
  - Sem categoria
  - Web
tags:
  - CKEditor
  - Java Script
  - Plugins
---
Eu uso o CKEditor num gerador CRUD que eu desenvolvi em PHP, para gerar o painel de controle do site automaticamente através da modelagem do banco de dados. Ontem um cliente pediu um botão no CKEditor para salvar o texto sem dar refresh na página. Não encontrei nada pronto na Internet e resolvi desenvolver este plugin, o Ajax Save. O plugin adiciona um botão similar ao botão Salvar já existente no CKEditor, porém envia os dados via AJAX, ao contrário do primeiro, que somente submete o formulário onde o editor está contido. Let's work!

Baixe o <a href="http://ckeditor.com/download" rel="externo">CKEditor</a> e extraia numa pasta de sua preferência.
  
Baixe o <a href="http://jquery.com" rel="externo">jQuery</a>.

Dentro da pasta "plugins" do CKEditor crie uma pasta chamada "ajaxsave". Dentro da pasta "ajaxsave", crie um arquivo chamado "plugin.js", com o seguinte conteúdo: 

{% highlight js %}
(function(){
	var saveCmd = {
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
				catch(e){
					console.log(e);
				}
			}
		}
	}

	var pluginName = 'ajaxsave';

	CKEDITOR.plugins.add( pluginName, {
		init : function( editor ){
			var command = editor.addCommand( pluginName, saveCmd );
			command.modes = { wysiwyg : !!( editor.element.$.form ) };

			editor.ui.addButton( 'AjaxSave', {
				label : editor.lang.save,
				command : pluginName,
				icon: "plugins/ajaxsave/ajaxsave.png"
			});
		}
	});
})();
{% endhighlight %}

Dentro desta mesma pasta ficará a página PHP que receberá os dados. Então, crie um arquivo chamado "save.php", com o seguinte conteúdo: 

{% highlight php %}<?php
echo $_POST['texto'];
{% endhighlight %}

Nesta mesma pasta deve ter a imagem que será usada no botão. Eu coloquei essa aqui: ![](/blog/wp-content/imagens/ajaxsave.png). O nome dela deve ser "ajaxsave.png".

O plugin já está instalado. Agora vamos configurar o CKEditor para utilizar o plugin. Na pasta raíz do CKEditor existe um arquivo chamado "config.js". Este arquivo é utilizado para definir as configurações globais do CKEditor. O conteúdo do meu está assim:

{% highlight js %}
CKEDITOR.editorConfig = function( config ){
	config.extraPlugins = "ajaxsave";

	config.toolbar = [
		['AjaxSave', 'Preview'],
		['Cut', 'Copy', 'Paste', 'PasteText', 'PasteFromWord', '-', 'Print', 'SpellChecker'],
		['Undo','Redo','-','Find','Replace','-','SelectAll','RemoveFormat'],
		['Bold','Italic','Underline','Strike','-','Subscript'],

		['NumberedList','BulletedList','-','Outdent','Indent','Blockquote'],
		['JustifyLeft','JustifyCenter','JustifyRight','JustifyBlock'],
		['Link','Unlink','Anchor'],

		['Image','Flash','Table','HorizontalRule','Smiley','SpecialChar'],
		['Font','FontSize'],
		['TextColor','BGColor', '-', 'Source']
	];
};
{% endhighlight %}

Agora é só testar. Crie um arquivo chamado "index.html" dentro da pasta do CKEditor com o seguinte conteúdo: 

{% highlight html %}
<body>
<head>
	<script type="text/javascript" src="ckeditor/ckeditor.js"></script>
	<script type="text/javascript" src="jquery-1.4.2.min.js"></script>
</head>
<body>
	<form method="post">  
		<textarea name="editor"></textarea>
		<script type="text/javascript">
			CKEDITOR.replace('editor');
		</script>
	</form>
</body>
</html>
{% endhighlight %}

Abra o index.html, digite alguma coisa no editor e clique no botão do canto esquerdo superior. Um alerta deverá ser mostrado, com o conteúdo enviado via AJAX.

**Download dos arquivos**

[Plugin Ajax Save](https://www.dropbox.com/s/i98z3yr77o8u6j1/AjaxSave.plugin.zip?dl=0)

[CKEditor, com jQuery 1.4.2 e plugin já integrado](https://www.dropbox.com/s/k38wrwn0mihnipn/ckeditor.zip?dl=0)

Abraço e até a próxima!