---
id: 346
title: Tutorial de Instalação e Configuração do Doctrine 2.2
date: 2012-02-22T23:46:33+00:00
author: fonini
layout: post
guid: http://www.fonini.net/blog/?p=346
permalink: /2012/02/22/tutorial-doctrine-de-instalacao-e-configuracao-do-2-2/
categories:
  - Sem categoria
  - Web
tags:
  - Doctrine
  - ORM
  - PHP
---
Ol&aacute;! Esta &eacute; a primeira vez que arrumo tempo para testar a vers&atilde;o 2 deste famoso ORM para PHP, o Doctrine. Criei este tutorial para servir como refer&ecirc;ncia futura e tamb&eacute;m para eventualmente auxiliar algu&eacute;m que esteja estudando. Vale lembrar que voc&ecirc; precisa ter o PHP 5.3.0 ou superior instalado na m&aacute;quina devido aos namespaces utilizados no Doctrine 2.

&nbsp;

### Download e Instala&ccedil;&atilde;o

<a href="http://www.doctrine-project.org/downloads/DoctrineORM-2.2.0-full.tar.gz" rel="nofollow">Baixe a &uacute;ltima vers&atilde;o</a> (no momento em que escrevo &eacute; a 2.2): Crie uma pasta no seu servidor e extraia o conte&uacute;do do arquivo rec&eacute;m baixado para dentro dela. Sua estrutura dever&aacute; ficar mais ou menos assim:

<pre>sua_pasta
|-- bin
|-- Doctrine
|-- entities</pre>

Logo ap&oacute;s, crie na raiz um arquivo chamado "bootstrap.php". Este arquivo ir&aacute; conter a configura&ccedil;&atilde;o b&aacute;sica do Doctrine 2, bem como fornecer&aacute; uma inst&acirc;ncia do Entity Manager. Opa, Entity Manager? &Eacute; meu amigo, dessa vez a semelhan&ccedil;a com o Hibernate est&aacute; maior ainda. As entidades tem at&eacute; anota&ccedil;&otilde;es! Claro que voc&ecirc; pode definir as entidades com XML (argh) e YAML. Mas pelo menos pra mim, nada como definir como classes PHP! Crie tamb&eacute;m um banco de dados para testar o Doctrine 2. [php]
  
// bootstrap.php

use DoctrineORMToolsSetup;
  
require_once "entities/Cidade.php";
  
require_once "entities/Pessoa.php";

require_once "Doctrine/ORM/Tools/Setup.php";

Setup::registerAutoloadPEAR();

$debug = true;
  
$config = Setup::createAnnotationMetadataConfiguration(array(\_\_DIR\_\_."/entities"), $debug);

// Configuração de acesso ao banco de dados
  
$conn = array(
      
&#8216;driver&#8217; => &#8216;pdo_mysql&#8217;,
      
&#8216;user&#8217; => &#8216;usuario&#8217;,
      
&#8216;password&#8217; => &#8216;senha&#8217;,
      
&#8216;dbname&#8217; => &#8216;doctrine2_test&#8217;
  
);

// Obtendo uma instância do Entity Manager
  
$entityManager = DoctrineORMEntityManager::create($conn, $config); [/php]

&nbsp;

### Definindo as entidades

Agora que voc&ecirc; j&aacute; configurou o bootstrap, vamos criar as entidades (classes) que ser&atilde;o usadas para a persist&ecirc;ncia no banco de dados. Na pasta "entities", criada anteriormente, crie os arquivos "Cidade.php" e "Pessoa.php" com o conte&uacute;do abaixo:
  
[php]
  
// entities/Cidade.php

use DoctrineCommonCollectionsArrayCollection;

/*\* \* @Entity @Table(name="cidade") */
  
class Cidade {
      
/*\* @Id @Column(type="integer") @GeneratedValue \*/
      
protected $id;

/*\* @Column(type="string") \*/
      
protected $nome;

/*\* @Column(type="string") \*/
      
protected $uf;

/*\* \* @OneToMany(targetEntity="Pessoa", mappedBy="cidade") *
      
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
  
[/php] &nbsp;

[php]
  
// entities/Pessoa.php

/*\* \* @Entity @Table(name="pessoa") */
  
class Pessoa {
      
/*\* @Id @Column(type="integer") @GeneratedValue \*/
      
protected $id;

/*\* @Column(type="string") \*/
      
protected $nome;

/*\* @Column(type="datetime") \*/
      
protected $dataHoraCadastro;

/*\* \* @ManyToOne(targetEntity="Cidade", inversedBy="habitantesCidade") */
      
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
  
[/php]

&nbsp;

### Cria&ccedil;&atilde;o das tabelas

A cria&ccedil;&atilde;o das tabelas no banco de dados ser&aacute; feita atrav&eacute;s da linha de comando. Caso n&atilde;o queira usar a linha de comando, o arquivo com os comandos SQL se encontra para download no final do post, juntamente com o projeto completo.

&nbsp;

### Utilizando a linha de comando

Se voc&ecirc; deseja usar a linha de comando do Doctrine 2, fa&ccedil;a uma pequena altera&ccedil;&atilde;o no arquivo bin/doctrine, adicionando a seguinte linha antes do include: 

[php] set\_include\_path(get\_include\_path() . PATH_SEPARATOR . &#8216;../&#8217;); [/php] 

Crie na raiz um arquivo chamado config-cli.php, que ir&aacute; conter a configura&ccedil;&atilde;o para rodar o Doctrine Tool atrav&eacute;s do terminal do Linux (ou prompt do Windows).

[php]
  
// config-cli.php

require_once "bootstrap.php";

$helperSet = new SymfonyComponentConsoleHelperHelperSet(array( &#8216;em&#8217; => new DoctrineORMToolsConsoleHelperEntityManagerHelper($entityManager) ));
  
[/php] 

Agora voc&ecirc; j&aacute; pode acessar a pasta "bin" atrav&eacute;s do terminal e gerar o SQL necess&aacute;rio para criar as tabelas usadas no exemplo. Para isto, basta entrar na pasta "bin" e rodar o comando:

<pre id="terminal" computer="valhalla" user="fonini">./doctrine orm:schema-tool:create --dump-sql</pre>

Ou se preferir, voc&ecirc; pode deixar o Doctrine conectar ao banco de dados e criar as tabelas para voc&ecirc;. Para isto, basta remover o trecho "&#8211;dump-sql" do comando. Criado o banco de dados, vamos testar a persist&ecirc;ncia de uma entidade (vulgo insert). Crie um arquivo com o nome de sua prefer&ecirc;ncia na ra&iacute;z, com o seguinte conte&uacute;do: 

[php]
  
require "bootstrap.php";

$cidade = new Cidade();
  
$cidade->setNome(&#8216;Marau&#8217;);
  
$cidade->setUf(&#8216;RS&#8217;);

$entityManager->persist($cidade);
  
$entityManager->flush();

echo "Cidade criada com o ID ".$cidade->getId()."n";
  
[/php] 

Rode o arquivo. Legal, n&atilde;o? Se n&atilde;o houve nenhum erro, d&ecirc; uma olhada no banco de dados, que o seu registro estar&aacute; l&aacute;. Caso houve algum erro, debugue at&eacute; a morte para encontrar o maldito e deixar funcionando. Veja agora um exemplo de persist&ecirc;ncia de um objeto da classe Pessoa com um objeto da classe Cidade associado: 

[php]
  
require "bootstrap.php";

$cidade = new Cidade();
  
$cidade->setNome(&#8216;Marau&#8217;);
  
$cidade->setUf(&#8216;RS&#8217;);

$pessoa = new Pessoa();
  
$pessoa->setNome(&#8216;Jonnas Fonini&#8217;);
  
$pessoa->setDataHoraCadastro(new DateTime("now"));
  
$pessoa->setCidade($cidade);

$entityManager->persist($cidade);
  
$entityManager->persist($pessoa);
  
$entityManager->flush();

echo "Pessoa criada com o ID ".$pessoa->getId()." e associada com a Cidade ".$cidade->getId();
  
[/php]

&nbsp;

### Localizando uma entidade pelo ID

[php]
  
require "bootstrap.php";

$pessoa = $entityManager->find("Pessoa", 1);
  
print &#8216;Nome: &#8216; . $pessoa->getNome() . &#8216; &#8216;;
  
print &#8216;Cidade: &#8216; . $pessoa->getCidade()->getNome();
  
[/php] 

Outros exemplos, como listagem, atualiza&ccedil;&atilde;o e exclus&atilde;o voc&ecirc; encontra no arquivo dispon&iacute;vel no final do post.

&nbsp;

### Conclus&atilde;o

Apesar de ser a primeira vez que uso o Doctrine 2, posso dizer que est&aacute; demais! Est&aacute; bem mais organizado que a primeira vers&atilde;o, sem contar que as anota&ccedil;&otilde;es facilitam muito o mapeamento do banco. Pra quem n&atilde;o gosta, pode usar XML e YAML. O bootstrap tamb&eacute;m est&aacute; mais limpo e exige bem menos configura&ccedil;&atilde;o.

&nbsp;

### Download

[Baixe aqui](http://www.fonini.net/labs/doctrine2.zip) os arquivos usados no exemplo. Grande abra&ccedil;o a todos e at&eacute; a pr&oacute;xima.