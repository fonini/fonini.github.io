---
id: 89
title: Plugin para inserir vídeos do YouTube no CKEditor
date: 2010-03-25T08:55:17+00:00
author: fonini
layout: post
guid: http://www.fonini.net/blog/?p=89
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

<span style="font-size: 14px;"><strong><br />Instalação<br /></strong></span>

Baixe o <a href="http://www.ckeditor.com" rel="externo nofollow">CKEditor</a>, extraia para alguma pasta, baixe o [Plugin](http://www.fonini.net/labs/ckeditor-youtube.zip) e extraia para a pasta plugins do CKEditor. Feito isso, você deve informar ao sistema para usar esse plugin. No arquivo &#8220;config.js&#8221;, localizado na pasta do CKEditor, adicione a seguinte linha:</p> 

[js]
  
config.extraPlugins = "youtube";
  
[/js]

Você também deve adicionar o botão do plugin na barra de ferramentas do programa. Veja um exemplo:</p> 

[js]
  
config.toolbar = [
	  
[&#8216;Preview&#8217;],
	  
[&#8216;Cut&#8217;, &#8216;Copy&#8217;, &#8216;Paste&#8217;, &#8216;PasteText&#8217;, &#8216;PasteFromWord&#8217;, &#8216;-&#8216;, &#8216;Print&#8217;, &#8216;SpellChecker&#8217;],
	  
[&#8216;Undo&#8217;,&#8217;Redo&#8217;,&#8217;-&#8216;,&#8217;Find&#8217;,&#8217;Replace&#8217;,&#8217;-&#8216;,&#8217;SelectAll&#8217;,&#8217;RemoveFormat&#8217;],
	  
[&#8216;Bold&#8217;,&#8217;Italic&#8217;,&#8217;Underline&#8217;,&#8217;Strike&#8217;,&#8217;-&#8216;,&#8217;Subscript&#8217;,&#8217;Superscript&#8217;],
	  
[&#8216;NumberedList&#8217;,&#8217;BulletedList&#8217;,&#8217;-&#8216;,&#8217;Outdent&#8217;,&#8217;Indent&#8217;,&#8217;Blockquote&#8217;],
	  
[&#8216;JustifyLeft&#8217;,&#8217;JustifyCenter&#8217;,&#8217;JustifyRight&#8217;,&#8217;JustifyBlock&#8217;],
	  
[&#8216;Link&#8217;,&#8217;Unlink&#8217;,&#8217;Anchor&#8217;], [&#8216;Image&#8217;,&#8217;Flash&#8217;,&#8217;Table&#8217;,&#8217;HorizontalRule&#8217;,&#8217;Smiley&#8217;,&#8217;SpecialChar&#8217;],
	  
[&#8216;Font&#8217;,&#8217;FontSize&#8217;],
	  
[&#8216;TextColor&#8217;,&#8217;BGColor&#8217;, &#8216;-&#8216;, &#8216;Source&#8217;, &#8216;YouTube&#8217;]
  
];
  
[/js]

<span style="font-size: 14px;"><strong><br />Código<br /></strong></span>

[js]
  
CKEDITOR.dialog.add( &#8216;youtube&#8217;, function( editor )
  
{
	  
return {
		  
title : &#8216;Inserir vídeo do YouTube&#8217;,
		  
minWidth : 390,
		  
minHeight : 230,
		  
contents : [
		  
{
			  
id : &#8216;urlTab&#8217;,
			  
label : &#8216;URL do Vídeo&#8217;,
			  
title : &#8216;URL do Vídeo&#8217;,
			  
elements :
			  
[
				  
{
					  
id : &#8216;url&#8217;,
					  
type : &#8216;text&#8217;,
					  
label : &#8216;Cole a URL do vídeo do YouTube&#8217;
				  
},
				  
{
					  
id : &#8216;xhtml&#8217;,
					  
type : &#8216;checkbox&#8217;,
					  
label : &#8216;XHTML válido&#8217;
				  
},
				  
{
					  
id : &#8216;width&#8217;,
					  
type : &#8216;text&#8217;,
					  
label : &#8216;Largura&#8217;,
					  
width : &#8217;40&#8217;
				  
},
				  
{
					  
id : &#8216;height&#8217;,
					  
type : &#8216;text&#8217;,
					  
label : &#8216;Altura&#8217;,
					  
width : &#8217;40&#8217;
				  
}
			  
]
		  
},
		  
{
			  
id : &#8216;embedTab&#8217;,
			  
label : &#8216;Código Embed&#8217;,
			  
title : &#8216;Código Embed&#8217;,
			  
elements :
			  
[
				  
{
					  
id : &#8216;embed&#8217;,
					  
type : &#8216;textarea&#8217;,
					  
label : &#8216;Cole o código gerado pelo YouTube (embed)&#8217;
				  
}
			  
]
		  
}
          
],
		  
onOk : function() {
			  
var editor = this.getParentEditor();
			  
var contentUrl = this.getValueOf( &#8216;urlTab&#8217;, &#8216;url&#8217; );
			  
var contentEmbed = this.getValueOf( &#8216;embedTab&#8217;, &#8216;embed&#8217; );
			  
var xhtml = this.getValueOf( &#8216;urlTab&#8217;, &#8216;xhtml&#8217; );
			  
var width = this.getValueOf( &#8216;urlTab&#8217;, &#8216;width&#8217; );
			  
var height = this.getValueOf( &#8216;urlTab&#8217;, &#8216;height&#8217; );

width = width ? width : 450;
			  
height = height ? height : 366;

if ( contentUrl.length > 0 ) {
				  
if (xhtml == true){
					  
contentUrl = contentUrl.replace(/^[^v]+v.(.{11}).*/,"$1");
					  
editor.insertHtml(&#8216;<object type="application/x-shockwave-flash" style="width:&#8217; + width + &#8216;px; height:&#8217; + height + &#8216;px;" data="http://www.youtube.com/v/&#8217;+contentUrl+&#8217;"><param name="movie" value="http://www.youtube.com/v/&#8217;+contentUrl+&#8217;" /></object>&#8217;);
				  
}
				  
else {
					  
contentUrl = contentUrl.replace(/^[^v]+v.(.{11}).*/, "$1");
					  
editor.insertHtml(&#8216;<object width="&#8217; + width + &#8216;" height="&#8217; + height + &#8216;"><param name="movie" value="http://www.youtube.com/v/&#8217;+contentUrl+&#8217;"></param><param name="allowFullScreen" value="true"></param><param name="allowscriptaccess" value="always"></param><embed src="http://www.youtube.com/v/&#8217;+contentUrl+&#8217;" type="application/x-shockwave-flash" allowscriptaccess="always" allowfullscreen="true" width="&#8217; + width + &#8216;" height="&#8217; + height + &#8216;"></embed></object>&#8217;);
				  
}
			  
}
			  
else
			  
if ( contentEmbed.length > 0 ) {
				  
editor.insertHtml(contentEmbed);
			  
}
		  
},
	  
buttons : [ CKEDITOR.dialog.okButton, CKEDITOR.dialog.cancelButton ]
	  
};

} );

CKEDITOR.plugins.add( &#8216;youtube&#8217;,
  
{
	  
init : function( editor )
	  
{
		  
var command = editor.addCommand( &#8216;youtube&#8217;, new CKEDITOR.dialogCommand( &#8216;youtube&#8217; ) );
		  
command.modes = { wysiwyg:1, source:1 };
		  
command.canUndo = false;

editor.ui.addButton( &#8216;YouTube&#8217;,
		  
{
			  
label : &#8216;Inserir vídeo do YouTube&#8217;,
			  
command : &#8216;youtube&#8217;,
			  
icon : this.path + &#8216;youtube.png&#8217;
		  
});

CKEDITOR.dialog.add( &#8216;youtube&#8217;, &#8216;youtube&#8217; );
	  
}
  
});
  
[/js]

<span style="font-size: 14px;"><strong><br />Demo<br /></strong></span>

Você pode ver um demo do sistema funcionando clicando <a href="http://www.fonini.net/labs/ckeditor" rel="externo nofollow">aqui</a>.

Abraço e até a próxima!