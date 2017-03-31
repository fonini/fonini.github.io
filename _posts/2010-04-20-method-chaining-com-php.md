---
title: Method Chaining com PHP
date: 2010-04-20T08:18:49+00:00
author: fonini
layout: post
permalink: /2010/04/20/method-chaining-com-php/
categories:
  - Sem categoria
  - Web
tags:
  - PHP
---
Method Chaining (encadeamento de métodos) é uma técnica de programação que permite reduzir o tamanho de seus códigos. Em determinadas classes, você precisa chamar vários métodos diferentes em diversas linhas. Com method chaining, você poderá chamar esses métodos em cadeia, em somente uma linha. Por exemplo, veja a seguinte classe de formatação de strings:

{% highlight php %}<?php
class String {
	private $str;

	public function __construct($str){	  
		$this->str = $str;
	}

	public function toLower(){	  
		$this->str = strtolower($this->str);
	}

	public function capitalize(){	  
		$this->str = ucfirst($this->str);
	}

	public function bold(){	  
		$this->str = '<strong>'.$this->str.'</strong>';
	}

	public function getStr(){	  
		return $this->str;
	}
}

$string = new String("TEXTO DE EXEMPLO");

$string->toLower();
$string->capitalize();  
$string->bold();

echo $string->getStr();
{% endhighlight %}

Essa é forma que grande parte dos programadores escrevem seus códigos. Com method chaining, nossa classe ficaria assim:

{% highlight php %}<?php
class String{
	private $str;

	public function __construct($str){	  
		$this->str = $str;
	}

	public function toLower(){	  
		$this->str = strtolower($this->str);  
		return $this;
	}

	public function capitalize(){	  
		$this->str = ucfirst($this->str);  
		return $this;
	}

	public function bold(){	  
		$this->str = '<strong>'.$this->str.'</strong>';  
		return $this;
	}

	public function getStr(){
		return $this->str;
	}
}

$string = new String("TEXTO DE EXEMPLO");

echo $string->toLower()->capitalize()->bold()->getStr();
  
// Retorno: <strong>Texto de exemplo</strong>;  
{% endhighlight %}

Bem mais simples, não? A diferença da outra classe, é que você retorna a instância do objeto a cada método chamado, permitindo o encadeamento.

Bom, como você pode ver, essa classe praticamente não tem muita utilidade, mas permite ter uma boa visão de como funciona a técnica. Agora é com você.

Abraço e até a próxima!