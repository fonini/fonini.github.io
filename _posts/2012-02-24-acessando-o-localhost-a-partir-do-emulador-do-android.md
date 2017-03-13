---
id: 394
title: Acessando o localhost a partir do emulador do Android
date: 2012-02-24T09:06:41+00:00
author: fonini
layout: post
permalink: /2012/02/24/acessando-o-localhost-a-partir-do-emulador-do-android/
categories:
  - Android
  - Sem categoria
tags:
  - Android
---
Um requisito muito comum de um aplicativo desenvolvido para a plataforma Android é que o mesmo acesse um web service para troca de informações. No momento do desenvolvimento do aplicativo, geralmente o web service fica na mesma máquina em que se encontra o emulador. 

Como faço pra acessar o localhost da máquina através do emulador? Usando "localhost" na string de conexão? Não funciona. 

Uso o IP da minha máquina para conectar? Pode até funcionar, mas e se você estiver desconectado? 

Neste caso, basta usar o IP mágico, **10.0.2.2**. Através deste endereço, o emulador Android saberá que deve acessar o localhost da sua máquina, independente da configuração da sua rede e mesmo que você estiver desconectado. 

Tente você mesmo. Com seu servidor web iniciado, acesse o endereço através do browser do emulador Android. 

Saudações!