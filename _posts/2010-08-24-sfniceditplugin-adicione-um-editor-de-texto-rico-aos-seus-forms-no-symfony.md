---
id: 116
title: 'sfNicEditPlugin: Adicione um editor de texto rico aos seus forms no Symfony'
date: 2010-08-24T10:11:30+00:00
author: fonini
layout: post
permalink: /2010/08/24/sfniceditplugin-adicione-um-editor-de-texto-rico-aos-seus-forms-no-symfony/
categories:
  - Sem categoria
  - Web
tags:
  - PHP
  - Plugins
  - Symfony
---
Em meados de 2009 usei o framework Symfony para desenvolver um sistema em PHP para um projeto do qual eu era bolsista. Terminado o projeto, abandonei o framework. Agora reiniciei meus estudos e estou gostando bastante. Tanto que já desenvolvi meu primeiro plugin para compartilhar com a comunidade e já tenho muitos outros em mente.

O nome do plugin é sfNicEditPlugin. Ele adiciona uma instância do editor de texto rico <a href="http://www.nicedit.com" rel="externo nofollow">NicEdit</a> a um textarea. Esta é a primeira versão do plugin, ainda faltam alguns parâmetros que o NicEdit aceita, outros já estão disponíveis.

Você pode encontrar o plugin no meu <a href="http://github.com/fonini/sfNicEditPlugin" rel="externo nofollow">GitHub</a> ou na <a href="http://www.symfony-project.org/plugins/sfNicEditPlugin" rel="externo nofollow">página de plugins do Symfony</a>. Em ambos os locais você encontra instruções de instalação em inglês. Aqui no blog vou publicar a versão em português.

**Instalação**  

***Instalação (via pacote PEAR)***

{% highlight shell %}symfony plugin:install sfNicEditPlugin{% endhighlight %}

Instalação via Git

{% highlight shell %}git clone git://github.com/fonini/sfNicEditPlugin.git{% endhighlight %}

Ou baixe o plugin <a href="http://plugins.symfony-project.org/get/sfNicEditPlugin/sfNicEditPlugin-1.0.1.tgz" rel="nofollow externo">aqui</a> e extraia para a pasta plugins.

Você deve ativar o plugin, editando o arquivo config/ProjectConfiguration.class.php.

{% highlight php %}<?php  
class ProjectConfiguration extends sfProjectConfiguration{
	public function setup(){
		$this->enablePlugins(array('sfDoctrinePlugin', 'sfNicEditPlugin', '...;'));
	}
}
{% endhighlight %}

Após ativar o plugin, você deve publicar os arquivos CSS e JS utilizados por ele. Rode o seguinte comando:

{% highlight shell %}symfony plugin:publish-assets{% endhighlight %}

Por último, limpe o cache:

{% highlight shell %}symfony cc{% endhighlight %}



**Usando o widget**

Basta você editar a classe que gera o form em que você vai usar o NicEdit, por exemplo lib/form/doctrine/NewsForm.class.php.

{% highlight php %}<?php
public function configure(){
	$this->setWidget('text', new sfWidgetFormTextareaNicEdit(array('fullPanel' => true), array('cols' => 100, 'rows' => 20)));
}
{% endhighlight %}

Pretendo disponibilizar uma nova versão em breve com todos os parâmetros de configuração disponíves no NicEdit. Entre em contato em caso de dúvida. Abraço!