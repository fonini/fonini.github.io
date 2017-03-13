---
id: 54
title: Usando SQLite com Java
date: 2010-02-18T08:57:32+00:00
author: fonini
layout: post
permalink: /2010/02/18/usando-sqlite-com-java/
categories:
  - Sem categoria
  - Web
tags:
  - Java
  - SQLite
---
Por essa nem eu esperava. Estou me aventurando no mundo do Java, depois de tudo que eu falei mal dessa linguagem. Mas fazer o que, não dá pra trabalhar com uma linguagem só :p No fundo, Java é muito legal. Depois de aprender a sintaxe básica do Java, resolvi me aventurar também no SQLite e de quebra, matei dois coelhos com uma pedrada só.

O SQLite é uma biblioteca escrita em C que fornece um banco de dados que dispensa configurações/ajustes. É criado um novo arquivo no disco e a biblioteca se encarrega de todas as operações sobre ele, dispensando um processo separado para o SGBD, como é comum na maioria dos bancos de dados. Para mais informações, consulte o site oficial (<a href="http://sqlite.org" rel="externo">http://sqlite.org</a>).

O exemplo abaixo é extremamente básico, pois ainda estou aprendendo as manhas. Let's work!

Para começar, baixe a biblioteca do SQLite <a href="http://www.zentus.com/sqlitejdbc" rel="externo">aqui</a>. O .jar disponível funciona tanto em Linux, como em Windows e Mac. Inclua a biblioteca em seu projeto. No caso do <a href="http://netbeans.org" rel="externo">NetBeans</a>, procure a aba Projetos, selecione seu projeto, vá em Bibliotecas, botão direito e selecione Adicionar JAR/Pasta, informando a localização do arquivo baixado.

O exemplo baseia-se em um cadastro de pessoas, contendo nome e idade. São três classes: Pessoa (o "The book is on the table" da orientação a objetos, todo mundo que está aprendendo OO faz essa classe), SQLite, onde estão implementados os métodos para inserção e listagem e a classe Exemplo, a classe principal do projeto.

**Classe Pessoa**

{% highlight java %}
package testesqlite;

public class Pessoa {
	private int idade;
	private String nome;

	public Pessoa(String nome, int idade) {
		this.nome = nome;  
		this.idade = idade;
	}

	public String getNome() {	  
		return this.nome;
	}

	public void setNome(String nome) {	  
		this.nome = nome;
	}

	public int getIdade() {
		return this.idade;
	}

	public void setIdade(int idade) {
		this.idade = idade;
	}
}
{% endhighlight %}

**Classe SQLite**

{% highlight java %}
package testesqlite;

import java.sql.*;
import java.util.Vector;

public class SQLite {
	private Connection conn;
	private Statement stm;

	public SQLite(String arquivo) throws SQLException, ClassNotFoundException {
		Class.forName("org.sqlite.JDBC");

		this.conn = DriverManager.getConnection("jdbc:sqlite:" + arquivo);
		this.stm = this.conn.createStatement();
	}

	public void initDB() {	  
		try {
			// Remove e cria a tabela a cada execução. Mero exemplo

			this.stm.executeUpdate("DROP TABLE IF EXISTS pessoas");

			this.stm.executeUpdate("CREATE TABLE pessoas ("
				+ "nome varchar(70) PRIMARY KEY NOT NULL,"
				+ "idade integer);");
		} 
		catch (SQLException e) {
			e.printStackTrace();  
		}  
	}

	public void insert(Pessoa pessoa) {		  
		try {		  
			this.stm = this.conn.createStatement();
		  
			this.stm.executeUpdate("INSERT INTO pessoas VALUES ("
				+ pessoa.getNome() + ","
				+ pessoa.getIdade() + ")");
		}
		catch (SQLException e) {
			e.printStackTrace();
		}
	}

	public void removePessoa(String nome) {		  
		try {		  
			this.stm = this.conn.createStatement();

			this.stm.executeUpdate("DELETE FROM pessoas WHERE nome = " + nome);
		}
		catch (SQLException e) {
			e.printStackTrace();  
		}  
	}

	public Vector getAll() {
		Vector lista = new Vector();	  
		ResultSet rs;

		try {
			rs = this.stm.executeQuery("SELECT * FROM pessoas ORDER BY idade");

			while (rs.next()) {
				lista.add(new Pessoa(rs.getString("nome"), rs.getInt("idade")));
			}

			rs.close();

		}
		catch (SQLException e) {
			e.printStackTrace();
		}

		return lista;
	}
}
  
{% endhighlight %}

**Classe Exemplo (main)**

{% highlight java %}
package testesqlite;

import java.util.Iterator;

public class Exemplo {
	public static void main(String[] args) {
		try {
			SQLite dbCon = new SQLite("pessoas.db");
			dbCon.initDB();

			dbCon.insert(new Pessoa("Jonnas", 19));
			dbCon.insert(new Pessoa("Fulano", 20));
			dbCon.insert(new Pessoa("Beltrano", 10));

			Exemplo.listaTodos(dbCon);

			System.out.println("Removemos a pessoa com o nome Fulano e listamos novamenten");
			dbCon.removePessoa("Fulano");

			Exemplo.listaTodos(dbCon);
		}
		catch (Exception e) {
			e.printStackTrace();
		}  
	}

	public static void listaTodos(SQLite dbCon) {
		Iterator it = dbCon.getAll().iterator();
		Pessoa hs;

		while (it.hasNext()) {
			hs = (Pessoa) it.next();

			System.out.println("Nome:" + hs.getNome());
			System.out.println("Idade:" + hs.getIdade() + "n");
		}
	}
}
{% endhighlight %}

O código tá bem amador ainda, mas dá pra ter uma noção de como funciona o SQLite com Java. É criado um arquivo chamado "pessoas.db" que será o banco de dados. É criada uma tabela "pessoas" e inserido três registros nela. Todos os registros são listados, remove-se uma das pessoas e lista-se novamente.

Baixe [aqui](https://www.dropbox.com/s/87c3ax23ljrwztw/TesteSQLite.rar?dl=0) o projeto criado no NetBeans (com a biblioteca já incluída).

Abraço e até a próxima!