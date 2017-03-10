---
id: 79
title: 17 dicas para omitizar seus códigos JavaScript
date: 2010-03-08T09:11:12+00:00
author: fonini
layout: post
guid: http://www.fonini.net/blog/?p=79
permalink: /2010/03/08/17-dicas-para-omitizar-seus-codigos-javascript/
categories:
  - Sem categoria
  - Web
tags:
  - Java Script
---
Reuni algumas dicas da Internet que considero úteis para compartilhar com o pessoal. As dicas abrangem desde melhores práticas de programação até aumento de performance do código.

<span style="font-size: 14px;"><strong>1 </strong></span>&#8211; **Inicializar arrays e objetos** com a = [] e b = {} é mais rápido do que a = new Array e b = new Object

<span style="font-size: 14px;"><strong>2 </strong></span>&#8211; ~~(1&nbsp; *&nbsp; &#8220;20.7&#8221;) é mais rápido que parseInt(20.7)

<span style="font-size: 14px;"><strong>3</strong></span> &#8211; Uma das melhores maneiras de aumentar a performance de seus códigos JavaScript é usar o **cache de objetos**. O seguinte código, por exemplo, é ineficiente pois acessa o objeto diretamente várias vezes. Se você tiver 15 imagens na página, serão 30 acessos ao objeto.

[js]
  
for (i = 0; i < document.images.length; i++)
	  
document.images[i].src = "imagem.jpg";
  
[/js]
  

  
Uma forma de melhorar o desempenho deste código é guardar o objeto em uma variável, como no exemplo abaixo. Nesse caso o browser não precisa acessar o DOM novamente a cada iteração do laço.

[js]
  
var imagens = document.images;
  
var tam = imagens.length;
  
for (i = 0; i < tam; i++){
	  
imagens[i].src = "imagem.jpg";
  
}
  
[/js]

**<span style="font-size: 14px;">4</span> &#8211; Use === ao invés de ==**
  
O JavaScript usa dois diferentes operadores de igualdade, quando precisamos comparar dois valores e também seus tipos de dados se faz necessário o uso do ===, agora quando precisamos comparar apenas seus valores mas não o tipo de dados podemos usar ==

**<span style="font-size: 14px;">5</span> &#8211; Reduza a quantidade de váriaveis globais**
  
Reduzindo a quantidade de variáveis globais você reduz muito a chance de conflito entre scripts diferentes, bibliotecas ou até no mesmo código.

**<span style="font-size: 14px;">6</span> &#8211; Não declare variáveis dentro de laços de repetição**.
  
Já vi casos onde a variável container havia sido declarada dentro do loop, reduzindo a performance do código. Guardar o tamanho do array em uma variável para usar no &#8220;for&#8221; também é recomendado, pois calcula o tamanho somente uma vez

[js]
  
var container = document.getElementById(&#8216;minhadiv&#8217;);
  
var tam = vetor.length;
  
for(var i = 0; i < tam; i++) {
	  
container.innerHtml += i + &#8216;<br />&#8217;;
  
}
  
[/js]

**<span style="font-size: 14px;">7</span> &#8211; Use chaves e ponto-e-vírgula em seus códigos.** 
  
Retirar esses elementos pode reduzir alguns bytes do seu código, mas o uso deles torna o código mais legível. Seu uso também é muito importante caso você use algum otimizador de JavaScript, pois o mesmo poderá se perder caso você não tenha delimitado o final de cada linha de código.

<span style="font-size: 14px;"><strong>8</strong></span> **&#8211; Se possível, use apenas uma biblioteca JavaScript em sua página.**  
Já vi sites que usam Prototype, jQuery e MooTools na mesma página. Pesquise bastante antes de utilizar uma biblioteca JavaScript, procure uma que se adapte as suas necessidades, evitando assim a inclusão de novas bibliotecas, já que a grande maioria delas tem as mesmas funcionalidades.

**<span style="font-size: 14px;">9</span> &#8211; Coloque o JavaScript em arquivos externos sempre que possível, ao invés de colocar o código diretamente no HTML.** Com essa técnica o browser não precisa carregar novamente o código da página, pois o mesmo estará no cache. Tente também reduzir a quantidade de arquivos externos, combinando os códigos em um único arquivo. Isso economiza diversas requisições HTTP, cruciais para o desempenho do site.

**<span style="font-size: 14px;">10</span> &#8211; Use blocos CDATA para evitar erros de validação.** 
  
O validador pode identificar uma comparação como sendo a abertura de uma tag HTML que não será fechada, invalidando seu código, como por exemplo if (var < 10). Usando blocos CDATA, como no exemplo abaixo, evitamos que isto aconteça.</p> 

**<span style="font-size: 14px;">11</span> &#8211; Use a estrutura de controle switch ao invés de múltiplos if/elses aninhados.**

[js]
  
if (dia == 2){
  
&#8230;
  
}
  
elseif (dia == 3){
  
&#8230;
  
}
  
elseif (dia == 4){
  
&#8230;
  
}
  
[/js]
  

  
Usando switch, o código se torna muito mais legível, além de facilitar na hora da manutenção.

[js]
  
switch (dia){
	  
case 2:
		  
&#8230;
		  
break;
	  
case 3:
		  
&#8230;
		  
break;
	  
case 4:
		  
&#8230;
		  
break;
	  
default:
		  
&#8230;
  
}
  
[/js]

**  
<span style="font-size: 14px;">12</span> &#8211; Use o atributo defer para indicar o uso scripts externos no IE**
  
A função do atributo do defer é avisar o script que está sendo requisitado externamente para esperar&nbsp; até que a página seja carregada ou o DOM esteja preparado. O mesmo pode ser realizado através de bons métodos não-obstrutivos via JavaScript, que usualmente inclui códigos que previnem a execução de scripts antes que o DOM seja carregado por completo.
  
A vantagem do defer ocorre quando utilizamos o Internet Explorer, tendo em vista que é único browser que suporta o atributo defer. Então, se você precisa de um rápido script que rode únicamente e exclusivamente no Internet Explorer, e você não quer que ele execute antes que o DOM esteja preparado, então simplesmente adicione defer=&#8221;defer&#8221; no sua tag <script> e ela irá rapidamente tratar o seu problema. Corrigir a transparência de arquivos PNG no IE6 é um exemplo prático do uso do defer.  
Mas lembre-se que o atributo defer deve ser usado quando escondemos um script de outros browsers com o uso dos comentários condicionais (conditional comments) para que afete somente os navegadores da Microsoft. De outra maneira, o script vai rodar normalmente em outros browsers.

**<span style="font-size: 14px;">13 </span>&#8211; Evite usar palavras reservadas do JavaScript em nomes de funções e/ou variáveis. As principais são essas:**

[js]
  
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
  
[/js]

**<span style="font-size: 14px;">14</span> &#8211; Utilize compressão de código.
  
** Comprimir o código pode reduzir consideravelmente o tamanho do mesmo, reduzindo o tempo de carregamento da página. Existem muitos compressores de código online que realizam o serviço para você. O código também pode ser comprimido no Apache, através de um arquivo .htaccess com o conteúdo similar a esse:

[xml]
  
<FilesMatch ".js$">
	  
AddHandler application/x-httpd-php .js
  
</FilesMatch>
  
[/xml]

<span style="font-size: 14px;"><strong>15</strong></span> &#8211; A menos que você esteja usando alguma biblioteca JavaScript que somente execute o código quando o DOM estiver carregado, **sempre inclua seu código JavaScript no final da página**. Isso evita que o código seja executado antes do carregamento da página, causando efeitos indesejáveis e/ou lentidão.

<span style="font-size: 14px;"><strong>16</strong></span> **&#8211; Use uma biblioteca de JavaScript cross-browser.** 
  
Atualmente existem várias bibliotecas que fazem o trabalho sujo da incompatibilidade entre browsers para você e reduzem a quantidade de linhas de código, bastando você se concentrar na lógica para resolver o problema sem se preocupar se o código vai funcionar em todos os browsers. A minha preferida é a jQuery, cujo lema é &#8220;Write less, do more&#8221; (escreva menos, faça mais).

**<span style="font-size: 14px;">17</span> &#8211; Comente seu código sempre que possível.**
  
Isso evita muita dor de cabeça no futuro, quando for dar manutenção no código e também evita a famosa frase: &#8220;Putz! O que faz essa parte do código?&#8221;.