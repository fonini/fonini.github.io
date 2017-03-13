---
id: 124
title: Desenvolvendo um módulo de contato no Symfony 1.4
date: 2010-10-08T08:35:11+00:00
author: fonini
layout: post
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

{% highlight shell %}./symfony generate:module frontend contato{% endhighlight %}

O comando acima cria um módulo vazio, localizado em **apps/frontend/modules/contato**.
O próximo passo é criar a classe do formulário. Esta classe irá conter todos os widgets (entenda por inputs, textareas, selects) que irão compor o formulário.

Crie um arquivo chamado ContatoForm.class.php em lib/form, com o conteúdo abaixo:

{% highlight php %}<?php // lib/form/ContatoForm.class.php

class ContactForm extends BaseForm {
	public function configure(){
		$this->setWidgets(array(
			'nome' => new sfWidgetFormInputText(),
			'email' => new sfWidgetFormInputText(),
			'assunto' => new sfWidgetFormInputText(),
			'mensagem' => new sfWidgetFormTextarea(),
		));

		$this->widgetSchema->setLabels(array(
			'nome' => 'Nome',
			'email' => 'Email',
			'assunto' => 'Assunto',
			'mensagem' => 'Mensagem'
		));

		$this->setValidators(array(
			'nome' => new sfValidatorString(array('required' => true)),
			'email' => new sfValidatorEmail(),
			'assunto' => new sfValidatorString(array('required' => true)),
			'mensagem' => new sfValidatorString(array('min_length' => 10)),
		));

		// Se esta opção não for setada, serão geradas tabelas no HTML
		$this->widgetSchema->setFormFormatterName('list');

		$this->widgetSchema->setNameFormat('contato[%s]');
	}
}
{% endhighlight %}

Com a classe do formulário pronta, basta passar uma instância dela para o template. Edite o arquivo apps/frontend/modules/contato/actions/actions.class.php e adapte-o para o código que segue:

{% highlight php %}<?php // apps/frontend/modules/contato/actions/actions.class.php
class contatoActions extends sfActions {
	public function executeIndex(sfWebRequest $request){
		$this->form = new ContatoForm();

		if ($request->isMethod('post')){
			$this->form->bind($request->getParameter('contato'));

			if ($this->form->isValid()){
				$this->redirect('contato/enviar?'.http_build_query($this->form->getValues()));
			}
		}
	}
}
{% endhighlight %}

Agora definiremos o template que irá receber a instância da classe ContatoForm, gerando os campos do formulário.
Edite o arquivo apps/frontend/modules/contato/templates/indexSucess.php. Faço um parentêses aqui. Para cada action que você definir (no arquivo de actions, obviamente), você pode criar um arquivo nomedaactionSuccess.php. O conteúdo desse arquivo será exibido ao executar a action (a menos que ela redirecione para outra action). Exemplo: uma action enviaemail deve possuir um template enviaemailSuccess.php.

{% highlight html %} <!-- apps/frontend/modules/contato/templates/indexSuccess.php -->
<form action="<?php echo url_for('contato/index') ?>" method="post">
	<ul>
		<?php echo $form; ?>
		<li>
			<input type="submit" value="Enviar" />
		</li>
	</ul>
</form>
{% endhighlight %}

Você deve ter percebido que a action do formulário está apontando para contato/enviar. Ou seja, ao ser submetido, o método enviar da classe contatoActions será invocado, logo teremos que criá-lo. Volte para o arquivo apps/frontend/modules/contato/actions/actions.class.php e adicione os métodos abaixo, o método que enviará o email e o método que será chamado se o envio for bem sucedido. Mude as configurações para seu servidor de envio. Outros parâmetros na <a href="http://www.swiftmailer.org" rel="externo nofollow">documentação da Swift Mailer</a>.</p> 

{% highlight php %}<?php // apps/frontend/modules/contato/actions/actions.class.php
public function executeEnviar(sfWebRequest $request){

	$transport = Swift_SmtpTransport::newInstance('smtp.seudominio.com', 25)
		->setUsername('seuemail@dominio.com')
		->setPassword('senha');

	$mailer = Swift_Mailer::newInstance($transport);

	$message = Swift_Message::newInstance()
		->setSubject( $request->getParameter('assunto') )
		->setFrom(array( $request->getParameter('email') => $request->getParameter('nome') ))
		->setTo(array('email_contato@seudominio.com.br'))
		->setReplyTo( $request->;getParameter('email') )
		->setBody( $request->getParameter('mensagem') );

	if ($mailer->send($message)){
		$this->redirect('contato/feito');
	}
}

public function executeFeito(){
  
}
{% endhighlight %}

Agora basta criar um template para o método executeFeito, mostrando uma mensagem de envio bem sucedido.

{% highlight html %} <!-- apps/frontend/modules/contato/templates/feitoSuccess.php -->
<span style="font-weight: bold; font-size: 14px;">Contato enviado com sucesso. Obrigado!</span>
{% endhighlight %}

Tudo pronto! Teste seu módulo agora: 

{% highlight shell %}
http://localhost/seuprojeto/index.php/contato.
{% endhighlight %}

**Download**

Caso algo tenha dado errado, baixe os arquivos utilizados e coloque-os em suas devidas pastas. Melhor ainda que substituir os arquivos é tentar encontrar a causa do problema e quem sabe melhorar o módulo, que está bem básico.

[Download dos arquivos](https://www.dropbox.com/s/t08161cjvovmaow/modulo-contato-symfony.zip?dl=0)

Grande abraço e até a próxima!