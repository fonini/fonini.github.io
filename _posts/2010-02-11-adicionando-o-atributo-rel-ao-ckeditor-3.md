---
id: 48
title: 'Adicionando o atributo "rel" ao CKEditor 3'
date: 2010-02-11T16:14:40+00:00
author: fonini
layout: post
permalink: /2010/02/11/adicionando-o-atributo-rel-ao-ckeditor-3/
categories:
  - Sem categoria
  - Web
tags:
  - CKEditor
  - Java Script
  - Plugins
---
Como todo mundo deve saber, o atributo "target" não valida no XHTML Strict. A solução que eu uso para contornar este problema é baseada em jQuery. Se o link possuir o atributo rel="externo", o mesmo abrirá em uma nova janela. Porém, o editor que eu uso no painel de controle deste site (<a href="http://www.ckeditor.com" rel="externo">CKEditor 3</a>) não permite adicionar o atributo rel aos links, somente editando o código HTML a mão. Se tiver uns 20 links no post a tarefa se torna um saco.

Apesar da falta de café de hoje a tarde aqui na empresa (devidamente solucionada com uma pequena gambiarra na cafeteira), resolvi modificar o plugin responsável por inserir links no CKEditor e estou compartilhando com quem se interessar. Basta extrair o arquivo na pasta **plugins/link/dialogs** e usar.

Como não tinha tempo suficiente para adicionar uma funcionalidade a mais, sobrescrevi uma existente (lang), já que não uso esse atributo.

Arquivo: [mod_link_ckeditor.zip](https://www.dropbox.com/s/2dxyo5jyxif7475/mod_link_ckeditor.zip?dl=0)

Abraço e até a próxima