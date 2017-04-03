---
title: Fórmula de Haversine em PostgreSQL
date: 2017-04-03T14:00:00+00:00
author: fonini
layout: post
permalink: /2017/04/03/formula-haversine-postgresql
tags:
  - PostgreSQL
  - Haversine
  - Geo
---

A [Fórmula de Haversine](https://pt.wikipedia.org/wiki/Fórmula_de_Haversine) é usada para encontrar a distância entre 2 pontos geográficos.

Abaixo você encontra uma implementação desta fórmula em PostgreSQL, bem como um caso de uso.

{% highlight sql %}
CREATE OR REPLACE FUNCTION haversine(latitude1 numeric(10,6),longitude1 numeric(10,6), latitude2 numeric(10,6), longitude2 numeric(10,6))
RETURNS double precision AS
$BODY$
	SELECT 6371 * acos( cos( radians(latitude1) ) * cos( radians( latitude2 ) ) * cos( radians( longitude1 ) - radians(longitude2) ) + sin( radians(latitude1) ) * sin( radians( latitude2 ) ) ) AS distance
$BODY$
LANGUAGE sql;
{% endhighlight %}

Dica: Esta função retorna a distância em quilômetros. Se você quer que o retorno seja em milhas, altere a constante 6371 para 3959.


Para testar, crie a tabela abaixo:

{% highlight sql %}
CREATE TABLE bancos(
    id SERIAL NOT NULL,
    nome VARCHAR(50) NOT NULL,
    latitude NUMERIC(10,6) NOT NULL,
    longitude NUMERIC(10,6) NOT NULL,
    CONSTRAINT pk_id_banco PRIMARY KEY (id)
);
{% endhighlight %}


Insira alguns dados:

{% highlight sql %}
INSERT INTO bancos (nome, latitude, longitude) VALUES 
('Sicredi', -28.449750, -52.199235),
('Banco do Brasil', -28.450894, -52.199193),
('Caixa Ecônomica Federal', -28.451004, -52.199391),
('Itaú', -28.449365, -52.199478),
('Bradesco', -28.452599, -52.199242),
('Banrisul', -28.452159, -52.199144);
{% endhighlight %}


Supondo que você esteja na [Praça Central de Marau/RS (-28.449292, -52.199461)](https://www.google.com.br/maps/place/28%C2%B026'57.5%22S+52%C2%B011'58.1%22W/@-28.4492896,-52.2005553,18z/data=!3m1!4b1!4m5!3m4!1s0x0:0x0!8m2!3d-28.449292!4d-52.199461) e deseje ir até o banco mais próximo:

{% highlight sql %}
SELECT nome
FROM bancos
ORDER BY haversine(-28.449292, -52.199461, latitude, longitude)
{% endhighlight %}

{% highlight yaml %}
Sicredi
Itaú
Banco do Brasil
Caixa Ecônomica Federal
Banrisul
Bradesco
{% endhighlight %}


Caso queira ver a distância até todos os bancos em metros:

{% highlight sql %}
SELECT nome, haversine(-28.449293, -52.199451, latitude, longitude) * 1000
FROM bancos
{% endhighlight %}

| Nome                    | Distância (m) |
|-------------------------|---------------|
| Sicredi                 | 55.02         |
| Banco do Brasil         | 179.80        |
| Caixa Ecônomica Federal | 190.34        |
| Bradesco                | 368.17        |
| Banrisul                | 320.09        |
| Itaú                    | 113.93        |