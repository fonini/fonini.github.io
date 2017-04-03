---
title: Plugin para Rhythmbox para buscar letras de músicas no Vagalume
date: 2010-03-17T08:53:14+00:00
author: fonini
layout: post
permalink: /2010/03/17/plugin-para-rhythmbox-para-buscar-letras-de-musicas-no-vagalume/
tags:
  - Linux
  - Plugins
---
Fiz uma extensão para o plugin Lyrics do Rhythmbox. Esse plugin busca letras de músicas de alguns sites na internet, porém é bem difícil encontrar letras de músicas nacionais. 

Então resolvi criar essa extensão para o plugin, que busca letras no site [Vagalume](http://www.vagalume.com.br). É a primeira versão do plugin e pode conter erros, pois eu não sabia nada de Python antes de escrever o plugin. 

Você pode encontrar versões mais atualizadas daqui a algum tempo no [GitHub](http://github.com/fonini/VagalumeParser).

**Instalação**

Baixe a extensão [aqui](https://www.dropbox.com/s/yvw5qt1fjr1b5sq/vagalume-parser.zip?dl=0) e extraia para uma pasta de sua preferência. Depois é só substituir (como root) os arquivos da pasta /usr/lib/rhythmbox/plugins/lyrics por esses que você acabou de baixar.

Feito isso, entre no Rhythmbox, vá em Editar/Plugins, encontre o plugin Letras de Músicas, ative caso esteja desativado e selecione o site vagalume.com.br na listagem.

Abraço e até a próxima!