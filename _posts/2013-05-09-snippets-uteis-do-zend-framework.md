---
id: 340
title: Snippets úteis do Zend Framework
date: 2013-05-09T10:30:50+00:00
author: fonini
layout: post
permalink: /2013/05/09/snippets-uteis-do-zend-framework/
categories:
  - Sem categoria
  - Web
tags:
  - PHP
  - Zend Framework
---
Compartilho aqui alguns snippets e comandos úteis do Zend Framework, para referência futura e quem sabe ajudar alguém que precise.
  


#### Retornar o código de resposta 404 (Not found).

{% highlight php %} $this->_response->clearBody()->clearHeaders()->setHttpResponseCode(404)->sendResponse(); {% endhighlight %}



#### Redirecionar para URL com âncora (sharp/cerquilha/jogo da velha)

{% highlight php %}<?php
$opt = array('module' => 'admin', 'controller' => 'galeria', 'action' => 'editar', 'id' => 1); $url = $this->_helper->getHelper('Url')->url($opt); $url .= "#descricao"; $this->_helper->redirector->gotoUrl($url); {% endhighlight %}



#### Trocar o layout no controller

{% highlight php %}<?php
$this->_helper->layout->setLayout('servicos'); {% endhighlight %}



#### Timestamp no formato de banco de dados

{% highlight php %}<?php
Zend_Date::now()->toString('yyyy-MM-dd HH:mm:ss'); {% endhighlight %}



#### Desabilitar layout

{% highlight php %}<?php
$this->_helper->layout()->disableLayout(); {% endhighlight %}



#### Desabilitar renderização da view

{% highlight php %}<?php
$this->_helper->viewRenderer->setNoRender(true);{% endhighlight %}



#### Debugar consultas no banco de dados

{% highlight php %}<?php
$db = Zend_Db_Table::getDefaultAdapter(); $profiler = $db->getProfiler()->setEnabled(true); print_r($profiler->getLastQueryProfile()); {% endhighlight %}



#### Dados do usuário logado (caso esteja usando Zend_Auth)

{% highlight php %}<?php
Zend_Auth::getInstance()->getIdentity();{% endhighlight %}



#### Utilizando transações: 

{% highlight php %}<?php
$db = Zend_Db_Table::getDefaultAdapter();

try{
	$db->beginTransaction();

	// query

	$db->commit();
}
catch (Exception $e){	  
	$db->rollBack();
}
{% endhighlight %}