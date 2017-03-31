---
title: Tutorial de Doctrine, um ORM para PHP
date: 2010-09-14T08:04:30+00:00
author: fonini
layout: post
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

{% highlight shell %}
seu_projeto/lib/Doctrine
seu_projeto/lib/vendor
seu_projeto/lib/Doctrine.php
{% endhighlight %}

Crie também uma pasta chamada "models" na raíz do projeto, dando permissão 777 a ela. Esta pasta irá conter o model da aplicação.

{% highlight shell %}
seu_projeto/models
{% endhighlight %}

**Configuração**

Crie um arquivo na pasta raíz do projeto chamado "bootstrap.php". Esse arquivo irá conter as configurações e parâmetros de funcionamento do Doctrine. Abaixo está o arquivo que eu uso. Você pode definir outros parâmetros consultando a <a href="http://www.doctrine-project.org/projects/orm/1.2/docs/en" rel="externo nofollow">documentação oficial</a>.

{% highlight php %}<?php // seu_projeto/bootstrap.php

require_once(dirname(__FILE__) . '/lib/Doctrine.php');

spl_autoload_register(array('Doctrine', 'autoload'));
spl_autoload_register(array('Doctrine_Core', 'modelsAutoload'));

$manager = Doctrine_Manager::getInstance();

// Configurações do banco de dados. O banco deve ser criado previamente.
$user = 'postgres';
$password = 'teste';
$host = 'localhost';
$dbname = 'testdoctrine';
$driver = 'pgsql';

$conn = Doctrine_Manager::connection($driver.'://'.$user.':'.$password.'@'.$host.'/'.$dbname);
$conn->setOption('username', $user);
$conn->setOption('password', $password);

$manager->setAttribute(Doctrine_Core::ATTR_EXPORT, Doctrine_Core::EXPORT_ALL);
$manager->setAttribute(Doctrine_Core::ATTR_MODEL_LOADING, Doctrine_Core::MODEL_LOADING_CONSERVATIVE);
$manager->setAttribute(Doctrine_Core::ATTR_AUTOLOAD_TABLE_CLASSES, true);
$manager->setAttribute(Doctrine_Core::ATTR_VALIDATE, Doctrine_Core::VALIDATE_ALL);

// Permite o override dos metodos do model.
$manager->setAttribute(Doctrine_Core::ATTR_AUTO_ACCESSOR_OVERRIDE, true);

// Formato das sequências (uso para PostgreSQL)
$manager->setAttribute(Doctrine_Core::ATTR_SEQNAME_FORMAT, '%s_seq');

// Carrega os models da pasta especificada, no caso "models"
Doctrine_Core::loadModels('models');
{% endhighlight %}



**Criação dos models**

Com seu projeto configurado, o próximo passo é criar o model. Vou mostrar as 3 formas disponíveis. 

_**Gerando as classes através das tabelas já existentes**_

Crie um arquivo chamado "test.php" que será usado neste e nos próximos passos. Deverá ter o seguinte conteúdo: 

{% highlight php %}<?php
require_once('bootstrap.php');  
{% endhighlight %}

Agora, basta adicionar as linhas abaixo ao seu arquivo "test.php". Comente-a após a geração, pois senão os models serão gerados novamente a cada execução. 

{% highlight php %}<?php // seu_projeto/test.php
require_once('bootstrap.php');

Doctrine_Core::generateModelsFromDb('models', array('doctrine'), array(	  
  'generateTableClasses' => true  
));
{% endhighlight %}

Você pode usar como exemplo as tabelas abaixo: 

{% highlight sql %}CREATE TABLE cidade (
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

ALTER TABLE ONLY pessoa ADD CONSTRAINT pessoa_id_cidade_cidade_id FOREIGN KEY (id_cidade) REFERENCES cidade(id);
{% endhighlight %}

_**Gerando as classes através de um arquivo YAML**_

Um arquivo YAML (extensão .yml) é um arquivo semelhante a um arquivo XML e eu diria muito mais poderoso (minha opinião). Ao invés de tags, os dados são representados pela identação dos atributos e seus valores (o pessoal do Python ama isso). A identação deve ser feita com **espaços** e não com tabulações. Para mais informações, consulte a <a href="http://en.wikipedia.org/wiki/YAML" rel="externo nofollow">Wikipédia</a>.
	  
Esta forma permite representar seus models no arquivo YAML.
	  
Se você ainda não tem classes definidas, crie o arquivo "schemas.yml" na raíz do projeto com o conteúdo abaixo: 

{% highlight yaml %}Cidade:
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
{% endhighlight %}

Caso você já tenha as classes definidas, basta remover o código de geração das classes do arquivo "test.php" e adicionar as linhas abaixo: 

{% highlight php %}<?php // seu_projeto/test.php
require_once('bootstrap.php');
Doctrine_Core::generateYamlFromModels('schema.yml', 'models');
{% endhighlight %}

Após executar o test.php, você verá um arquivo chamado "schema.yml" na pasta raíz, com a definição do model. Crie agora um arquivo chamado "generate.php" com o código abaixo. Esse arquivo será responsável por remover as tabelas do banco de dados (se existirem) e recriá-las com base no arquivo "schema.yml", gerando também as classes PHP. Portanto, muito cuidado, só execute quando for estritamente necessário, sob a pena de perder os dados do banco. 

{% highlight php %}<?php // seu_projeto/generate.php
require_once('bootstrap.php');

//Remova as próximas 2 linhas caso não queira remover e criar seu banco a cada execução.
Doctrine_Core::dropDatabases();
Doctrine_Core::createDatabases();
  
Doctrine_Core::generateModelsFromYaml('schema.yml', 'models');
Doctrine_Core::createTablesFromModels('models');
{% endhighlight %}

_**Definindo manualmente suas classes PHP**_

Usarei como exemplo duas classes, Pessoa e Cidade, sendo que uma pessoa pertence a uma cidade. Basta criar dois arquivos na pasta "models", Pessoa.php e Cidade.php, com o código abaixo: 

{% highlight php %}<?php // seu_projeto/models/Cidade.php
class Cidade extends Doctrine_Record{
  public function setTableDefinition(){	  
    $this->hasColumn('id', 'integer', null, array(	  
      'fixed' => false,
      'notnull' => true,
      'primary' => true,
      'autoincrement' => true
    ));

    $this->hasColumn('nome', 'string', 500, array('fixed' => true, 'notnull' => true));
    $this->hasColumn('uf', 'string', 2, array('fixed' => true, 'notnull' =>; true));  
  }
}
{% endhighlight %}

{% highlight php %}<?php // seu_projeto/models/Pessoa.php
class Pessoa extends Doctrine_Record{
  public function setTableDefinition(){	  
    $this->hasColumn('id', 'integer', null, array(
      'fixed' => false,
      'notnull' => true,
      'primary' => true,
      'autoincrement' => true
    ));

    $this->hasColumn('nome', 'string', 500, array('fixed' => true, 'notnull' => true));
    $this->hasColumn('data_nasc', 'date');
    $this->hasColumn('id_cidade', 'integer');
  }

  public function setUp(){
    $this->hasOne('Cidade', array(
      'local' => 'id_cidade',
      'foreign' => 'id'
    ));
  }
}
{% endhighlight %}

Após a definição das classes, rode o arquivo "test.php" com a linha "Doctrine_Core::generateYamlFromModels('schema.yml', 'models');". Após rodar esse arquivo, execute o "generate.php", que irá apagar o banco de dados, criá-lo novamente e criar as tabelas referentes as classes.

**Realizando consultas**

Com o model pronto, vamos realizar algumas consultas. 

_Inserindo pessoa com uma cidade associada a ela_

{% highlight php %}<?php
$cidade = new Cidade();  
$cidade->nome = 'Marau';
$cidade->uf = 'RS';
$cidade->save();

$pessoa = new Pessoa();
$pessoa->nome = "Jonnas Fonini";
$pessoa->data_nasc = date('1990-04-12');
$pessoa->id_cidade = $cidade;
$pessoa->save();
{% endhighlight %}

_Consultando informações de uma pessoa_

{% highlight php %}<?php
$pessoa = Doctrine_Core::getTable('Pessoa')->find(1);  

echo 'Id: '.$pessoa->id.'<br />';
echo 'Nome: '.$pessoa->nome.'<br />';
echo 'Data Nasc.: '.$pessoa->data_nasc.'<br />';
echo 'Cidade: '.$pessoa->Cidade->nome;
{% endhighlight %}

_Atualizando informações de uma pessoa_

{% highlight php %}<?php
$pessoa = Doctrine_Core::getTable('Pessoa')->find(1);  
$pessoa->data_nasc = date('Y-m-d');
$pessoa->save();
{% endhighlight %}

_Removendo uma pessoa_

{% highlight php %}<?php
$pessoa = Doctrine_Core::getTable('Pessoa')->find(1);  
$pessoa->delete();
{% endhighlight %}

**Download**

[Clique aqui](https://www.dropbox.com/s/nu6dttbu9o3874e/projeto-doctrine.zip?dl=0) para baixar o projeto já pronto. Mude as configurações do banco de dados no arquivo "bootstrap.php".

**Conclusão**

O Doctrine facilita muito a manipulação do banco de dados em PHP, poupando a você o trabalho de escrever consultas SQL. Incremente ainda mais seus estudos estudando o framework <a href="http://www.symfony-project.org" rel="externo nofollow">Symfony</a>, um dos mais completos da atualizade e que faz uso do Doctrine. Pretendo criar mais posts sobre o Doctrine em breve.
	  
Grande abraço a todos e até a próxima.