# dctb-svg-animate

Original de https://www.facebook.com/origamid/

A fórmula mágica é:

SVG (path's) + CSS Animation + stroke-dashoffset + stroke-dasharray + JS

O código completo está no exemplo: http://codepen.io/origamid/pen/vKEQWX


1. Selecionar o item que deseja animar. Deve ser um vetor composto por linhas (stroke). Exportar para SVG. No illustrator é só ir em File > Save As > Selecionar SVG.

2. Otimizar o SVG, com isso você vai diminuir o tamanho do svg e ainda transformar linhas em path's.
  1. É fácil otimizar, basta entrar neste link: https://jakearchibald.github.io/svgomg/ e arrastar o arquivo para a tela que o upload será feito.
  2. A única mudança que precisa fazer nas configurações é desmarcar o item Merge paths (No menu vertical que está no canto direito do site). Salve o código gerado e cole direto no seu HTML.
3. A animação é feita da seguinte forma:

Existem 2 propriedades no CSS que manipulam o stroke (linha) de cada path (são as partes do seu arquivo) do seu SVG.

* stroke-dasharray

A dasharray vai definir o tamanho do pontilhado das linhas. Uma dasharray de 0, cria linhas não pontilhadas. Uma dasharray de 10, cria um pontilhado de 10px (não é 10px, mas é quase isso).

* stroke-dashoffset

A dashoffset especifica a que distância o primeiro pontilhado vai começar. No 0 você terá um um pontilhado normal, com o primeiro tracinho iniciando no começo do path.

Agora a grande sacada de Jake Archibald foi a seguinte. Se definirmos um stroke-dasharray do tamanho do path, ou seja se o path tem 100 de distância o stroke-dasharray tiver 100 também.

Você vai acabar criando um pontilhado tão grande que não será possível ver os outros traços. Já que um tracinho vai ocupar 100% da distância do path.

E se definirmos um stroke-dashoffset também do tamanho do path, esse grande traço que criamos agora terá um offset do mesmo tamanho dele.

Exemplo: se temos uma caixa de 100px e um item dentro dela com margem de -100px, esse item acaba não aparecendo dentro da caixa, ele está "fora dela".

Ai a animação acontece quando mudamos o stroke-dashoffset do tamanho total para 0.

Se o stroke-dashoffset for de 200, a distância que ele percorrer para voltar ao ponto 0, inicial dele, deverá ser animada.

Agora precisamos definir o comprimento de cada path do nosso SVG. Isso é muito simples com uma função que eu criei com jQuery
var comprimento = $(this).get(0).getTotalLength();

E dinamicamente com o jQuery adicionamos este valor ao stroke-dashoffset e stroke-dasharray de cada path do nosso SVG. (Veja o exemplo para o código completo)

Animar com CSS

```
@keyframes svg-animate {
  from {}
  to {
  stroke-dashoffset: 0;
  }
}
svg.animate path {
  animation: svg-animate 4s forwards infinite;
}
```
A explicação está no exemplo.

Agora basta você adicionar a classe animate, que criamos no CSS, no seu SVG e ele será animado.
Compartilhe o seu experimento.

Mais em: https://www.origamid.com/
http://gph.is/1RPgQc8
