---
id: 118
title: Tutorial de Doctrine, um ORM para PHP
date: 2010-09-14T08:04:30+00:00
author: fonini
layout: post
guid: http://www.fonini.net/blog/?p=118
permalink: /2010/09/14/tutorial-de-doctrine-um-orm-para-php/
categories:
  - Sem categoria
  - Web
tags:
  - Doctrine
  - PHP
---
O <a href="http://www.doctrine-project.org" rel="externo nofollow">Doctrine</a> é um mapeador objeto-relacional (ORM) para PHP, aos moldes do Hibernate para Java. Este ORM elimina a tarefa de escrever consultas SQL básicas, além de facilitar a conexão com o banco de dados, através da extensão PDO. O Doctrine permite que você crie seu model escrevendo suas classes em PHP (seguindo alguns padrões pré-definidos), através de arquivos YAML ou ele se encarrega da geração do model através das tabelas já criadas no banco de dados. Uma vez que o model está criado, você pode definir validadores para campos específicos da tabela realizando essas alterações na classe gerada que estende cada model. Dessa forma, seu model fica preservado, você apenas altera a classe estendida, tornando fácil desfazer modificações.

**Instalação**

Baixe a última versão estável no <a href="http://www.doctrine-project.org/projects/orm/download" rel="externo nofollow">site do projeto</a>. No momento em que escrevo este post, a última versão estável é a 1.2.3. A versão 2 escontra-se em fase beta. Quem sabe quando ela for lançada sai mais um post. Crie uma pasta para seu projeto no seu webserver e dentro dela crie uma pasta lib. Após criar a pasta, extraia o Doctrine para ela. A estrutura deverá ficar semelhante a esta:
	  
seu_projeto/lib/Doctrine
	  
seu_projeto/lib/vendor
	  
seu_projeto/lib/Doctrine.php

Crie também uma pasta chamada &#8220;models&#8221; na raíz do projeto, dando permissão 777 a ela. Esta pasta irá conter o model da aplicação.
	  
seu_projeto/models

**Configuração**

Crie um arquivo na pasta raíz do projeto chamado &#8220;bootstrap.php&#8221;. Esse arquivo irá conter as configurações e parâmetros de funcionamento do Doctrine. Abaixo está o arquivo que eu uso. Você pode definir outros parâmetros consultando a <a href="http://www.doctrine-project.org/projects/orm/1.2/docs/en" rel="externo nofollow">documentação oficial</a>.

[php]// seu_projeto/bootstrap.php

require\_once(dirname(\\_\_FILE\_\_) . &#8216;/lib/Doctrine.php&#8217;);

spl\_autoload\_register(array(&#8216;Doctrine&#8217;, &#8216;autoload&#8217;));
  
spl\_autoload\_register(array(&#8216;Doctrine_Core&#8217;, &#8216;modelsAutoload&#8217;));

$manager = Doctrine_Manager::getInstance();

// Configurações do banco de dados. O banco deve ser criado previamente.
  
$user = &#8216;postgres&#8217;;
  
$password = &#8216;teste&#8217;;
  
$host = &#8216;localhost&#8217;;
  
$dbname = &#8216;testdoctrine&#8217;;
  
$driver = &#8216;pgsql&#8217;;

$conn = Doctrine_Manager::connection($driver.&#8217;://&#8217;.$user.&#8217;:&#8217;.$password.&#8217;@&#8217;.$host.&#8217;/&#8217;.$dbname);
  
$conn->setOption(&#8216;username&#8217;, $user);
  
$conn->setOption(&#8216;password&#8217;, $password);
  
$manager->setAttribute(Doctrine\_Core::ATTR\_EXPORT, Doctrine\_Core::EXPORT\_ALL);
  
$manager->setAttribute(Doctrine\_Core::ATTR\_MODEL\_LOADING, Doctrine\_Core::MODEL\_LOADING\_CONSERVATIVE);
  
$manager->setAttribute(Doctrine\_Core::ATTR\_AUTOLOAD\_TABLE\_CLASSES, true);
  
$manager->setAttribute(Doctrine\_Core::ATTR\_VALIDATE, Doctrine\_Core::VALIDATE\_ALL);

// Permite o override dos metodos do model.
  
$manager->setAttribute(Doctrine\_Core::ATTR\_AUTO\_ACCESSOR\_OVERRIDE, true);

// Formato das sequências (uso para PostgreSQL)
  
$manager->setAttribute(Doctrine\_Core::ATTR\_SEQNAME\_FORMAT, &#8216;%s\_seq&#8217;);

// Carrega os models da pasta especificada, no caso "models"
  
Doctrine_Core::loadModels(&#8216;models&#8217;);
  
[/php]



**Criação dos models**

Com seu projeto configurado, o próximo passo é criar o model. Vou mostrar as 3 formas disponíveis. 

_**Gerando as classes através das tabelas já existentes**_

Crie um arquivo chamado &#8220;test.php&#8221; que será usado neste e nos próximos passos. Deverá ter o seguinte conteúdo: 

[php]require_once(&#8216;bootstrap.php&#8217;);
  
[/php]

Agora, basta adicionar as linhas abaixo ao seu arquivo &#8220;test.php&#8221;. Comente-a após a geração, pois senão os models serão gerados novamente a cada execução. 

[php]// seu_projeto/test.php
  
require_once(&#8216;bootstrap.php&#8217;);

Doctrine_Core::generateModelsFromDb(&#8216;models&#8217;, array(&#8216;doctrine&#8217;), array(
	  
&#8216;generateTableClasses&#8217; => true
	  
)
  
);
  
[/php]

Você pode usar como exemplo as tabelas abaixo: 

[sql]CREATE TABLE cidade (
      
id bigint NOT NULL,
      
nome character(500) NOT NULL,
      
uf character(2) NOT NULL
  
);

CREATE TABLE pessoa (
      
id bigint NOT NULL,
      
nome character(500) NOT NULL,
      
data_nasc date,
      
id_cidade bigint
  
);

ALTER TABLE ONLY cidade ADD CONSTRAINT cidade_pkey PRIMARY KEY (id);
  
ALTER TABLE ONLY pessoa ADD CONSTRAINT pessoa_pkey PRIMARY KEY (id);
  
ALTER TABLE ONLY pessoa ADD CONSTRAINT
  
pessoa\_id\_cidade\_cidade\_id FOREIGN KEY (id_cidade) REFERENCES cidade(id);
  
[/sql]

_**Gerando as classes através de um arquivo YAML**_

Um arquivo YAML (extensão .yml) é um arquivo semelhante a um arquivo XML e eu diria muito mais poderoso (minha opinião). Ao invés de tags, os dados são representados pela identação dos atributos e seus valores (o pessoal do Python ama isso). A identação deve ser feita com **espaços** e não com tabulações. Para mais informações, consulte a <a href="http://en.wikipedia.org/wiki/YAML" rel="externo nofollow">Wikipédia</a>.
	  
Esta forma permite representar seus models no arquivo YAML.
	  
Se você ainda não tem classes definidas, crie o arquivo &#8220;schemas.yml&#8221; na raíz do projeto com o conteúdo abaixo: 

<pre>Cidade:
  connection: 0
  tableName: cidade
  columns:
    id:
      fixed: false
      notnull: true
      primary: true
      autoincrement: true
      type: integer(8)
    nome:
      fixed: true
      notnull: true
      type: string(500)
    uf:
      fixed: true
      notnull: true
      type: string(2)
  relations:
    Pessoa:
      local: id
      foreign: id_cidade
      type: many
Pessoa:
  connection: 0
  tableName: pessoa
  columns:
    id:
      fixed: false
      notnull: true
      primary: true
      autoincrement: true
      type: integer(8)
    nome:
      fixed: true
      notnull: true
      type: string(500)
    data_nasc: date(25)
    id_cidade: integer(8)
  relations:
    Cidade:
      local: id_cidade
      foreign: id
      type: one
</pre>

Caso você já tenha as classes definidas, basta remover o código de geração das classes do arquivo &#8220;test.php&#8221; e adicionar as linhas abaixo: 

<pre class="brush:php">// seu_projeto/test.php
require_once('bootstrap.php');
Doctrine_Core::generateYamlFromModels('schema.yml', 'models');
</pre>

Após executar o test.php, você verá um arquivo chamado &#8220;schema.yml&#8221; na pasta raíz, com a definição do model. Crie agora um arquivo chamado &#8220;generate.php&#8221; com o código abaixo. Esse arquivo será responsável por remover as tabelas do banco de dados (se existirem) e recriá-las com base no arquivo &#8220;schema.yml&#8221;, gerando também as classes PHP. Portanto, muito cuidado, só execute quando for estritamente necessário, sob a pena de perder os dados do banco. 

[php]// seu_projeto/generate.php
  
require_once(&#8216;bootstrap.php&#8217;);

//Remova as próximas 2 linhas caso não queira remover e criar seu banco a cada execução.
  
Doctrine_Core::dropDatabases();
  
Doctrine_Core::createDatabases();
  
Doctrine_Core::generateModelsFromYaml(&#8216;schema.yml&#8217;, &#8216;models&#8217;);
  
Doctrine_Core::createTablesFromModels(&#8216;models&#8217;);
  
[/php]

_**Definindo manualmente suas classes PHP**_

Usarei como exemplo duas classes, Pessoa e Cidade, sendo que uma pessoa pertence a uma cidade. Basta criar dois arquivos na pasta &#8220;models&#8221;, Pessoa.php e Cidade.php, com o código abaixo: 

[php]// seu_projeto/models/Cidade.php

class Cidade extends Doctrine_Record{
	  
public function setTableDefinition(){
		  
$this->hasColumn(&#8216;id&#8217;, &#8216;integer&#8217;, null, array(
			  
&#8216;fixed&#8217; => false,
			  
&#8216;notnull&#8217; => true,
			  
&#8216;primary&#8217; => true,
			  
&#8216;autoincrement&#8217; => true
			  
)
		  
);
		  
$this->hasColumn(&#8216;nome&#8217;, &#8216;string&#8217;, 500, array(&#8216;fixed&#8217; => true, &#8216;notnull&#8217; => true));
		  
$this->hasColumn(&#8216;uf&#8217;, &#8216;string&#8217;, 2, array(&#8216;fixed&#8217; => true, &#8216;notnull&#8217; =>; true));
	  
}
  
}
  
\[/php\]\[php\]// seu_projeto/models/Pessoa.php

class Pessoa extends Doctrine_Record{
	  
public function setTableDefinition(){
		  
$this->hasColumn(&#8216;id&#8217;, &#8216;integer&#8217;, null, array(
			  
&#8216;fixed&#8217; => false,
			  
&#8216;notnull&#8217; => true,
			  
&#8216;primary&#8217; => true,
			  
&#8216;autoincrement&#8217; => true
			  
)
		  
);
		  
$this->hasColumn(&#8216;nome&#8217;, &#8216;string&#8217;, 500, array(&#8216;fixed&#8217; => true, &#8216;notnull&#8217; => true));
		  
$this->hasColumn(&#8216;data_nasc&#8217;, &#8216;date&#8217;);
		  
$this->hasColumn(&#8216;id_cidade&#8217;, &#8216;integer&#8217;);
	  
}

public function setUp(){
		  
$this->hasOne(&#8216;Cidade&#8217;, array(
				  
&#8216;local&#8217; => &#8216;id_cidade&#8217;,
				  
&#8216;foreign&#8217; => &#8216;id&#8217;
			  
)
		  
);
	  
}
  
}
  
[/php]

Após a definição das classes, rode o arquivo &#8220;test.php&#8221; com a linha &#8220;Doctrine_Core::generateYamlFromModels(&#8216;schema.yml&#8217;, &#8216;models&#8217;);&#8221;. Após rodar esse arquivo, execute o &#8220;generate.php&#8221;, que irá apagar o banco de dados, criá-lo novamente e criar as tabelas referentes as classes.

**Realizando consultas**

Com o model pronto, vamos realizar algumas consultas. 

_Inserindo pessoa com uma cidade associada a ela_

[php]$cidade = new Cidade();
  
$cidade->nome = &#8216;Marau&#8217;;
  
$cidade->uf = &#8216;RS&#8217;;
  
$cidade->save();

$pessoa = new Pessoa();
  
$pessoa->nome = "Jonnas Fonini";
  
$pessoa->data_nasc = date(&#8216;1990-04-12&#8217;);
  
$pessoa->id_cidade = $cidade;
  
$pessoa->save();
  
[/php]

_Consultando informações de uma pessoa_

[php]$pessoa = Doctrine_Core::getTable(&#8216;Pessoa&#8217;)->find(1);
  
echo &#8216;Id: &#8216;.$pessoa->id.'<br />&#8217;;
  
echo &#8216;Nome: &#8216;.$pessoa->nome.'<br />&#8217;;
  
echo &#8216;Data Nasc.: &#8216;.$pessoa->data_nasc.'<br />&#8217;;
  
echo &#8216;Cidade: &#8216;.$pessoa->Cidade->nome;
  
[/php]

_Atualizando informações de uma pessoa_

[php]$pessoa = Doctrine_Core::getTable(&#8216;Pessoa&#8217;)->find(1);
  
$pessoa->data_nasc = date(&#8216;Y-m-d&#8217;);
  
$pessoa->save();
  
[/php]

_Removendo uma pessoa_

[php]$pessoa = Doctrine_Core::getTable(&#8216;Pessoa&#8217;)->find(1);
  
$pessoa->delete();
  
[/php]

**Download**

[Clique aqui](http://www.fonini.net/labs/projeto-doctrine.zip) para baixar o projeto já pronto. Mude as configurações do banco de dados no arquivo &#8220;bootstrap.php&#8221;.

**Conclusão**

O Doctrine facilita muito a manipulação do banco de dados em PHP, poupando a você o trabalho de escrever consultas SQL. Incremente ainda mais seus estudos estudando o framework <a href="http://www.symfony-project.org" rel="externo nofollow">Symfony</a>, um dos mais completos da atualizade e que faz uso do Doctrine. Pretendo criar mais posts sobre o Doctrine em breve.
	  
Grande abraço a todos e até a próxima.

[#soudev](http://www.soudev.com.br)