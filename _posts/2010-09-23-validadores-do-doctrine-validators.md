---
title: Validadores do Doctrine (validators)
date: 2010-09-23T08:48:24+00:00
author: fonini
layout: post
permalink: /2010/09/23/validadores-do-doctrine-validators/
categories:
  - Sem categoria
  - Web
tags:
  - Doctrine
  - PHP
---
Neste post mostrarei os validadores presentes no <a href="http://www.doctrine-project.org" rel="externo nofollow">Doctrine</a> (usei a versão 1.2.3). O Doctrine facilita a validação dos dados, bastando apenas definir os validadores para cada atributo ao invés de fazer vários malabarismos com funções do PHP e expressões regulares. Você pode definir os validadores na classe que estende a classe base. Dessa maneira, você pode gerar o model novamente e suas alterações não serão perdidas. Primeiro listarei os validadores e ao final mostrarei alguns exemplos. Vamos lá.

<span style="color: rgb(255, 0, 0);">**Importante**
	  
Para que seus dados sejam validados, cheque se seu "bootstrap.php" contém a diretiva abaixo. Caso contrário, seus dados não serão validados.

{% highlight php %}<?php
$manager->setAttribute(Doctrine_Core::ATTR_VALIDATE, Doctrine_Core::VALIDATE_ALL);
{% endhighlight %}

**notnull**

Garante que o valor não seja nulo na aplicação e no banco de dados.

{% highlight php %}<?php // models/SuaClasse.php

class SuaClasse extends BaseSuaClasse {
	// ...

	public function setTableDefinition(){
		parent::setTableDefinition();

		// ...

		$this->hasColumn('nome', 'string', 70, array(
			'notnull' => true
		));
	}
}
{% endhighlight %}

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>teste, jonnas
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>valores nulos 

**email**

Checa se o valor é um endereço de email válido.

{% highlight php %}<?php
$this->hasColumn('email', 'string', 100, array(				  
	'email' => true		  
)); 
{% endhighlight %}

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>contato@email.net
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>fulano!#@server 

**notblank**

Este validador é semelhante ao validador notnull, exceto que além de não validar valores nulos, também não valida strings vazias.

{% highlight php %}<?php
$this->hasColumn('nome', 'string', 100, array(				  
	'notblank' => true		  
)); 
{% endhighlight %}

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span> teste, jonnas
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span> valores nulos, " 

**nospace**

Checa se o valor não contém espaços.

{% highlight php %}<?php
$this->hasColumn('campo_sem_espacos', 'string', 100, array(				  
	'nospace' => true		  
)); 
{% endhighlight %}

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>JonnasFonini
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>Jonnas Fonini 

**past**

Checa se o valor é uma data que já ocorreu, o dia de ontem, por exemplo.

{% highlight php %}<?php
$this->hasColumn('data', 'timestamp', null, array(				  
	'past' => true		  
)); 
{% endhighlight %}

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>Sendo hoje 14/09/2010, 01/01/2010 é válida
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>Sendo hoje 14/09/2010, a mesma e posteriores são inválidas 

**future**

Checa se o valor é uma data que ainda não aconteceu, amanhã, por exemplo.

{% highlight php %}<?php
$this->hasColumn('data', 'timestamp', null, array(
	'future' => true		  
)); 
{% endhighlight %}

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>Sendo hoje 14/09/2010, 15/09/2010 é válida
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>Sendo hoje 14/09/2010, a mesma e anteriores são inválidas 

**minlength**

Checa se o valor passado tem o tamanho mínimo necessário.

{% highlight php %}<?php
$this->hasColumn('senha', 'string', 32, array(				  
	'minlength' => 6		  
)); 
{% endhighlight %}

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>abcdef, abcdefg
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>abc 

**ip**

Checa se o valor passado é um endereço IP válido.

{% highlight php %}<?php
$this->hasColumn('endereco_ip', 'string', 15, array(				  
	'ip' => true		  
)); 
{% endhighlight %}

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>192.168.250.222, 201.10.34.21
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>345.10.10.290 

**htmlcolor**

Checa se o valor passado é uma cor HTML em hexadecimal.

{% highlight php %}<?php
$this->hasColumn('cor', 'string', 7, array(				  
	'htmlcolor' => true		  
)); 
{% endhighlight %}

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>#000FFF, FF0000
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>#GGG111, #FFF (cores abreviadas são inválidas) 

**range**
	  
Checa se o valor numérico está contido no intervalo especificado.

{% highlight php %}<?php
$this->hasColumn('idade', 'integer', null, array(
	'range' => array(18, 70)			  
));
{% endhighlight %}

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>19, 50, 69
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>10, 18, 70 

**unique**
	  
Checa se o valor já existe no banco de dados.

{% highlight php %}<?php
$this->hasColumn('rg', 'string', 15, array(				  
	'unique' => true
));  
{% endhighlight %}

**regexp**

Checa se o valor casa com a expressão regular passada.

{% highlight php %}<?php
$this->hasColumn('somente_letras', 'string', 15, array(				  
	'regexp' => '/^[a-zA-Z]+$/'		  
));
{% endhighlight %}

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>flex
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>flex4 

**creditcard**

Checa se o valor é um número de cartão de crédito válido.

{% highlight php %}<?php
$this->hasColumn('cartao', 'integer', 16, array(				  
	'creditcard' => true
)); 
{% endhighlight %}

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>Cartões Visa, Master Card, American Express, Discover e Diners
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>Outras bandeiras, exceto as citadas acima 

**readonly**
	  
Evita que o valor de uma coluna da tabela seja alterado.

{% highlight php %}<?php
$this->hasColumn('coluna_que_nao_pode_ser_alterada', 'string', 25, array(				  
	'readonly' => true
));  
{% endhighlight %}

**unsigned**

Checa se o valor númerico passado possui sinal, de menos, por exemplo.

{% highlight php %}<?php
$this->hasColumn('idade', 'integer', 3, array(
	'unsigned' => true		  
)); 
{% endhighlight %}

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>70, 100
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>-20 

**usstate**

Checa se a string passada é a sigla válida de um estado americano. Confira a lista completa <a href="http://en.wikipedia.org/wiki/Us_states" rel="externo nofollow">aqui</a>.

{% highlight php %}<?php
$this->hasColumn('estado_americano', 'string', 2, array(				  
	'usstate' => true		  
));
{% endhighlight %}

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>AL, CA
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>QW 

**country**

Checa se a string passada é a sigla válida de um país. Confira a lista completa <a href="http://en.wikipedia.org/wiki/ISO_3166-1" rel="externo nofollow">aqui</a>.

{% highlight php %}<?php
$this->hasColumn('pais', 'string', 2, array(				  
	'country' => true
));  
{% endhighlight %}

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>br, BR, ar
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>xx

Grande abraço e até a próxima!