---
title: Configuração do nginx com Cloudflare
date: 2017-04-03T08:09:50+00:00
author: fonini
layout: post
permalink: /2017/04/03/configuracao-do-nginx-com-cloudflare
categories:
  - Sem categoria
  - Linux
---

Se você utiliza [Cloudflare](https://cloudflare.com) com nginx em seus sites/sistemas, o script abaixo permite que você libere somente os IPs da Cloudflare
no nginx. Dessa forma, acessos diretos ao IP de sua instância serão bloqueados.

Isso também pode ser feito no iptables (quem sabe num post em breve).

Além de liberar somente acessos oriundos da Cloudflare, o script restaura o IP real do visitante.
Como o Cloudflare funciona como um proxy, o IP que chega nos headers da requisição é um dos IPs do Cloudflare e não o IP real do visitante.

Porém, o IP real é enviado em um header diferente, o CF-Connecting-IP. O script lê esse header, quando for proveniente da Cloudflare e atualiza o header 
do IP real.


{% highlight shell %}
#!/bin/bash
NGINX_CONFIG=/etc/nginx/conf.d

out="$({
	printf "#IPv4\n"
	curl -s https://www.cloudflare.com/ips-v4
	printf "\n\n#IPv6\n"
	curl -s https://www.cloudflare.com/ips-v6
})"

echo "$out" | sed -r 's/^([^#].+)$/set_real_ip_from \1;/g' > "$NGINX_CONFIG"/cloudflare-real-ips.conf

echo "$out" | sed -r 's/^([^#].+)$/allow \1;/g' > "$NGINX_CONFIG"/cloudflare-allow.conf
{% endhighlight %}

Lembre de alterar o caminho da pasta de configuração do nginx.

Rode o script e inclua os arquivos criados por ele na configuração do nginx.

Exemplo:

{% highlight shell %}
# /etc/nginx/conf.d/meuserver.com.conf

server {
	server_name seuserver.com;

	listen 443 ssl http2;
	listen [::]:443 http2;

	# Liberar somente acessos a partir da Cloudflare
	include /etc/nginx/conf.d/cloudflare-allow.conf;
	deny all;

	# Atualizar IP real do visitante
	real_ip_header CF-Connecting-IP;
	include /etc/nginx/conf.d/cloudflare-real-ips.conf;

	...
}
{% endhighlight %}

Coloque o script no cron para ser executado periodicamente, pois é possível que os IPs da Cloudflare mudem.