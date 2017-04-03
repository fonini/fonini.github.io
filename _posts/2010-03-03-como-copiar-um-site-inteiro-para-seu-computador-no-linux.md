---
title: Como copiar um site inteiro para seu computador no Linux
date: 2010-03-03T09:16:03+00:00
author: fonini
layout: post
permalink: /2010/03/03/como-copiar-um-site-inteiro-para-seu-computador-no-linux/
tags:
  - Linux
---
De volta, após alguns dias sem postar devido a morte da minha vó, Cecília, 93 anos. Descanse em paz, minha vó querida.

Mas vamos lá!

Tenho visto muitas dúvidas de usuários Linux em como copiar um site inteiro para o computador, para acesso offline. Uso o mesmo software dos tempos de Windows, o HTTrack Website Copier, disponível no repositório.

Para instalar: 

{% highlight shell %}sudo apt-get install webhttrack{% endhighlight %}

Para usuários de outras distros, existem mais versões no [site oficial](http://www.httrack.com/page/2/en/index.html).

O programa estará disponível no menu Aplicativos/Internet/WebHTTrack Website Copier. O programa foi escrito em C e roda diretamente no browser.

Após aberto, selecione um idioma e crie um novo projeto. O legal desse programa é que você pode continuar a cópia de um site abortado anteriormente, bastando seleciona-lo no início do programa, ao invés de criar um novo projeto. Lembre de especificar o local para onde o site será baixado em seu computador.

Após criar um novo projeto, adicione o endereço do site e avance. Também é possível submeter uma lista, em formato texto, contendo links a serem baixados. Depois de ter configurado todas as opções, o software inicia a cópia do site.

Não recomendo o uso deste programa pois gera um tráfego imenso no servidor do site e isso pode afetar usuários com limite de tráfego mensal baixo. Use com moderação somente em casos necessários.

Abraço e até a próxima!