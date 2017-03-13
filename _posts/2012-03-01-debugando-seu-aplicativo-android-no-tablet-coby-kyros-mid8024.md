---
id: 411
title: Debugando seu aplicativo Android no tablet Coby Kyros Mid8024
date: 2012-03-01T13:53:20+00:00
author: fonini
layout: post
guid: http://www.fonini.net/blog/?p=411
permalink: /2012/03/01/debugando-seu-aplicativo-android-no-tablet-coby-kyros-mid8024/
categories:
  - Android
  - Sem categoria
tags:
  - Android
  - Driver
  - Xing Ling
---
Hoje precisei instalar uma app Android que desenvolvi no tablet de um cliente. Conectei o bicho no USB do computador e nada de reconhecer. Olhei no Gerenciador de Dispositivos do Windows 7 (infelizmente preciso trabalhar no maldito) e vi que existia um dispositivo não reconhecido, o **S5P OTG-USB** . 

Após alguma procura, localizei o driver necessário, esse [aqui](http://www.driveridentifier.com/scan/driver_file_detail.php?inf_file_id=510504&md5=830fc6ecaf4549aac2fe3a52df8745d4&scanid=1E91495F3AD149598DF2EFE444EC31B1&item_id=278631742&hardware_id=USBVID_18D1%26PID_4E22%26MI_01). Agora, basta extrair os arquivos para alguma pasta, ir novamente no Gerenciador de Dispositivos, clicar com o botão direito no S5P OTG-USB, clicar em Atualizar driver (ou instalar driver, se necessário) e localizar a pasta dos drivers. 

Pronto. Para testar se funcionou, execute comando: **adb devices** e veja se seu dispositivo foi reconhecido. No meu caso, ele foi reconhecido como **MID_Serials device**. 

Agora basta debugar seu aplicativo. 

No no meu caso, eu fazia o download da app, começava a instalação, mas aparecia a mensagem: "**O aplicativo não foi instalado**". Fiz o processo para debugar o aplicativo e descobri que o tablet não tinha a lib do Google Maps. O erro era esse: INSTALL_FAILED_MISSING_SHARED_LIBRARY. 

O processo de debug direto no dispositivo me fez perceber o problema na hora. Se não tivesse debugado, estaria até agora tentando entender o erro. Fica a dica. 

[Download do driver](http://www.driveridentifier.com/scan/driver_file_detail.php?inf_file_id=510504&md5=830fc6ecaf4549aac2fe3a52df8745d4&scanid=1E91495F3AD149598DF2EFE444EC31B1&item_id=278631742&hardware_id=USBVID_18D1%26PID_4E22%26MI_01) 

[Link alternativo](http://dl.dropbox.com/u/9937691/android_usb_driver.zip) 

Grande abraço!