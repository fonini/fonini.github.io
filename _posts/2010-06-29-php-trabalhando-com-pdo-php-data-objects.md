---
id: 104
title: 'PHP &#8211; Trabalhando com PDO (PHP Data Objects)'
date: 2010-06-29T08:07:57+00:00
author: fonini
layout: post
guid: http://www.fonini.net/blog/?p=104
permalink: /2010/06/29/php-trabalhando-com-pdo-php-data-objects/
categories:
  - Sem categoria
  - Web
tags:
  - PHP
---
Olá pessoal, voltando com um novo post depois de muito tempo sem blogar. Hoje vou falar sobre PDO (PHP Data Objects), uma extensão presente a partir da versão 5 do PHP que permite desenvolver códigos de acesso a banco de dados portáveis, mudando apenas uma linha de código.

Imagine um sistema cheio de mysql\_connect&#8217;s, mysql\_query&#8217;s e de uma hora pra outra você se vê obrigado a mudar o banco de dados pra PostgreSQL, por exemplo. Imagine o trabalho de alterar toda essa parte do seu projeto? O PDO veio para solucionar esse e muitos outros problemas, como o de SQL Injection, já que usa prepared statements (falarei deles mais abaixo). No caso de você ter um sistema inteiro usando PDO e decide mudar de SGBD, basta alterar apenas a linha de conexão com o tipo de banco de dados desejado.</p> 

**<span style="font-size: 14px;">Conexão</span>**</p> 

[php] try{
		  
$conn = new PDO(&#8216;mysql:host=localhost;dbname=seuBD&#8217;, &#8216;root&#8217;, &#8216;12345&#8217;);
	  
}
	  
catch (PDOException $e){
		  
print &#8216;Erro: &#8216; . $e->getMessage();
	  
}
  
[/php]

Este é um exemplo de conexão. Você pode criar uma classe utilizando o padrão <a href="http://pt.wikipedia.org/wiki/Singleton" rel="externo nofollow">Singleton</a>, instanciando apenas uma conexão PDO para a aplicação inteira. Se você quisesse alterar o SGBD para PostgreSQL, bastava apenas substituir a palavra _mysql_ por _pgsql_.

Para descobrir quais drivers do PDO você tem disponíveis, execute o código abaixo:</p> 

[php] foreach(PDO::getAvailableDrivers() as $driver){
		  
echo $driver.'<br />&#8217;;
	  
}
  
[/php]

Por padrão, o PDO não exibe erros de consultas escritas incorretamente, por exemplo. Para exibir os erros e facilitar o desenvolvimento da aplicação, basta passar os seguintes parâmetros ao objeto:</p> 

[php] $conn->setAttribute(PDO::ATTR\_ERRMODE, PDO::ERRMODE\_WARNING);
  
[/php]

**<span style="font-size: 14px;">Selecionando dados<br /> </span>**

Agora que você já tem seu objeto PDO instanciado, é só usá-lo para realizar as consultas. Veja um exemplo de select:</p> 

[php] $clientes = $conn->prepare(&#8216;SELECT id, nome FROM clientes&#8217;);
	  
$clientes->execute();

while ($dadosClientes = $clientes->fetch()){
		  
echo &#8216;ID: &#8216; . $dadosClientes[&#8216;id&#8217;] . &#8216; Nome: &#8216; . $dadosClientes[&#8216;nome&#8217;] . &#8216;<br />&#8217;;
	  
}
  
[/php]


	  
Viu como é simples? Você também pode passar parâmetros para a consulta da seguinte forma:</p> 

[php] $clientes = $conn->prepare(&#8216;SELECT id, nome FROM clientes WHERE id = :id AND nome = :nome&#8217;);
	  
$clientes->bindParam(&#8216;:id&#8217;, $\_POST[&#8216;id&#8217;], PDO::PARAM\_INT);
	  
$clientes->bindParam(&#8216;:nome&#8217;, $_POST[&#8216;nome&#8217;]);
	  
$clientes->execute();

while ($dadosClientes = $clientes->fetch()){
		  
echo &#8216;ID: &#8216; . $dadosClientes[&#8216;id&#8217;] . &#8216; Nome: &#8216; . $dadosClientes[&#8216;nome&#8217;] . &#8216;<br />&#8217;;
	  
}
  
[/php]

A grande vantagem do PDO é que se você usar prepared statements, não precisará se preocupar com SQL Injection, pois o PDO já faz todo o serviço de filtragem dos dados de entrada para você, de forma muito segura.

A lógica é a mesma para executar outros tipos de consultas. Veja um exemplo de insert:</p> 

[php] $clientes = $conn->prepare(&#8216;INSERT INTO clientes (nome) VALUES (:nome));
	  
$clientes->bindParam(&#8216;:nome&#8217;, $_POST[&#8216;nome&#8217;]);
	  
$clientes->execute();

if ($clientes->rowCount() > 0){
		  
echo &#8216;Registro inserido com sucesso&#8217;;
	  
}
  
[/php]

Para mais detalhes, consulte a <a href="http://br3.php.net/manual/en/book.pdo.php" rel="externo nofollow">documentação oficial</a>.

Espero que tenham gostado do post. Um abraço e até a próxima!