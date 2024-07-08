Agora veremos algumas tags semânticas que são usadas com as imagens. É muito comum que usemos tags que englobam as imagens para que possamos evitar qualquer comportamento inesperado por parte delas. Aqui veremos algumas comuns e seus cenários:

### Picture e Source

A tag picture é simplesmente incrível. Imagine que você tem duas imagens que mostram a mesma coisa porém possuem proporções e tamanhos diferentes para quando a página está no mobile e quando a página está no desktop. Então naturalmente você pensa em usar algum tipo ou de mediaQuery para mudar a imagem, ou JS, ou qualquer outro modo de mostrar uma e ocultar a outra. Com a Tag picture esse problema é resolvido de uma forma simples e muito intuitiva.

A tag Picture vem acompanhada com uma tag chamada Source. Com ela podemos passar como atributo um media query para que aquela fonte da imagem seja usado apenas quando o media query for verdadeiro. Assim não precisamos passar parâmetro para a tag img. Vejamos:

```html
<picture>
	<!-- Só irá mostrar até 500px -->
	<source media="(max-width: 500px )" srcset="./imgs/imgMobile.jpg">
	
	<!-- Só irá mostrar depois de 501px -->
	<source media="(min-width: 501px)" srcset="./imgs/imgDesktop.png">
	<img src="" alt="">
</picture>
```

Versão de Mobile:

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f09b261b-27be-4e5f-94c9-772c3fb4911f/Untitled.png)

Versão de Desktop:

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ecd74df2-8edc-4dfb-a6db-956006ec92fd/Untitled.png)

Isso nos permite ter um controle melhor do que vai ser mostrado e como em cada local, de uma forma simples, intuitiva, e com menos CSS/JS!

### Figure e figcaption

A tag figure serve para ser usada em conjunto com as tags img quando se tem imagens que servem para algum segmento da página que não seja decorativo. Com ela podemos adicionar uma segunda tag figcaption que serve para descrever a imagem utilizada.

Claro que com um pouco de CSS ficaria melhor, mas dá para entender que a semântica e a leiturabilidade do código é o que importa.

```html
<!-- Mesmo resultado, não semântico -->
<div>
    <img src="./imgs/triade.jpg" alt="">
    <p>Tríade das linguagens Front-end.</p>
</div>

<figure>
    <img src="./imgs/triade.jpg" alt="">
    <figcaption> Tríade das linguagens Front-end.</figcaption>
</figure>
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4cef1d8a-077b-4305-8fcd-f35b9d672eb5/Untitled.png)

### Videos

Os videos são muito parecidos com as fotos. Precisam da tag video e dentro uma tag source. Lembrando que para que eles aparecam devemos adicionar altura e largura neles.

```html
<video width="320" height="240" controls>
    <source src="./videos/htmlvideo.mp4" type="video/mp4">
</video>
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/27ff4b5d-1f30-49cc-8343-f1c7a64b1607/Untitled.png)

Tópico: [[HTML]]