---
title: "Melhorando a segurança do seu SSL"
date: 2017-04-13 15:57:49 -0300
layout: post
author: fonini
permalink: /2017/04/13/melhorando-a-seguranca-do-seu-ssl/
tags: 
  - Linux
  - ssl
  - nginx
---

Você pode usar o [SSL Server Test](https://www.ssllabs.com/ssltest/) da [Qualy's SSL Labs](https://www.ssllabs.com/) para testar a 
configuração do SSL do seu servidor.

Fiz um teste com um certificado da [Let's Encrypt](https://letsencrypt.org/) em uma instância da Amazon, com servidor NGINX
e obtive nota B.

Veja abaixo algumas dicas para melhorar a nota e consequentemente, a segurança do seu servidor.

Um dos itens apontados como inseguros foi Weak Diffie-Hellman.

Para resolver este problema, digite os comandos abaixo em seu servidor:

{% highlight shell %}
openssl dhparam -out dhparams.pem 2048
{% endhighlight %}

Esse comando irá gerar uma chave PEM que você deverá guardar em um lugar seguro de sua máquina.

Feito isso, você deve informar o caminho desse arquivo ao seu servidor e também informar algumas cifras adicionais.

Veja um exemplo para o NGINX. Coloque a configuração abaixo no bloco https de sua configuração:

{% highlight shell %}
ssl_ciphers 'ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-DSS-AES128-SHA256:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA:DHE-RSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:AES:CAMELLIA:DES-CBC3-SHA:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!aECDH:!EDH-DSS-DES-CBC3-SHA:!EDH-RSA-DES-CBC3-SHA:!KRB5-DES-CBC3-SHA';

ssl_prefer_server_ciphers on;

ssl_dhparam /caminho/do/dhparams.pem
{% endhighlight %}

Em seguida, reinicie o NGINX e execute o teste do SSL Labs novamente:

{% highlight shell %}
sudo service nginx restart
{% endhighlight %}

Agora a nota do site está como B.