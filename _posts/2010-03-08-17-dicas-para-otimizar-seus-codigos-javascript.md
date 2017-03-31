---
title: 17 dicas para otimizar seus códigos JavaScript
date: 2010-03-08T09:11:12+00:00
author: fonini
layout: post
permalink: /2010/03/08/17-dicas-para-otimizar-seus-codigos-javascript/
categories:
  - Sem categoria
  - Web
tags:
  - Java Script
---
Reuni algumas dicas da Internet que considero úteis para compartilhar com o pessoal. As dicas abrangem desde melhores práticas de programação até aumento de performance do código.

**1** - Inicializar arrays e objetos com a = [] e b = {} é mais rápido do que a = new Array e b = new Object

**2** - ~~(1  *  "20.7") é mais rápido que parseInt(20.7)

**3** - Uma das melhores maneiras de aumentar a performance de seus códigos JavaScript é usar o **cache de objetos**. O seguinte código, por exemplo, é ineficiente pois acessa o objeto diretamente várias vezes. Se você tiver 15 imagens na página, serão 30 acessos ao objeto.

{% highlight js %} 
for (i = 0; i < document.images.length; i++){
	document.images[i].src = "imagem.jpg";
} 
{% endhighlight %}
  
Uma forma de melhorar o desempenho deste código é guardar o objeto em uma variável, como no exemplo abaixo. Nesse caso o browser não precisa acessar o DOM novamente a cada iteração do loop.

{% highlight js %}
var imagens = document.images;
var tam = imagens.length;

for (i = 0; i < tam; i++){	  
	imagens[i].src = "imagem.jpg";
}
{% endhighlight %}

**4** - Use === ao invés de ==

O JavaScript usa dois diferentes operadores de igualdade, quando precisamos comparar dois valores e também seus tipos de dados se faz necessário o uso do ===, agora quando precisamos comparar apenas seus valores mas não o tipo de dados podemos usar ==

**5** - Reduza a quantidade de váriaveis globais

Reduzindo a quantidade de variáveis globais você reduz muito a chance de conflito entre scripts diferentes, bibliotecas ou até no mesmo código.

**6** - Não declare variáveis dentro de laços de repetição**
  
Já vi casos onde a variável container havia sido declarada dentro do loop, reduzindo a performance do código. Guardar o tamanho do array em uma variável para usar no "for" também é recomendado, pois calcula o tamanho somente uma vez

{% highlight js %}
var container = document.getElementById('minhadiv');
var tam = vetor.length;

for(var i = 0; i < tam; i++) {	  
	container.innerHtml += i + '<br />';
}
  
{% endhighlight %}

**7** - Use chaves e ponto-e-vírgula em seus códigos.
  
Retirar esses elementos pode reduzir alguns bytes do seu código, mas o uso deles torna o código mais legível. Seu uso também é muito importante caso você use algum otimizador de JavaScript, pois o mesmo poderá se perder caso você não tenha delimitado o final de cada linha de código.

**8** - Se possível, use apenas uma biblioteca JavaScript em sua página.
Já vi sites que usam Prototype, jQuery e MooTools na mesma página. Pesquise bastante antes de utilizar uma biblioteca JavaScript, procure uma que se adapte as suas necessidades, evitando assim a inclusão de novas bibliotecas, já que a grande maioria delas tem as mesmas funcionalidades.

**9** - Coloque o JavaScript em arquivos externos sempre que possível, ao invés de colocar o código diretamente no HTML.** Com essa técnica o browser não precisa carregar novamente o código da página, pois o mesmo estará no cache. Tente também reduzir a quantidade de arquivos externos, combinando os códigos em um único arquivo. Isso economiza diversas requisições HTTP, cruciais para o desempenho do site.

**10** - Use blocos CDATA para evitar erros de validação.
  
O validador pode identificar uma comparação como sendo a abertura de uma tag HTML que não será fechada, invalidando seu código, como por exemplo if (var < 10). Usando blocos CDATA, como no exemplo abaixo, evitamos que isto aconteça.</p> 

**11** - Use a estrutura de controle switch ao invés de múltiplos if/elses aninhados.

{% highlight js %}
if (dia == 2){
	...
}
elseif (dia == 3){ 
	...
}
elseif (dia == 4){ 
	...
}
{% endhighlight %}
  
Usando switch, o código se torna muito mais legível, além de facilitar na hora da manutenção.

{% highlight js %}
switch (dia){
	case 2:	  
		...  
		break;
	case 3:	  
		...
		break
	case 4:
		...
		break;
	default:	  
		...
}
{% endhighlight %}

**12** - Use o atributo defer para indicar o uso scripts externos no IE
  
A função do atributo do defer é avisar o script que está sendo requisitado externamente para esperar até que a página seja carregada ou o DOM esteja preparado. O mesmo pode ser realizado através de bons métodos não-obstrutivos via JavaScript, que usualmente inclui códigos que previnem a execução de scripts antes que o DOM seja carregado por completo.
  
A vantagem do defer ocorre quando utilizamos o Internet Explorer, tendo em vista que é único browser que suporta o atributo defer. Então, se você precisa de um rápido script que rode únicamente e exclusivamente no Internet Explorer, e você não quer que ele execute antes que o DOM esteja preparado, então simplesmente adicione defer="defer" na sua tag &lt;script&gt; e ela irá rapidamente tratar o seu problema. Corrigir a transparência de arquivos PNG no IE6 é um exemplo prático do uso do defer.  
Mas lembre-se que o atributo defer deve ser usado quando escondemos um script de outros browsers com o uso dos comentários condicionais (conditional comments) para que afete somente os navegadores da Microsoft. De outra maneira, o script vai rodar normalmente em outros browsers.

**13** - Evite usar palavras reservadas do JavaScript em nomes de funções e/ou variáveis. As principais são essas:

{% highlight js %}
break
case
catch
continue
default
delete
do
else
finally
for
function
if
in
instanceof
new
return
switch
this
throw
try
typeof
var
void
while
with
{% endhighlight %}

**14** - Utilize compressão de código

Comprimir o código pode reduzir consideravelmente o tamanho do mesmo, reduzindo o tempo de carregamento da página. Existem muitos compressores de código online que realizam o serviço para você. O código também pode ser comprimido no Apache, através de um arquivo .htaccess com o conteúdo similar a esse:

{% highlight xml %}
<FilesMatch ".js$">
	AddHandler application/x-httpd-php .js
</FilesMatch>
{% endhighlight %}

**15** - A menos que você esteja usando alguma biblioteca JavaScript que somente execute o código quando o DOM estiver carregado, **sempre inclua seu código JavaScript no final da página**. Isso evita que o código seja executado antes do carregamento da página, causando efeitos indesejáveis e/ou lentidão.

**16** - Use uma biblioteca de JavaScript cross-browser.
  
Atualmente existem várias bibliotecas que fazem o trabalho sujo da incompatibilidade entre browsers para você e reduzem a quantidade de linhas de código, bastando você se concentrar na lógica para resolver o problema sem se preocupar se o código vai funcionar em todos os browsers. A minha preferida é a jQuery, cujo lema é "Write less, do more" (escreva menos, faça mais).

**17** - Comente seu código sempre que possível.
  
Isso evita muita dor de cabeça no futuro, quando for dar manutenção no código.