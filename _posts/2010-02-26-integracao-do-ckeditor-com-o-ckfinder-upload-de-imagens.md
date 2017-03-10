---
id: 68
title: Integração do CKEditor com o CKFinder (upload de imagens)
date: 2010-02-26T09:02:58+00:00
author: fonini
layout: post
permalink: /2010/02/26/integracao-do-ckeditor-com-o-ckfinder-upload-de-imagens/
categories:
  - Sem categoria
  - Web
tags:
  - CKEditor
  - Java Script
  - Plugins
---
Na minha carreira de desenvolvedor já testei 3 editores WYSWYG (What You See, What You Get) baseados em JavaScript. O primeiro foi o NicEdit, extremamente leve, mas os clientes reclamavam da falta de recursos. Mudei para o TinyMCE. Novamente encontraram problemas, desta vez foi com as imagens. Segundo eles. era muito complicado inserir uma imagem. Finalmente mudei para o CKEditor. Pesado, trocentos arquivos, mas com a tão sonhada funcionalidade de upload de imagens, quando integrado com o CKFinder. O CKFinder permite que você faça upload de imagens e outros arquivos, inserindo-os no CKEditor. Também fornece uma página, onde é possível navegar entre os arquivos escolhidos e alterar várias opções.

O objetivo deste post é ensinar como integrar o CKEditor com o CKFinder.

Baixe o <a href="http://www.ckeditor.com" rel="externo">CKEditor</a> e extraia em alguma pasta.
  
Baixe o <a href="http://www.ckfinder.com" rel="externo">CKFinder</a> e extraia dentro da pasta que você extraiu o CKEditor. Eu estou usando a versão para PHP

Agora, vá até a pasta do CKFinder e edite o arquivo "config.php". A primeira função do arquivo, CheckAuthentication(), deve retornar true para que você possa acessar o painel do CKFinder. Porém, se ela sempre retornar true, qualquer um poderá acessar e modificar suas imagens. A solução, no meu caso, foi usar a própria sessão do usuário para autenticar no CKFinder. Mais ou menos assim: 

{% highlight php %}<?php
function CheckAuthentication() {
	if (!empty($_SESSION['usuario'])){
		return true;
	}

	return false;
}
{% endhighlight %}

Para anexar o CKFinder com o CKEditor temos duas opções: no próprio arquivo (HTML, PHP) que vai conter o editor ou no arquivo de configuração do CKEditor, config.js.

No caso de configurar no próprio código: 

{% highlight js %}
CKEDITOR.replace( 'editor', {
	filebrowserBrowseUrl : 'ckeditor/ckfinder/ckfinder.html',  
	filebrowserImageBrowseUrl : 'ckeditor/ckfinder/ckfinder.html?type=Images',  
	filebrowserFlashBrowseUrl : 'ckeditor/ckfinder/ckfinder.html?type=Flash',  
	filebrowserUploadUrl : 'ckeditor/ckfinder/core/connector/php/connector.php?command=QuickUpload&type=Files',  
	filebrowserImageUploadUrl : 'ckeditor/ckfinder/core/connector/php/connector.php?command=QuickUpload&type=Images',  
	filebrowserFlashUploadUrl : 'ckeditor/ckfinder/core/connector/php/connector.php?command=QuickUpload&type=Flash'
});
{% endhighlight %}

Usando o config.js da pasta do CKEditor: 

{% highlight js %}
CKEDITOR.editorConfig = function( config ){  
	config.filebrowserBrowseUrl = 'ckeditor/ckfinder/ckfinder.html',
	config.filebrowserImageBrowseUrl = 'ckeditor/ckfinder/ckfinder.html?type=Images',
	config.filebrowserFlashBrowseUrl = 'ckeditor/ckfinder/ckfinder.html?type=Flash',
	config.filebrowserUploadUrl = 'ckeditor/ckfinder/core/connector/php/connector.php?command=QuickUpload&type=Files',
	config.filebrowserImageUploadUrl = 'ckeditor/ckfinder/core/connector/php/connector.php?command=QuickUpload&type=Images',
	config.filebrowserFlashUploadUrl = 'ckeditor/ckfinder/core/connector/php/connector.php?command=QuickUpload&type=Flash'
};
{% endhighlight %}

O sistema está pronto. Na configuração padrão, o CKFinder armazena as imagens do upload na raíz do servidor, pasta ckfinder/userfiles/. Essa pasta deve ter permissão 777 para que funcione corretamente. Esse caminho pode ser mudado no arquivo "config.php" da pasta do CKFinder.

Após a instalação, o CKFinder fica disponível no botão "Figura" do CKEditor. Clicando nesse botão e indo até a aba "Submeter", você poderá realizar o upload das suas imagens. Clicando em "Localizar no servidor", você poderá usar as imagens já upadas.

Abraço e até a próxima!