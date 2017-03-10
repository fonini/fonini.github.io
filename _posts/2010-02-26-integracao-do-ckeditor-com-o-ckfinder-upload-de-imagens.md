---
id: 68
title: Integração do CKEditor com o CKFinder (upload de imagens)
date: 2010-02-26T09:02:58+00:00
author: fonini
layout: post
guid: http://www.fonini.net/blog/?p=68
permalink: /2010/02/26/integracao-do-ckeditor-com-o-ckfinder-upload-de-imagens/
categories:
  - Sem categoria
  - Web
tags:
  - CKEditor
  - Java Script
  - Plugins
---
Na minha &#8220;carreira&#8221; de desenvolvedor já testei 3 editores WYSWYG (What You See, What You Get) baseados em JavaScript. O primeiro foi o NicEdit, extremamente leve, mas os clientes reclamavam da falta de recursos. Mudei para o TinyMCE. Novamente encontraram problemas, desta vez foi com as imagens. Segundo eles. era muito complicado inserir uma imagem. Finalmente mudei para o CKEditor. Pesado, trocentos arquivos, mas com a tão sonhada funcionalidade de upload de imagens, quando integrado com o CKFinder. O CKFinder permite que você faça upload de imagens e outros arquivos, inserindo-os no CKEditor. Também fornece uma página, onde é possível navegar entre os arquivos escolhidos e alterar várias opções.

O objetivo deste post é ensinar como integrar o CKEditor com o CKFinder.

Baixe o <a href="http://www.ckeditor.com" rel="externo">CKEditor</a> e extraia em alguma pasta.
  
Baixe o <a href="http://www.ckfinder.com" rel="externo">CKFinder</a> e extraia dentro da pasta que você extraiu o CKEditor. Eu estou usando a versão para PHP

Agora, vá até a pasta do CKFinder e edite o arquivo &#8220;config.php&#8221;. A primeira função do arquivo, CheckAuthentication(), deve retornar true para que você possa acessar o painel do CKFinder. Porém, se ela sempre retornar true, qualquer um poderá acessar e modificar suas imagens. A solução, no meu caso, foi usar a própria sessão do usuário para autenticar no CKFinder. Mais ou menos assim:</p> 

[php]
  
function CheckAuthentication() {
	  
if (!empty($_SESSION[&#8216;usuario&#8217;]))
		  
return true;
	  
return false;
  
}
  
[/php]

Para anexar o CKFinder com o CKEditor temos duas opções: no próprio arquivo (HTML, PHP) que vai conter o editor ou no arquivo de configuração do CKEditor, config.js.

No caso de configurar no próprio código:</p> 

[js]
  
CKEDITOR.replace( &#8216;editor&#8217;,{
	  
filebrowserBrowseUrl : &#8216;ckeditor/ckfinder/ckfinder.html&#8217;,
	  
filebrowserImageBrowseUrl : &#8216;ckeditor/ckfinder/ckfinder.html?type=Images&#8217;,
	  
filebrowserFlashBrowseUrl : &#8216;ckeditor/ckfinder/ckfinder.html?type=Flash&#8217;,
	  
filebrowserUploadUrl : &#8216;ckeditor/ckfinder/core/connector/php/connector.php?command=QuickUpload&type=Files&#8217;,
	  
filebrowserImageUploadUrl : &#8216;ckeditor/ckfinder/core/connector/php/connector.php?command=QuickUpload&type=Images&#8217;,
	  
filebrowserFlashUploadUrl : &#8216;ckeditor/ckfinder/core/connector/php/connector.php?command=QuickUpload&type=Flash&#8217;
  
}
  
;);
  
[/js]

Usando o config.js da pasta do CKEditor:</p> 

[js]
  
CKEDITOR.editorConfig = function( config ){
	  
config.filebrowserBrowseUrl = &#8216;ckeditor/ckfinder/ckfinder.html&#8217;,
	  
config.filebrowserImageBrowseUrl = &#8216;ckeditor/ckfinder/ckfinder.html?type=Images&#8217;,
	  
config.filebrowserFlashBrowseUrl = &#8216;ckeditor/ckfinder/ckfinder.html?type=Flash&#8217;,
	  
config.filebrowserUploadUrl = &#8216;ckeditor/ckfinder/core/connector/php/connector.php?command=QuickUpload&type=Files&#8217;,
	  
config.filebrowserImageUploadUrl = &#8216;ckeditor/ckfinder/core/connector/php/connector.php?command=QuickUpload&type=Images&#8217;,
	  
config.filebrowserFlashUploadUrl = &#8216;ckeditor/ckfinder/core/connector/php/connector.php?command=QuickUpload&type=Flash&#8217;
  
};
  
[/js]

O sistema está pronto. Na configuração padrão, o CKFinder armazena as imagens do upload na raíz do servidor, pasta ckfinder/userfiles/. Essa pasta deve ter permissão 777 para que funcione corretamente. Esse caminho pode ser mudado no arquivo &#8220;config.php&#8221; da pasta do CKFinder.

Após a instalação, o CKFinder fica disponível no botão &#8220;Figura&#8221; do CKEditor. Clicando nesse botão e indo até a aba &#8220;Submeter&#8221;, você poderá realizar o upload das suas imagens. Clicando em &#8220;Localizar no servidor&#8221;, você poderá usar as imagens já upadas.

Abraço e até a próxima!</p>