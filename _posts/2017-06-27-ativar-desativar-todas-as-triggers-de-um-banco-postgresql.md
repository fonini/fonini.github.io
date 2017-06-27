---
title: "Ativar/desativar todas as triggers de um banco PostgreSQL"
date: 2017-06-27 18:26:36 -0300
layout: post
author: fonini
permalink: /2017/06/27/ativar-desativar-todas-as-triggers-de-um-banco-postgresql/
tags: 
  - PostgreSQL
---

{% highlight sql %}
create or replace function fn_trigger_all(enable boolean) returns void as 
$body$
declare
table record;
begin
  for table in select relname from pg_class where relhastriggers = true and not relname like 'pg_%'
  loop
    if enable then
      execute 'alter table ' || table.relname || ' enable trigger all';
    else
      execute 'alter table ' || table.relname || ' disable trigger all';
    end if;
  end loop;

  return;
end;
$body$
language 'plpgsql';
{% endhighlight %}

Para desabilitar:
{% highlight sql %}
select fn_trigger_all(false);
{% endhighlight %}

Para habilitar novamente:
{% highlight sql %}
select fn_trigger_all(true);
{% endhighlight %}