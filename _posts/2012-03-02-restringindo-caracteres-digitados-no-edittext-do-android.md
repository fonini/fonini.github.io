---
title: Restringindo caracteres digitados no EditText do Android
date: 2012-03-02T10:51:24+00:00
author: fonini
layout: post
permalink: /2012/03/02/restringindo-caracteres-digitados-no-edittext-do-android/
categories:
  - Android
  - Sem categoria
tags:
  - Android
---
Desenvolvendo em Android, temos alguns casos em que precisamos restringir os caracteres que são permitidos em campos como o EditText. 

Um exemplo, é um campo que aceite valores como **1,80** e **1.80**. No caso, se a restrição fosse somente números com . (ponto) como separador decimal, bastaria definir o **android:inputType** como **numberDecimal**. Porém, número com , (vírgula) como separador não iriam funcionar. 

Para tarefas como essa, o atributo **android:digits** está aí para salvar a pátria. Basta definir nele quais dígitos serão permitidos naquele EditText e o Android cuida do resto. 

Exemplo: 

**Permitir somente números, tanto com . como , como separadores decimais:**

{% highlight xml %}
<EditText android:digits="1234567890.," android:layout_width="wrap_content" android:layout_height="wrap_content" />
{% endhighlight %}

Fácil, não? 

Essa solução também é util para ser usada em conjunto com o android:inputType="numberDecimal". Nesse caso, é apresentado o teclado numérico, permitindo que vírgulas também sejam incluídas. 

Exemplo:

{% highlight xml %} 
<EditText android:digits="1234567890.," android:inputType="numberDecimal" android:layout_width="wrap_content" android:layout_height="wrap_content" />
{% endhighlight %}

### Outros exemplos

**Números hexadecimais:**

{% highlight xml %}
<EditText android:digits="abcdef1234567890" android:layout_width="wrap_content" android:layout_height="wrap_content" />
{% endhighlight %}

**Somente números pares:**

{% highlight xml %}
<EditText android:digits=02468" android:inputType="number" android:layout_width="wrap_content" android:layout_height="wrap_content" />
{% endhighlight %}

Abraço!