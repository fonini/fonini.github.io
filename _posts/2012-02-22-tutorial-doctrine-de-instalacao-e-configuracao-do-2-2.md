---
id: 346
title: Tutorial de Instalação e Configuração do Doctrine 2.2
date: 2012-02-22T23:46:33+00:00
author: fonini
layout: post
permalink: /2012/02/22/tutorial-doctrine-de-instalacao-e-configuracao-do-2-2/
categories:
  - Sem categoria
  - Web
tags:
  - Doctrine
  - ORM
  - PHP
---
Olá! Esta é a primeira vez que arrumo tempo para testar a versão 2 deste famoso ORM para PHP, o Doctrine. Criei este tutorial para servir como referência futura e também para eventualmente auxiliar alguém que esteja estudando. Vale lembrar que você precisa ter o PHP 5.3.0 ou superior instalado na máquina devido aos namespaces utilizados no Doctrine 2.

### Download e Instalação

<a href="http://www.doctrine-project.org/downloads/DoctrineORM-2.2.0-full.tar.gz" rel="nofollow">Baixe a última versão</a> (no momento em que escrevo é a 2.2): Crie uma pasta no seu servidor e extraia o conteúdo do arquivo recém baixado para dentro dela. Sua estrutura deverá ficar mais ou menos assim:

{% highlight shell %}>sua_pasta
|-- bin
|-- Doctrine
|-- entities{% endhighlight %}

Logo após, crie na raiz um arquivo chamado "bootstrap.php". Este arquivo irá conter a configuração básica do Doctrine 2, bem como fornecerá uma instância do Entity Manager. Opa, Entity Manager? É meu amigo, dessa vez a semelhança com o Hibernate está maior ainda. As entidades tem até anotações! Claro que você pode definir as entidades com XML (argh) e YAML. Mas pelo menos pra mim, nada como definir como classes PHP! Crie também um banco de dados para testar o Doctrine 2. 

{% highlight php %}<?php // bootstrap.php
use DoctrineORMToolsSetup;

require_once "entities/Cidade.php";  
require_once "entities/Pessoa.php";
require_once "Doctrine/ORM/Tools/Setup.php";

Setup::registerAutoloadPEAR();

$debug = true;
  
$config = Setup::createAnnotationMetadataConfiguration(array(__DIR__."/entities"), $debug);

// Configuração de acesso ao banco de dados
$conn = array(
	'driver' => 'pdo_mysql',
	'user' => 'usuario',
	'password' => 'senha',
	'dbname' => 'doctrine2_test'
);

// Obtendo uma instância do Entity Manager
$entityManager = DoctrineORMEntityManager::create($conn, $config); {% endhighlight %}

### Definindo as entidades

Agora que você já configurou o bootstrap, vamos criar as entidades (classes) que serão usadas para a persistência no banco de dados. Na pasta "entities", criada anteriormente, crie os arquivos "Cidade.php" e "Pessoa.php" com o conteúdo abaixo:

{% highlight php %}<?php // entities/Cidade.php
use DoctrineCommonCollectionsArrayCollection;

/** * @Entity @Table(name="cidade") */
class Cidade {

	/** @Id @Column(type="integer") @GeneratedValue */
	protected $id;

	/** @Column(type="string") */
	protected $nome;

	/** @Column(type="string") */
	protected $uf;

	/** * @OneToMany(targetEntity="Pessoa", mappedBy="cidade") * 
	@var Pessoa[] */

	protected $habitantesCidade = null;

	public function __construct() {
		$this->habitantesCidade = new ArrayCollection();
	}

	public function getId() {
		return $this->id;
	}

	public function getNome() {
		return $this->nome;
	}

	public function setNome($nome) {
		$this->nome = $nome;
	}

	public function getUf() {
		return $this->uf;
	}

	public function setUf($uf) {
		$this->uf = $uf;
	}

	public function adicionarHabitante($pessoa) {
		$this->habitantesCidade[] = $pessoa;
	}
}
{% endhighlight %}

{% highlight php %}<?php // entities/Pessoa.php

/** * @Entity @Table(name="pessoa") */
class Pessoa {

	/** @Id @Column(type="integer") @GeneratedValue */
	protected $id;

	/** @Column(type="string") */
	protected $nome;

	/** @Column(type="datetime") */
	protected $dataHoraCadastro;

	/** * @ManyToOne(targetEntity="Cidade", inversedBy="habitantesCidade") */  
	protected $cidade;

	public function getId() {
		return $this->id;
	}

	public function getNome() {
		return $this->nome;
	}

	public function setNome($nome) {
		$this->nome = $nome;
	}

	public function getDataHoraCadastro() {
		return $this->dataHoraCadastro;
	}

	public function setDataHoraCadastro(DateTime $dataHoraCadastro) {
		$this->dataHoraCadastro = $dataHoraCadastro;
	}

	public function getCidade() {
		return $this->cidade;
	}

	public function setCidade($cidade) {
		$this->cidade = $cidade;
	}
}
{% endhighlight %}

### Criação das tabelas

A criação das tabelas no banco de dados será feita através da linha de comando. Caso não queira usar a linha de comando, o arquivo com os comandos SQL se encontra para download no final do post, juntamente com o projeto completo.

### Utilizando a linha de comando

Se você deseja usar a linha de comando do Doctrine 2, faça uma pequena alteração no arquivo bin/doctrine, adicionando a seguinte linha antes do include: 

{% highlight php %}<?php
set_include_path(get_include_path() . PATH_SEPARATOR . '../'); {% endhighlight %}

Crie na raiz um arquivo chamado config-cli.php, que irá conter a configuração para rodar o Doctrine Tool através do terminal do Linux (ou prompt do Windows).

{% highlight php %}<?php // config-cli.php
require_once "bootstrap.php";

$helperSet = new SymfonyComponentConsoleHelperHelperSet(array( 'em' => new DoctrineORMToolsConsoleHelperEntityManagerHelper($entityManager) ));
{% endhighlight %} 

Agora você já pode acessar a pasta "bin" através do terminal e gerar o SQL necessário para criar as tabelas usadas no exemplo. Para isto, basta entrar na pasta "bin" e rodar o comando:

{% highlight shell %}./doctrine orm:schema-tool:create --dump-sql{% endhighlight %}

Ou se preferir, você pode deixar o Doctrine conectar ao banco de dados e criar as tabelas para você. Para isto, basta remover o trecho "-;dump-sql" do comando. Criado o banco de dados, vamos testar a persistência de uma entidade (vulgo insert). Crie um arquivo com o nome de sua preferência na raíz, com o seguinte conteúdo: 

{% highlight php %}<?php
require "bootstrap.php";

$cidade = new Cidade();
$cidade->setNome('Marau');
$cidade->setUf('RS');

$entityManager->persist($cidade);
$entityManager->flush();

echo "Cidade criada com o ID ".$cidade->getId()."n";
{% endhighlight %} 

Rode o arquivo. Legal, não? Se não houve nenhum erro, dê uma olhada no banco de dados, que o seu registro estará lá. Caso houve algum erro, debugue até a morte para encontrar o maldito e deixar funcionando. Veja agora um exemplo de persistência de um objeto da classe Pessoa com um objeto da classe Cidade associado: 

{% highlight php %}<?php
require "bootstrap.php";

$cidade = new Cidade();
$cidade->setNome('Marau');
$cidade->setUf('RS');

$pessoa = new Pessoa();
$pessoa->setNome('Jonnas Fonini');
$pessoa->setDataHoraCadastro(new DateTime("now"));
$pessoa->setCidade($cidade);

$entityManager->persist($cidade);
$entityManager->persist($pessoa);

$entityManager->flush();

echo "Pessoa criada com o ID ".$pessoa->getId()." e associada com a Cidade ".$cidade->getId();
{% endhighlight %}


### Localizando uma entidade pelo ID

{% highlight php %}<?php
require "bootstrap.php";

$pessoa = $entityManager->find("Pessoa", 1);

print 'Nome: ' . $pessoa->getNome() . ' ';  
print 'Cidade: ' . $pessoa->getCidade()->getNome();
{% endhighlight %} 

Outros exemplos, como listagem, atualização e exclusão você encontra no arquivo disponível no final do post.

### Conclusão

Apesar de ser a primeira vez que uso o Doctrine 2, posso dizer que está demais! Está bem mais organizado que a primeira versão, sem contar que as anotações facilitam muito o mapeamento do banco. Pra quem não gosta, pode usar XML e YAML. O bootstrap também está mais limpo e exige bem menos configuração.

### Download

[Baixe aqui](http://www.fonini.net/labs/doctrine2.zip) os arquivos usados no exemplo. Grande abraço a todos e até a próxima.