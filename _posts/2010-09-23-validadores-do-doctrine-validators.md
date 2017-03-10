---
id: 120
title: Validadores do Doctrine (validators)
date: 2010-09-23T08:48:24+00:00
author: fonini
layout: post
guid: http://www.fonini.net/blog/?p=120
permalink: /2010/09/23/validadores-do-doctrine-validators/
categories:
  - Sem categoria
  - Web
tags:
  - Doctrine
  - PHP
---
Neste post mostrarei os validadores presentes no <a href="http://www.doctrine-project.org" rel="externo nofollow">Doctrine</a> (usei a versão 1.2.3). O Doctrine facilita a validação dos dados, bastando apenas definir os validadores para cada atributo ao invés de fazer vários malabarismos com funções do PHP e expressões regulares. Você pode definir os validadores na classe que estende a classe base. Dessa maneira, você pode gerar o model novamente e suas alterações não serão perdidas. Primeiro listarei os validadores e ao final mostrarei alguns exemplos. Vamos lá.

<span style="color: rgb(255, 0, 0);"><strong>Importante</strong></span>
	  
Para que seus dados sejam validados, cheque se seu &#8220;bootstrap.php&#8221; contém a diretiva abaixo. Caso contrário, seus dados não serão validados.

[php]$manager->setAttribute(Doctrine\_Core::ATTR\_VALIDATE, Doctrine\_Core::VALIDATE\_ALL);
  
[/php]

**notnull**
	  
Garante que o valor não seja nulo na aplicação e no banco de dados.

[php]// models/SuaClasse.php

class SuaClasse extends BaseSuaClasse
  
{
      
// &#8230;

public function setTableDefinition(){
		  
parent::setTableDefinition();

// &#8230;

$this->hasColumn(&#8216;nome&#8217;, &#8216;string&#8217;, 70, array(
				  
&#8216;notnull&#8217; => true
			  
)
		  
);
	  
}
  
}
  
[/php]

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>teste, jonnas
	  
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>valores nulos</p> 

**email**
	  
Checa se o valor é um endereço de email válido.

[php] $this->hasColumn(&#8216;email&#8217;, &#8216;string&#8217;, 100, array(
				  
&#8216;email&#8217; => true
			  
)
	  
);
  
[/php]

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>contato@fonini.net
	  
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>fulano!#@server</p> 

**notblank**
	  
Este validador é semelhante ao validador notnull, exceto que além de não validar valores nulos, também não valida strings vazias.

[php] $this->hasColumn(&#8216;nome&#8217;, &#8216;string&#8217;, 100, array(
				  
&#8216;notblank&#8217; => true
			  
)
	  
);
  
[/php]

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>teste, jonnas
	  
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>valores nulos, &#8221;</p> 

**nospace**
	  
Checa se o valor não contém espaços.

[php] $this->hasColumn(&#8216;campo\_sem\_espacos&#8217;, &#8216;string&#8217;, 100, array(
				  
&#8216;nospace&#8217; => true
			  
)
	  
);
  
[/php]

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>JonnasFonini
	  
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>Jonnas Fonini</p> 

**past**
	  
Checa se o valor é uma data que já ocorreu, o dia de ontem, por exemplo.

[php] $this->hasColumn(&#8216;data&#8217;, &#8216;timestamp&#8217;, null, array(
				  
&#8216;past&#8217; => true
			  
)
	  
);
  
[/php]

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>Sendo hoje 14/09/2010, 01/01/2010 é válida
	  
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>Sendo hoje 14/09/2010, a mesma e posteriores são inválidas</p> 

**future**
	  
Checa se o valor é uma data que ainda não aconteceu, amanhã, por exemplo.

[php] $this->hasColumn(&#8216;data&#8217;, &#8216;timestamp&#8217;, null, array(
				  
&#8216;future&#8217; => true
			  
)
	  
);
  
[/php]

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>Sendo hoje 14/09/2010, 15/09/2010 é válida
	  
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>Sendo hoje 14/09/2010, a mesma e anteriores são inválidas</p> 

**minlength**
	  
Checa se o valor passado tem o tamanho mínimo necessário.

[php] $this->hasColumn(&#8216;senha&#8217;, &#8216;string&#8217;, 32, array(
				  
&#8216;minlength&#8217; => 6
			  
)
	  
);
  
[/php]

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>abcdef, abcdefg
	  
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>abc</p> 

**ip**
	  
Checa se o valor passado é um endereço IP válido.

[php] $this->hasColumn(&#8216;endereco_ip&#8217;, &#8216;string&#8217;, 15, array(
				  
&#8216;ip&#8217; => true
			  
)
	  
);
  
[/php]

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>192.168.250.222, 201.10.34.21
	  
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>345.10.10.290</p> 

**htmlcolor**
	  
Checa se o valor passado é uma cor HTML em hexadecimal.

[php] $this->hasColumn(&#8216;cor&#8217;, &#8216;string&#8217;, 7, array(
				  
&#8216;htmlcolor&#8217; => true
			  
)
	  
);
  
[/php]

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>#000FFF, FF0000
	  
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>#GGG111, #FFF (cores abreviadas são inválidas)</p> 

**range**
	  
Checa se o valor numérico está contido no intervalo especificado.

[php] $this->hasColumn(&#8216;idade&#8217;, &#8216;integer&#8217;, null, array(
				  
&#8216;range&#8217; => array(18, 70)
			  
)
	  
);
  
[/php]

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>19, 50, 69
	  
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>10, 18, 70</p> 

**unique**
	  
Checa se o valor já existe no banco de dados.

[php] $this->hasColumn(&#8216;rg&#8217;, &#8216;string&#8217;, 15, array(
				  
&#8216;unique&#8217; => true
			  
)
	  
);
  
[/php]

**regexp**
	  
Checa se o valor casa com a expressão regular passada.

[php] $this->hasColumn(&#8216;somente_letras&#8217;, &#8216;string&#8217;, 15, array(
				  
&#8216;regexp&#8217; => &#8216;/^[a-zA-Z]+$/&#8217;
			  
)
	  
);
  
[/php]

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>flex
	  
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>flex4</p> 

**creditcard**
	  
Checa se o valor é um número de cartão de crédito válido.

[php] $this->hasColumn(&#8216;cartao&#8217;, &#8216;integer&#8217;, 16, array(
				  
&#8216;creditcard&#8217; => true
			  
)
	  
);
  
[/php]

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>Cartões Visa, Master Card, American Express, Discover e Diners
	  
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>Outras bandeiras, exceto as citadas acima</p> 

**readonly**
	  
Evita que o valor de uma coluna da tabela seja alterado.

[php] $this->hasColumn(&#8216;coluna\_que\_nao\_pode\_ser_alterada&#8217;, &#8216;string&#8217;, 25, array(
				  
&#8216;readonly&#8217; => true
			  
)
	  
);
  
[/php]

**unsigned**
	  
Checa se o valor númerico passado possui sinal, de menos, por exemplo.

[php] $this->hasColumn(&#8216;idade&#8217;, &#8216;integer&#8217;, 3, array(
				  
&#8216;unsigned&#8217; => true
			  
)
	  
);
  
[/php]

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>70, 100
	  
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>-20</p> 

**usstate**
	  
Checa se a string passada é a sigla válida de um estado americano. Confira a lista completa <a href="http://en.wikipedia.org/wiki/Us_states" rel="externo nofollow">aqui</a>.

[php] $this->hasColumn(&#8216;estado_americano&#8217;, &#8216;string&#8217;, 2, array(
				  
&#8216;usstate&#8217; => true
			  
)
	  
);
  
[/php]

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>AL, CA
	  
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>QW</p> 

**country**
	  
Checa se a string passada é a sigla válida de um país. Confira a lista completa <a href="http://en.wikipedia.org/wiki/ISO_3166-1" rel="externo nofollow">aqui</a>.

[php] $this->hasColumn(&#8216;pais&#8217;, &#8216;string&#8217;, 2, array(
				  
&#8216;country&#8217; => true
			  
)
	  
);
  
[/php]

<span style="color: rgb(22, 188, 42);"><strong>Válido: </strong></span>br, BR, ar
	  
<span style="color: rgb(255, 0, 0);"><strong>Inválido: </strong></span>xx

No próximo post mostrarei como fazer um validador de estados brasileiros e outro de CEP&#8217;s.

Grande abraço e até a próxima!