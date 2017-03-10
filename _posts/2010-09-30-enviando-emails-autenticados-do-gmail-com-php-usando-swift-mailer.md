---
id: 122
title: Enviando emails autenticados do Gmail com PHP usando Swift Mailer
date: 2010-09-30T08:42:41+00:00
author: fonini
layout: post
guid: http://www.fonini.net/blog/?p=122
permalink: /2010/09/30/enviando-emails-autenticados-do-gmail-com-php-usando-swift-mailer/
categories:
  - Sem categoria
  - Web
tags:
  - PHP
---
O <a href="http://www.swiftmailer.org" rel="externo nofollow">Swift Mailer</a> é uma biblioteca para envio de emails, usando PHP5. Conheci a biblioteca inicialmente no framework <a href="http://www.symfony-project.org" rel="externo nofollow">Symfony</a>, pois a mesma é responsável pela tarefa de enviar emails no framework, pois seu uso é muito simples e a biblioteca é muito poderosa.

Tenho notado que muitas empresas estão adotando cada vez mais o uso do Google Apps como serviço de webmail, dada a facilidade de uso e configuração do sistema. O primeiro exemplo mostra como enviar emails autenticados a partir de uma conta de email do Google (Gmail ou Apps) e os outros tratam do envio de mensagens com anexo. Usei a versão 4.0.6 para o exemplo.

<span style="font-size: 14px;"><strong>Enviando emails com autenticação no Gmail (incluindo Google Apps)</strong></span>

[php]require(&#8216;lib/swift_required.php&#8217;);

$transport = Swift_SmtpTransport::newInstance(&#8216;smtp.gmail.com&#8217;, 465, &#8216;ssl&#8217;)
	  
->setUsername(&#8216;usuario@gmail.com&#8217;)
	  
->setPassword(&#8216;senha&#8217;);

$mailer = Swift_Mailer::newInstance($transport);

$message = Swift_Message::newInstance(&#8216;Assunto&#8217;)
	  
->setFrom(array(&#8216;seuemail@dominio.com.br&#8217; => &#8216;Seu Nome&#8217;))
	  
->setTo(array(&#8216;fulano@teste.com.br&#8217;))
	  
->setReplyTo(&#8216;seuemail@dominio.com.br&#8217;)
	  
->setBody(&#8216;Conteudo da mensagem&#8217;);

if ($mailer->send($message)){
	  
echo &#8216;Mensagem enviada com sucesso&#8217;;
  
}
  
else{
	  
echo &#8216;Problema ao enviar mensagem. Tente novamente mais tarde&#8217;;
  
}
  
[/php]

<span style="font-size: 14px;"><br /> <strong>Enviando emails com imagens embutidas (inline)</strong></span>
  
Útil para enviar emails com imagens que não serão bloqueadas pelos softwares leitores de email, já que estão embutidas no código e não em servidores remotos.

[php]require(&#8216;lib/swift_required.php&#8217;);

$transport = Swift_SmtpTransport::newInstance(&#8216;smtp.gmail.com&#8217;, 465, &#8216;ssl&#8217;)
	  
->setUsername(&#8216;usuario@gmail.com&#8217;)
	  
->setPassword(&#8216;senha&#8217;);

$mailer = Swift_Mailer::newInstance($transport);

$message = Swift_Message::newInstance(&#8216;Assunto&#8217;)
	  
->setFrom(array(&#8216;seuemail@dominio.com.br&#8217; => &#8216;Seu Nome&#8217;))
	  
->setTo(array(&#8216;fulano@teste.com.br&#8217;))
	  
->setReplyTo(&#8216;seuemail@dominio.com.br&#8217;);

$imagem\_inline = $message->embed(Swift\_Image::fromPath(&#8216;logotipo.png&#8217;));

$message->setBody(
	  
&#8216;<html>&#8217;.
	  
&#8216; <head></head>&#8217;.
	  
&#8216; <body>&#8217; .
	  
&#8216; <img src="&#8217;.$imagem_inline.&#8217;" alt="Imagem embutida na mensagem" />&#8217;.
	  
&#8216; <br /><br />Texto da mensagem&#8217;.
	  
&#8216; </body>&#8217;.
	  
&#8216;</html>&#8217;,
    
&#8216;text/html&#8217; //Definimos o tipo da mensagem para text/html, ao invés de texto puro
  
);

if ($mailer->send($message)){
	  
echo &#8216;Mensagem enviada com sucesso&#8217;;
  
}
  
else{
	  
echo &#8216;Problema ao enviar mensagem. Tente novamente mais tarde&#8217;;
  
}
  
[/php]

<span style="font-size: 14px;"><br /> <strong>Enviando emails com anexo</strong></span>

[php]require\_once &#8216;lib/swift\_required.php&#8217;;

$transport = Swift_SmtpTransport::newInstance(&#8216;smtp.seudominio.com&#8217;, 25)
	  
->setUsername(&#8216;seuemail@dominio.com&#8217;)
	  
->setPassword(&#8216;senha&#8217;);

$mailer = Swift_Mailer::newInstance($transport);

$message = Swift_Message::newInstance()
	  
->setSubject(&#8216;Email com PDF anexado&#8217;)
	  
->setFrom(array(&#8216;seuemail@seudominio.com&#8217; => &#8216;Seu nome&#8217;))
	  
->setTo(array(&#8216;contato1@teste.org&#8217;, &#8216;contato2@teste.org&#8217;))
	  
->setBody(&#8216;Leia a apostila em anexo&#8217;)
	  
->attach(Swift\_Attachment::fromPath(&#8216;apostilas/apostila\_inicial.pdf&#8217;));

if ( ! $mailer->send($message)){
	  
echo &#8216;Erro ao enviar email&#8217;;
  
}
  
[/php]

Bom, esses foram alguns exemplos bem básicos do uso da biblioteca Swift Mailer. Consulte a <a href="http://swiftmailer.org/docs/introduction" rel="externo nofollow">documentação oficial</a> para mais informações e um guia de referência completo.

Abraço e até a próxima!