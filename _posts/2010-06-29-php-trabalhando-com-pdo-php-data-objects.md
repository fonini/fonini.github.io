---
title: 'PHP: Trabalhando com PDO (PHP Data Objects)'
date: 2010-06-29T08:07:57+00:00
author: fonini
layout: post
permalink: /2010/06/29/php-trabalhando-com-pdo-php-data-objects/
tags:
  - PHP
---
Olá pessoal, voltando com um novo post depois de muito tempo sem blogar. Hoje vou falar sobre PDO (PHP Data Objects), uma extensão presente a partir da versão 5 do PHP que permite desenvolver códigos de acesso a banco de dados portáveis, mudando apenas uma linha de código.

Imagine um sistema cheio de mysql_connect's, mysql_query's e de uma hora pra outra você se vê obrigado a mudar o banco de dados pra PostgreSQL, por exemplo. Imagine o trabalho de alterar toda essa parte do seu projeto? O PDO veio para solucionar esse e muitos outros problemas, como o de SQL Injection, já que usa prepared statements (falarei deles mais abaixo). No caso de você ter um sistema inteiro usando PDO e decide mudar de SGBD, basta alterar apenas a linha de conexão com o tipo de banco de dados desejado.

**Conexão**

{% highlight php %}<?php
try{	  
	$conn = new PDO('mysql:host=localhost;dbname=seuBD', 'root', '12345');
}  
catch (PDOException $e){		  
	print 'Erro: ' . $e->getMessage();  
}
{% endhighlight %}

Este é um exemplo de conexão. Você pode criar uma classe utilizando o padrão <a href="http://pt.wikipedia.org/wiki/Singleton" rel="externo nofollow">Singleton</a>, instanciando apenas uma conexão PDO para a aplicação inteira. Se você quisesse alterar o SGBD para PostgreSQL, bastava apenas substituir a palavra _mysql_ por _pgsql_.

Para descobrir quais drivers do PDO você tem disponíveis, execute o código abaixo:

{% highlight php %}<?php
foreach(PDO::getAvailableDrivers() as $driver){		  
	echo $driver.'<br />';  
}
{% endhighlight %}

Por padrão, o PDO não exibe erros de consultas escritas incorretamente, por exemplo. Para exibir os erros e facilitar o desenvolvimento da aplicação, basta passar os seguintes parâmetros ao objeto:

{% highlight php %}<?php
$conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_WARNING);
{% endhighlight %}

**Selecionando dados**

Agora que você já tem seu objeto PDO instanciado, é só usá-lo para realizar as consultas. Veja um exemplo de select:

{% highlight php %}<?php
$clientes = $conn->prepare('SELECT id, nome FROM clientes');	  
$clientes->execute();

while ($dadosClientes = $clientes->fetch()){
	echo 'ID: ' . $dadosClientes['id'] . ' Nome: ' . $dadosClientes['nome'] . '<br />';  
}
{% endhighlight %}

	  
Viu como é simples? Você também pode passar parâmetros para a consulta da seguinte forma:

{% highlight php %}<?php
$clientes = $conn->prepare('SELECT id, nome FROM clientes WHERE id = :id AND nome = :nome');	  
$clientes->bindParam(':id', $_POST['id'], PDO::PARAM_INT);
$clientes->bindParam(':nome', $_POST['nome']);
$clientes->execute();

while ($dadosClientes = $clientes->fetch()){
	echo 'ID: ' . $dadosClientes['id'] . ' Nome: ' . $dadosClientes['nome'] . '<br />';  
}
{% endhighlight %}

A grande vantagem do PDO é que se você usar prepared statements, não precisará se preocupar com SQL Injection, pois o PDO já faz todo o serviço de filtragem dos dados de entrada para você, de forma muito segura.

A lógica é a mesma para executar outros tipos de consultas. Veja um exemplo de insert:

{% highlight php %}<?php
$clientes = $conn->prepare('INSERT INTO clientes (nome) VALUES (:nome)');	  
$clientes->bindParam(':nome', $_POST['nome']);
$clientes->execute();

if ($clientes->rowCount() > 0){
	echo 'Registro inserido com sucesso';  
}
{% endhighlight %}

Para mais detalhes, consulte a <a href="http://br3.php.net/manual/en/book.pdo.php" rel="externo nofollow">documentação oficial</a>.

Espero que tenham gostado do post. Um abraço e até a próxima!