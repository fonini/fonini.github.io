---
title: Como instalar e configurar o PostgreSQL 8.4 no Ubuntu
date: 2010-02-05T10:28:04+00:00
author: fonini
layout: post
permalink: /2010/02/05/como-instalar-e-configurar-o-postgresql-8-4-no-ubuntu/
tags:
  - Linux
  - PostgreSQL
  - Ubuntu
---
O PostgreSQL é sem dúvidas um dos melhores SGBDs open source da atualidade. Robusto, confiável, agrega várias características que deixam muitos SGBD's pagos no chinelo. Eu, particularmente, uso em todos os projetos aqui na empresa, pois alguns sistemas demandam um rígido controle de consistência dos dados, integridade referencial, etc, e o PostgreSQL me dá essa segurança.

Lembro que sofri bastante nas primeiras vezes que fui instalar e configurar o Postgres no meu Ubuntu, por isso resolvi compartilhar essa experiência que pode ser útil para mais pessoas. Let's work!

No terminal, digite:

{% highlight c %}sudo apt-get install postgresql-8.4 postgresql-client-8.4 postgresql-client-common postgresql-common postgresql-contrib-8.4{% endhighlight %}

Feito isso, vamos configurar o Postgres. Edite o arquivo /etc/postgresql/8.4/main/pg_hba.conf

{% highlight c %}sudo gedit /etc/postgresql/8.4/main/pg_hba.conf{% endhighlight %}

Essa etapa permitirá a administração para outros usuários e não só para o usuário postgres.
  
Localize a seguinte linha:
  
**# Database administrative login by UNIX sockets**
  
Agora substitua a linha imediatamente abaixo desta, com o seguinte conteúdo:
  
**local all all trust**

Agora vamos permitir o acesso para seus usuários. Localize a linha
  
**# "local" is for Unix domain socket connections only**
  
e substitua a linha abaixo dela com o seguinte conteúdo:
  
**local all all trust**

Para liberar o acesso remoto procure a seguinte linha:
  
**# IPv4 local connections:**
  
e substitua a linha logo abaixo por esta:
  
**host all all 0.0.0.0/0 trust**

A primeira parte está concluída. Agora edite o arquivo postgresql.conf, que está localizado na mesma pasta:

{% highlight c %}sudo gedit /etc/postgresql/8.4/main/postgresql.conf{% endhighlight %}

Procure esta linha:

**# listen_addresses = 'localhost'**

Descomente a linha e troque 'localhost' por '*', assim qualquer computador poderá acessar o Postgres.

A linha ficará assim:

**listen_addresses = '*'**

Agora é só reiniciar o servidor com o seguinte comando:

{% highlight c %}/etc/init.d/postgresql-8.4 restart{% endhighlight %}

Se você quiser mudar a senha do usuário postgres, digite os seguintes comandos no terminal:

{% highlight c %}sudo su postgres -c psql postgres
# ALTER USER postgres WITH PASSWORD 'SuaNovaSenha';
# q{% endhighlight %}

Pronto! Seu PostgreSQL está pronto para o uso! Agora você pode instalar um software para gerenciar o banco de dados. Os mais conhecidos são o PgAdmin3 e o phpPgAdmin (necessita instalar Apache + PHP).
  
Qualquer dúvida comente ou entre em contato.

Abraço e até a próxima!