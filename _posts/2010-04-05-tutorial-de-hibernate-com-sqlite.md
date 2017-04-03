---
title: Tutorial de Hibernate com SQLite
date: 2010-04-05T09:26:08+00:00
author: fonini
layout: post
permalink: /2010/04/05/tutorial-de-hibernate-com-sqlite/
tags:
  - Hibernate
  - Java
  - SQLite
---
Comecei a trabalhar com Java há um mês, usando o framework Hibernate. O Hibernate é uma camada de persistência que pode parecer confusa no início, mas proporciona uma grande produtividade, uma vez que gerencia todo o processo de comunicação com o banco de dados, desde criação e atualização de tabelas, até chaves estrangeiras.

O NetBeans 6.8 é uma IDE que facilita muito o processo de criação, pois já vem com o Hibernate incluso. Vale lembrar que é sempre bom saber fazer o trabalho de forma braçal, para conhecer o lugar onde você está se metendo. Resolvi usar SQLite para alguns testes com o Hibernate e estou disponibilizando um exemplo básico do processo, usando o NetBeans. Let's work!

Abra o NetBeans, clique em Arquivo/Novo projeto, selecione Java/Aplicativo Java e escolha um nome para seu projeto. No meu caso ficou TesteHibernate e finalize.

O próximo passo é incluir a biblioteca do Hibernate no projeto. Na aba Projetos, clique com o botão direito em Bibliotecas/Adicionar biblioteca e selecione o Hibernate JPA. Para trabalhar com o SQlite você deve incluir também o driver JDBC do mesmo do projeto. Baixe-o aqui caso você não tenha. Após baixado, crie uma pasta chamada lib na pasta do projeto. Você pode adicionar todas as bibliotecas externas nessa pasta para facilitar a organização. Após colocar o driver na pasta, adicione-o ao projeto clicando novamente na aba Projetos/Bibliotecas/Adicionar JAR/Pasta e selecione o driver.

Agora que já temos o Hibernate e o driver do SQLite incluídos, vamos criar a conexão com o banco de dados. Clique na aba Serviços/Banco de Dados/Drivers. Se o driver do SQLite não estiver aparecendo, clique com o botão direito em Drivers/Novo driver. Em Arquivos do driver, adicione o driver da pasta lib e clique em Localizar. Deverá aparecer "org.sqlite.JDBC" no campo Classe do Driver. Dê o nome SQLite ao driver e clique em OK.

<img alt="Adicionando o driver do SQLite" src="/images/driver.jpg" style="width: 516px" />

Agora clique em Drivers/SQLite/Conectar utilizando.  
Escolha um nome de usuário, uma senha e a seguinte URL JDBC: jdbc:sqlite:teste.db. O banco estará no arquivo "teste.db" na pasta raíz do projeto.

<img alt="Conectando a um banco SQLite" src="/images/conexao.jpg" style="width: 497px" />

O próximo passo será criar a unidade de persistência do projeto. Clique em Arquivo/Novo arquivo/Persistence/Unidade de persistência. Em biblioteca de persistência, selecione o Hibernate, selecione sua conexão criada anteriormente e selecione a estratégia Criar e finalize.

<img alt="Criando uma unidade de persistência" src="/images/persistence.jpg" style="width: 604px" />

O SQLite exige um dialeto SQL específico, que não vem incluído no Hibernate. Eu encontrei um no seguinte endereço: [http://hibernate-sqlite.googlecode.com](http://hibernate-sqlite.googlecode.com). Você pode baixar somente a classe necessária, [clicando aqui](https://www.dropbox.com/s/jyeksq57uy82emk/SQLiteDialect.zip?dl=0). Extraia para a pasta "src" do projeto, ficando assim: "src/util/SQLiteDialect.java". Com a camada de persistência aberta no NetBeans (persistence.xml), clique em XML e adicione a linha do dialeto do SQLite, como mostrado abaixo: 

{% highlight java %}
	<property name="hibernate.dialect" value="util.SQLiteDialect" />
{% endhighlight %}

A camada de persistência está pronta. Vamos a criação do model.

Clique em Arquivo/Novo arquivo/Java/Classe Java e dê o nome Pessoa para a classe. O código está abaixo. Não entrarei em detalhes com as anotações utilizadas, quem sabe isso fica para um próximo post. 

{% highlight java %}  
package net.fonini.testehibernate;

import java.io.Serializable;
import java.util.Date;
import javax.persistence.Column;
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.Id;
import javax.persistence.SequenceGenerator;
import javax.persistence.Temporal;
import javax.persistence.TemporalType;

/**
* @author fonini
*/

@Entity
public class Pessoa implements Serializable {

	@Id
	@SequenceGenerator(name="seqPessoa")
	@GeneratedValue(generator="seqPessoa")
	private Integer id;

	@Column(length=50, nullable=false)
	private String nome;

	@Temporal(TemporalType.DATE)
	private Date aniversario;

	public Pessoa(){

	}

	public Date getAniversario() {
		return this.aniversario;  
	}

	public void setAniversario(Date aniversario) {
		this.aniversario = aniversario;  
	}

	public Integer getId() {
		return this.id;  
	}

	public void setId(Integer id) {
		this.id = id;
	}

	public String getNome() {
		return this.nome;  
	}

	public void setNome(String nome) {
		this.nome = nome;  
	}
}
{% endhighlight %}

Agora que temos nossa classe, vamos adicioná-la a unidade de persistência. Abra a unidade de persistência, e em "Incluir classes de entidade" clique em Adicionar e selecione a classe Pessoa. Se a classe não aparecer na listagem, verifique se as anotações estão corretas.

O próximo passo é criar uma classe de testes do JUnit para usá-la. Clique em Arquivo/Novo arquivo/Classe Java com o nome Teste e muda a localização para Pacotes de Testes. A classe irá possuir dois métodos: um deles persistirá 3 objetos Pessoa e o outro fará a listagem dos mesmos. 

{% highlight java %}
package net.fonini.testehibernate;

import java.util.Collection;
import java.util.Date;
import javax.persistence.EntityManager;
import javax.persistence.Persistence;
import org.junit.Test;

/**
* @author fonini
*/
  
public class Teste {	  
	private EntityManager em;

	public Teste(){	  
		this.em = Persistence.createEntityManagerFactory("TesteHibernatePU").createEntityManager();
	}

	@Test  
	public void inserir(){  
		// Instanciamos um objeto Pessoa, setando nome e data de nascimento  
		Pessoa p1 = new Pessoa();  
		p1.setNome("Jonnas Fonini");  
		p1.setAniversario(new Date());

		Pessoa p2 = new Pessoa();  
		p2.setNome("Luana Fonini");
		p2.setAniversario(new Date());

		Pessoa p3 = new Pessoa();  
		p3.setNome("Fulano de Tal");  
		p3.setAniversario(new Date());

		// Iniciamos a transação  
		em.getTransaction().begin();  

		// Aqui persistimos os objetos recém criados
		em.persist(p1);
		em.persist(p2);
		em.persist(p3);
  
		// E aqui efetuamos definitivamente a transação  
		em.getTransaction().commit();
	}

	@Test  
	public void listar(){	  
		Collection <Pessoa> lista = em.createQuery("from Pessoa").getResultList();

		for (Pessoa p : lista){
			System.out.println(p.getId() + " -; " + p.getNome() + " -; " + p.getAniversario());
		}
	}
}
{% endhighlight %}

Execute os testes pressionando SHIFT+F6 e veja os resultados. Se os testes atingirem 100%, está tudo certo. Senão, procure a possível causa nas exceções. Se você usa um sistema Unix-like, verifique se a pasta raíz do projeto está com as permissões adequadas para a criação do banco de dados. Note que mesmo com os testes atingindo 100% de sucesso, ainda ocorreu uma exceção. Isso se deve ao fato do SQLite não possuir chave estrangeira.

Você pode [baixar o projeto completo](https://www.dropbox.com/s/tz9hg5xpvg7xrdw/HibernateSQLite.zip?dl=0), com todas as bibliotecas necessárias incluídas.

Esse foi um tutorial bem básico, apesar de longo. Agora é com você. Bom estudos.  
Abraço e até a próxima!