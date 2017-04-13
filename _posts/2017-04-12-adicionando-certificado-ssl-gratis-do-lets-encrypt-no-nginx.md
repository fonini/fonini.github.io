---
title: "Adicionando certificado SSL grátis do Let's Encrypt no NGINX"
date: 2017-04-12 17:31:16 -0300
layout: post
author: fonini
permalink: /2017/04/12/adicionando-certificado-ssl-gratis-do-lets-encrypt-no-nginx/
tags: 
  - Linux
  - nginx
---

Baixe o cerbot e dê permissão de execução:

{% highlight shell %}
wget https://dl.eff.org/certbot-auto
chmod a+x certbot-auto
{% endhighlight %}

Se preferir, coloque o certbot no PATH do sistema.

Você precisa indicar o caminho do ".well-known" do seu site, para o Let's Encrypt conseguir confirmar que o site é realmente seu.
Ajuste os caminhos de acordo com sua arquitetura.

{% highlight shell %}
server {
	listen 80;
	listen [::]:80;

	server_name meusite.com www.meusite.com;

	location ~ ^/.well-known {
		root /var/www/meusite;
	}

	location / {
		return 301 https://$server_name$request_uri;
	}
}
{% endhighlight %}

Reinicie o NGINX para carregar as novas configurações.

{% highlight shell %}
sudo service nginx restart
{% endhighlight %}


Agora você vai rodar o comando que irá validar seu domínio e obter o certificado se tudo estiver configurado corretamente:

{% highlight shell %}
sudo ./certbot-auto certonly --webroot -w /var/www/meusite -d meusite.com.br -d www.meusite.com.br
{% endhighlight %}

Se o processo for concluído com sucesso, adicione mais uma diretiva ao seu arquivo de configuração,
que será responsável por servir a versão https do seu site:

{% highlight shell %}
server {  
	listen 443 ssl;
	listen [::]:443;

	server_name meusite.com www.meusite.com;

	ssl_certificate /etc/letsencrypt/live/meusite.com/fullchain.pem;
	ssl_certificate_key /etc/letsencrypt/live/meusite.com/privkey.pem;

	location ~ ^/.well-known {
		root /var/www/meusite;
	}

	location / {
		...
	}
}
{% endhighlight %}