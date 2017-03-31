---
title: Plugin para inserir vídeos do YouTube no CKEditor
date: 2010-03-25T08:55:17+00:00
author: fonini
layout: post
permalink: /2010/03/25/plugin-para-inserir-videos-do-youtube-no-ckeditor/
categories:
  - Sem categoria
  - Web
tags:
  - CKEditor
  - Java Script
  - Plugins
---
Depois de alguns dias sem postar em razão de muito trabalho, Curso de Java e 7 matérias na faculdade, estou de volta com mais um plugin para o CKEditor. Muitos usuários leigos não sabem como inserir um vídeo do YouTube no CKEditor, por não saberem manipular o código fonte do texto. Resolvi criar esse plugin para auxiliar nesta tarefa. Basta apenas colar a URL do vídeo ou o código embed gerado pelo YouTube e o sistema se encarrega do resto.

Também é possível gerar código XHTML válido ao inserir um vídeo via URL. Quando o código XHTML válido é gerado, não aparece nenhum elemento na tela indicando um vídeo, mas no código fonte sim. Estranho.

**Instalação**

Baixe o <a href="http://www.ckeditor.com" rel="externo nofollow">CKEditor</a>, extraia para alguma pasta, baixe o [Plugin](https://www.dropbox.com/s/05sfqp9xvcfvuo9/ckeditor-youtube.zip?dl=0) e extraia para a pasta plugins do CKEditor. Feito isso, você deve informar ao sistema para usar esse plugin. No arquivo "config.js", localizado na pasta do CKEditor, adicione a seguinte linha:

{% highlight js %}
config.extraPlugins = "youtube";
{% endhighlight %}

Você também deve adicionar o botão do plugin na barra de ferramentas do programa. Veja um exemplo:

{% highlight js %}
config.toolbar = [
	['Preview'],
	['Cut', 'Copy', 'Paste', 'PasteText', 'PasteFromWord', '-', 'Print', 'SpellChecker'],
	['Undo','Redo','-','Find','Replace','-','SelectAll','RemoveFormat'],
	['Bold','Italic','Underline','Strike','-','Subscript','Superscript'],
	['NumberedList','BulletedList','-','Outdent','Indent','Blockquote'],
	['JustifyLeft','JustifyCenter','JustifyRight','JustifyBlock'],
	['Link','Unlink','Anchor'], ['Image','Flash','Table','HorizontalRule','Smiley','SpecialChar'],
	['Font','FontSize'],
	['TextColor','BGColor', '-', 'Source', 'YouTube']
];
{% endhighlight %}

**Código**

{% highlight js %}
CKEDITOR.dialog.add( 'youtube', function( editor ){
	return {
		title : 'Inserir vídeo do YouTube',
		minWidth : 390,
		minHeight : 230,
		contents : [{
			id : 'urlTab',
			label : 'URL do Vídeo',
			title : 'URL do Vídeo',
			elements : [
				{
					id : 'url',
					type : 'text',
					label : 'Cole a URL do vídeo do YouTube'
				}, {
					id : 'xhtml',
					type : 'checkbox',
					label : 'XHTML válido'
				}, {
					id : 'width',
					type : 'text',
					label : 'Largura',
					width : '40'
				}, {
					id : 'height',
					type : 'text',
					label : 'Altura',
					width : '40'
				}
			]
		}, {
			id : 'embedTab',
			label : 'Código Embed',
			title : 'Código Embed',
			elements : [{
				id : 'embed',
				type : 'textarea',
				label : 'Cole o código gerado pelo YouTube (embed)'
			}]
		}],
		onOk : function() {
			var editor = this.getParentEditor();
			var contentUrl = this.getValueOf( 'urlTab', 'url' );

			var contentEmbed = this.getValueOf( 'embedTab', 'embed' );
			var xhtml = this.getValueOf( 'urlTab', 'xhtml' );

			var width = this.getValueOf( 'urlTab', 'width' );
			var height = this.getValueOf( 'urlTab', 'height' );

			width = width ? width : 450;
			height = height ? height : 366;

			if (contentUrl.length > 0) {
				if (xhtml == true){	
					contentUrl = contentUrl.replace(/^[^v]+v.(.{11}).*/,"$1");

					editor.insertHtml('<object type="application/x-shockwave-flash" style="width:' + width + 'px; height:' + height + 'px;" data="http://www.youtube.com/v/'+contentUrl+'"><param name="movie" value="http://www.youtube.com/v/'+contentUrl+'" /></object>');
				}
				else {
					contentUrl = contentUrl.replace(/^[^v]+v.(.{11}).*/, "$1");

					editor.insertHtml('<object width="' + width + '" height="' + height + '"><param name="movie" value="http://www.youtube.com/v/'+contentUrl+'"></param><param name="allowFullScreen" value="true"></param><param name="allowscriptaccess" value="always"></param><embed src="http://www.youtube.com/v/'+contentUrl+'" type="application/x-shockwave-flash" allowscriptaccess="always" allowfullscreen="true" width="' + width + '" height="' + height + '"></embed></object>');
				}
			}
			else
			if (contentEmbed.length > 0) {
				editor.insertHtml(contentEmbed);
			}
		},
		buttons : [ CKEDITOR.dialog.okButton, CKEDITOR.dialog.cancelButton ]
	};
});

CKEDITOR.plugins.add( 'youtube', {
	init : function( editor ) {
		var command = editor.addCommand( 'youtube', new CKEDITOR.dialogCommand( 'youtube' ) );
		command.modes = { wysiwyg:1, source:1 };
		command.canUndo = false;

		editor.ui.addButton( 'YouTube', {
			label : 'Inserir vídeo do YouTube',
			command : 'youtube',
			icon : this.path + 'youtube.png'
		});

		CKEDITOR.dialog.add( 'youtube', 'youtube' );
	}
});
{% endhighlight %}

Update:
Uma versão mais completa do [plugin](http://ckeditor.com/addon/youtube) está disponível no site do CKEditor.

Abraço e até a próxima!