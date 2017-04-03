---
title: Enviando emails autenticados do Gmail com PHP usando Swift Mailer
date: 2010-09-30T08:42:41+00:00
author: fonini
layout: post
permalink: /2010/09/30/enviando-emails-autenticados-do-gmail-com-php-usando-swift-mailer/
tags:
  - PHP
---
O <a href="http://www.swiftmailer.org" rel="externo nofollow">Swift Mailer</a> é uma biblioteca para envio de emails, usando PHP5. Conheci a biblioteca inicialmente no framework <a href="http://www.symfony-project.org" rel="externo nofollow">Symfony</a>, pois a mesma é responsável pela tarefa de enviar emails no framework, pois seu uso é muito simples e a biblioteca é muito poderosa.

Tenho notado que muitas empresas estão adotando cada vez mais o uso do Google Apps como serviço de webmail, dada a facilidade de uso e configuração do sistema. O primeiro exemplo mostra como enviar emails autenticados a partir de uma conta de email do Google (Gmail ou Apps) e os outros tratam do envio de mensagens com anexo. Usei a versão 4.0.6 para o exemplo.

**Enviando emails com autenticação no Gmail (incluindo Google Apps)**

{% highlight php %}<?php
require('lib/swift_required.php');

$transport = Swift_SmtpTransport::newInstance('smtp.gmail.com', 465, 'ssl')	  
->setUsername('usuario@gmail.com')
->setPassword('senha');

$mailer = Swift_Mailer::newInstance($transport);

$message = Swift_Message::newInstance('Assunto')
->setFrom(array('seuemail@dominio.com.br' => 'Seu Nome'))
->setTo(array('fulano@teste.com.br'))
->setReplyTo('seuemail@dominio.com.br')
->setBody('Conteudo da mensagem');

if ($mailer->send($message)){
	echo 'Mensagem enviada com sucesso';
}
else{	  
	echo 'Problema ao enviar mensagem. Tente novamente mais tarde';
}
{% endhighlight %}

**Enviando emails com imagens embutidas (inline)**

Útil para enviar emails com imagens que não serão bloqueadas pelos softwares leitores de email, já que estão embutidas no código e não em servidores remotos.

{% highlight php %}<?php
require('lib/swift_required.php');

$transport = Swift_SmtpTransport::newInstance('smtp.gmail.com', 465, 'ssl')	  
->setUsername('usuario@gmail.com')
->setPassword('senha');

$mailer = Swift_Mailer::newInstance($transport);

$message = Swift_Message::newInstance('Assunto')
->setFrom(array('seuemail@dominio.com.br' => 'Seu Nome'))
->setTo(array('fulano@teste.com.br'))
->setReplyTo('seuemail@dominio.com.br');

$imagem_inline = $message->embed(Swift_Image::fromPath('logotipo.png'));

$message->setBody(
	'<html>'.  
	' <head></head>'.
	' <body>' .
	' <img src="'.$imagem_inline.'" alt="Imagem embutida na mensagem" />'.
	' <br /><br />Texto da mensagem'.
	' </body>'.  
	'</html>',
	'text/html' //Definimos o tipo da mensagem para text/html, ao invés de texto puro
);

if ($mailer->send($message)){
	echo 'Mensagem enviada com sucesso';
}
else{	  
	echo 'Problema ao enviar mensagem. Tente novamente mais tarde';
}
{% endhighlight %}

**Enviando emails com anexo**

{% highlight php %}<?php
require('lib/swift_required.php)';

$transport = Swift_SmtpTransport::newInstance('smtp.seudominio.com', 25)	  
->setUsername('seuemail@dominio.com')
->setPassword('senha');

$mailer = Swift_Mailer::newInstance($transport);

$message = Swift_Message::newInstance()
->setSubject('Email com PDF anexado')
->setFrom(array('seuemail@seudominio.com' => 'Seu nome'))
->setTo(array('contato1@teste.org', 'contato2@teste.org'))
->setBody('Leia a apostila em anexo')
->attach(Swift_Attachment::fromPath('apostilas/apostila_inicial.pdf'));

if ($mailer->send($message)){
	echo 'Mensagem enviada com sucesso';
}
else{	  
	echo 'Problema ao enviar mensagem. Tente novamente mais tarde';
}
{% endhighlight %}

Bom, esses foram alguns exemplos bem básicos do uso da biblioteca Swift Mailer. Consulte a <a href="http://swiftmailer.org/docs/introduction" rel="externo nofollow">documentação oficial</a> para mais informações e um guia de referência completo.

Abraço e até a próxima!