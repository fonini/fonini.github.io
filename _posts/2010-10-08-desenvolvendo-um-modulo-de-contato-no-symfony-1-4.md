---
id: 124
title: Desenvolvendo um módulo de contato no Symfony 1.4
date: 2010-10-08T08:35:11+00:00
author: fonini
layout: post
guid: http://www.fonini.net/blog/?p=124
permalink: /2010/10/08/desenvolvendo-um-modulo-de-contato-no-symfony-1-4/
categories:
  - Sem categoria
  - Web
tags:
  - PHP
  - Symfony
---
Olá pessoal, o tutorial de hoje mostra como fazer um módulo com formulário de contato e envio dos dados por email usando o framework <a href="http://www.symfony-project.org" rel="nofollow externo">Symfony</a>. Você já deve possuir um projeto criado para poder proseeguir.

Primeiro, crie o módulo vazio com o comando abaixo:

<pre id="terminal" user="fonini" computer="valhalla">./symfony generate:module frontend contato</pre>

O comando acima cria um módulo vazio, localizado em **apps/frontend/modules/contato**. O próximo passo é criar a classe do formulário. Esta classe irá conter todos os widgets (entenda por inputs, textareas, selects) que irão compor o formulário.
	  
Crie um arquivo chamado ContatoForm.class.php em lib/form, com o conteúdo abaixo:

[php]// lib/form/ContatoForm.class.php
  
class ContactForm extends BaseForm
  
{
    
public function configure()
    
{
      
$this->setWidgets(array(
        
&#8216;nome&#8217; => new sfWidgetFormInputText(),
        
&#8216;email&#8217; => new sfWidgetFormInputText(),
        
&#8216;assunto&#8217; => new sfWidgetFormInputText(),
        
&#8216;mensagem&#8217; => new sfWidgetFormTextarea(),
      
));

$this->widgetSchema->setLabels(array(
        
&#8216;nome&#8217; => &#8216;Nome&#8217;,
        
&#8216;email&#8217; => &#8216;Email&#8217;,
        
&#8216;assunto&#8217; => &#8216;Assunto&#8217;,
        
&#8216;mensagem&#8217; => &#8216;Mensagem&#8217;
      
));

$this->setValidators(array(
        
&#8216;nome&#8217; => new sfValidatorString(array(&#8216;required&#8217; => true)),
        
&#8216;email&#8217; => new sfValidatorEmail(),
        
&#8216;assunto&#8217; => new sfValidatorString(array(&#8216;required&#8217; => true)),
        
&#8216;mensagem&#8217; => new sfValidatorString(array(&#8216;min_length&#8217; => 10)),
      
));

// se esta opção não for setada, serão geradas tabelas no HTML
      
$this->widgetSchema->setFormFormatterName(&#8216;list&#8217;);

$this->widgetSchema->setNameFormat(&#8216;contato[%s]&#8217;);
    
}
  
}
  
[/php]

Com a classe do formulário pronta, basta passar uma instância dela para o template. Edite o arquivo apps/frontend/modules/contato/actions/actions.class.php e adapte-o para o código que segue:

[php]// apps/frontend/modules/contato/actions/actions.class.php
  
class contatoActions extends sfActions
  
{
    
public function executeIndex(sfWebRequest $request)
    
{
      
$this->form = new ContatoForm();

if ($request->isMethod(&#8216;post&#8217;))
      
{
        
$this->form->bind($request->getParameter(&#8216;contato&#8217;));

if ($this->form->isValid())
        
{
          
$this->redirect(&#8216;contato/enviar?&#8217;.http\_build\_query($this->form->getValues()));
        
}
      
}
    
}
  
}
  
[/php]

Agora definiremos o template que irá receber a instância da classe ContatoForm, gerando os campos do formulário. Edite o arquivo apps/frontend/modules/contato/templates/indexSucess.php. Faço um parentêses aqui. Para cada action que você definir (no arquivo de actions, obviamente), você pode criar um arquivo nomedaactionSuccess.php. O conteúdo desse arquivo será exibido ao executar a action (a menos que ela redirecione para outra action). Exemplo: uma action enviaemail deve possuir um template enviaemailSuccess.php.

[html]// apps/frontend/modules/contato/templates/indexSuccess.php

<form action="<?php echo url_for(&#8216;contato/index&#8217;) ?>" method="post">
	  
<ul>
                  
<?php echo $form; ?>
		  
<li>
			  
<input type="submit" value="Enviar" />
                  
</li>
	  
</ul>
  
</form>
  
[/html]

Você deve ter percebido que a action do formulário está apontando para contato/enviar. Ou seja, ao ser submetido, o método enviar da classe contatoActions será invocado, logo teremos que criá-lo. Volte para o arquivo apps/frontend/modules/contato/actions/actions.class.php e adicione os métodos abaixo, o método que enviará o email e o método que será chamado se o envio for bem sucedido. Mude as configurações para seu servidor de envio. Outros parâmetros na <a href="http://www.swiftmailer.org" rel="externo nofollow">documentação da Swift Mailer</a>.</p> 

[php]// apps/frontend/modules/contato/actions/actions.class.php

public function executeEnviar(sfWebRequest $request)
  
{
    
$transport = Swift_SmtpTransport::newInstance(&#8216;smtp.seudominio.com&#8217;, 25)
      
->setUsername(&#8216;seuemail@dominio.com&#8217;)
      
->setPassword(&#8216;senha&#8217;);

$mailer = Swift_Mailer::newInstance($transport);

$message = Swift_Message::newInstance()
      
->setSubject( $request->getParameter(&#8216;assunto&#8217;) )
      
->setFrom(array( $request->getParameter(&#8216;email&#8217;) => $request->getParameter(&#8216;nome&#8217;) ))
      
->setTo(array(&#8216;email_contato@seudominio.com.br&#8217;))
      
->setReplyTo( $request->;getParameter(&#8216;email&#8217;) )
      
->setBody( $request->getParameter(&#8216;mensagem&#8217;) );

if ($mailer->send($message)){
      
$this->redirect(&#8216;contato/feito&#8217;);
    
}
  
}

public function executeFeito()
  
{
  
}
  
[/php]

Agora basta criar um template para o método executeFeito, mostrando uma mensagem de envio bem sucedido.

[html]<!&#8211; apps/frontend/modules/contato/templates/feitoSuccess.php &#8211;>
  
<span style="font-weight: bold; font-size: 14px;">Contato enviado com sucesso. Obrigado!</span>
  
[/html]

Tudo pronto! Teste seu módulo agora: http://localhost/seuprojeto/index.php/contato.

**Download**

Caso algo tenha dado errado, baixe os arquivos utilizados e coloque-os em suas devidas pastas. Melhor ainda que substituir os arquivos é tentar encontrar a causa do problema e quem sabe melhorar o módulo, que está bem básico.

[Download dos arquivos](http://www.fonini.net/labs/modulo-contato-symfony.zip)

Grande abraço e até a próxima!