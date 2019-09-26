---
title: "Executar SQL em todos os bancos de dados"
date: 2019-09-26 09:40:46 -0300
layout: post
author: fonini
permalink: /2019/09/26/executar-sql-em-todos-os-bancos-de-dados/
tags: 
  - postgresql
---

Esse comando vai gerar diversos comandos psql para serem executados no terminal, cada um deles gerando um arquivo CSV, usando o Tenant ID como nome.
Útil para gerar estatísticas com dados de diversos bancos.

{% highlight sql %}
select  'psql -d ' || d.database_name ||' -c "COPY (select ''Test'' as type from table) to ''/var/lib/pgsql/table/' || t.id ||'.csv'' delimiter'',''" '
from tenant t
inner join database d on d.tenant_id = t.id
order by t.id
{% endhighlight %}

Após, é só juntar os arquivos em um só.

{% highlight shell %}
cd /var/lib/pgsql
cat table/* > table.csv
{% endhighlight %}