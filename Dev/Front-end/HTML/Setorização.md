Depois de todos os tópicos que foram estudados, vamos dispor eles em uma página. O objetivo dela é falar um pouco sobre as linguagens do front end e uma breve apresentação de si. Fique à vontade para mudar os dados. Ela deve ficar mais ou menos assim:

```html
<h1> Oi, eu sou o Itallo! </h1>
<h2> Prazer! </h2>

<p>
    Sigo estudando para conseguir minha <strong> vaga de estágio.  </strong> 
    Moro no <i>rio de janeiro.</i> <br> Não vejo a hora de uma oportunidade!
</p>

<h3>O que já estudei</h3>
<ul>
    <li> <s> Html básico </s> </li>
    <li>Html intermediario</li>
    <li>Html avançado</li>
</ul>

<h3>Minhas linguagens preferidas</h3>
<ol>
    <li>CSS</li>
    <li>JS</li>
    <li>C#</li>
</ol>

<table>
    <caption>Meus horários de Estudo</caption>
    <thead>
        <tr>
            <th> Manhã </th>
            <th> Tarde </th>
            <th> Noite </th>
            <th> Madrugada </th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td> HTML </td>
            <td>Exercício de HTML</td>
            <td colspan="2" rowspan="3"> Descansar </td>
        </tr>
        <tr>
            <td> CSS </td> 
            <td>Exercício de CSS</td>           
        </tr>
        <tr>
            <td> JS </td>
            <td>Exercício de JS</td>
        </tr>
    </tbody>
</table>

<picture>
    <!-- Só irá mostrar até 500px -->
    <source media="(max-width: 500px )" srcset="./imgs/imgMobile.jpg">

    <!-- Só irá mostrar depois de 501px -->
    <source media="(min-width: 501px)" srcset="./imgs/imgDesktop.png">
    <img src="" alt="">
</picture>

<h1>Tipos de Linguagens Estudadas</h1>
<dl>
    <dt>HTML</dt>
    <dd>Linguagem de marcação de texto.</dd>
    <dt>CSS</dt>
    <dd>Linguagem de estilização em cascata.</dd>
    <dt>JS</dt>
    <dd>Linguagem de programação.</dd>
</dl>

<figure>
    <img src="./imgs/triade.jpg" alt="">
    <figcaption> Tríade das linguagens Front-end.</figcaption>
</figure>

<p> HTML, CSS e JavaScript são três linguagens fundamentais para o desenvolvimento 
de páginas web.</p>

<p> HTML (HyperText Markup Language) é uma linguagem de marcação utilizada para 
criar o conteúdo e a estrutura de uma página web. Com HTML, é possível adicionar 
textos, imagens, vídeos, links, formulários, tabelas e outras estruturas básicas 
de uma página. </p>

<p> CSS (Cascading Style Sheets) é uma linguagem de estilo utilizada para definir
a aparência e o layout de uma página web. Com CSS, é possível controlar a cor, o 
tamanho, a fonte, a posição e outras propriedades visuais de cada elemento da página,
criando uma experiência visualmente atraente e coerente para o usuário. </p>

<p> JavaScript é uma linguagem de programação usada para criar interatividade e 
dinamismo em uma página web. Com JavaScript, é possível adicionar comportamentos e 
efeitos especiais aos elementos da página, validar formulários, realizar animações, 
criar jogos e aplicativos web, e muito mais. </p>

<p> Juntas, essas três linguagens formam a base da programação web moderna, 
permitindo a criação de páginas e aplicativos web interativos e responsivos. Cada uma
delas tem sua própria função e é essencial para a criação de uma experiência de usuário
envolvente e eficiente.</p>

<video width="320" height="240" controls>
    <source src="./videos/htmlvideo.mp4" type="video/mp4">
</video>
```

Com um estilo bem básico, apenas para não quebrar muito o layout e para mostrar melhor alguns elementos para que a didática fique melhor. Não iremos focar nessa parte.

```html
<style>
        table{
            width: 60%;
            background-color: rgb(81, 81, 81);
            padding: 2%;
            color: white;
            text-align: center;
        }

        caption{
            background-color: rgb(180, 176, 185);
            padding-block: 3%;
            font-size: 2rem;
            color: black;
            font-weight: bold
        }

        thead{
            background-color: black;
        }

        tbody{
            background-color: white;
            color: black;
        }

        td{
            padding: 1.5%;
        }

        picture{
            width: 100%;
        }

        img{
            max-width: 100%;
        }

        figcaption{
            text-align: center;
		    }
</style>
```

Percebe que vendo o código assim rapidamente é difícil de entender o que está acontecendo? Por mais simples que o código seja, é complicado entender o que cada parte quer dizer, onde começa um tópico e onde termina o outro.

### A famigerada Tag Div

A tag Div nada mais é do que uma tag divisora, sem estilo especial. É uma tag genérica que basicamente divide um conteúdo do outro e os engloba para ajudar na distribuição do conteúdo. As tags elas servem justamente para englobar os elementos, fornecer informações ao navegador de como tratá-las, e as vezes aplicar alguns estilos especiais. Pensando nisso, podemos aplicar divs em - quase, muito quase - tudo!

```html
<div> Oi, eu sou o Itallo! </div>
<div> Prazer! </div>

<div>
    Sigo estudando para conseguir minha <strong> vaga de estágio.  </strong> 
    Moro no <i>rio de janeiro.</i> <br> Não vejo a hora de uma oportunidade!
</div>

<div>O que já estudei</div>
<div>
    <li> <s> Html básico </s> </li>
    <li>Html intermediario</li>
    <li>Html avançado</li>
</div>

<div>Minhas linguagens preferidas</div>
<ol>
    <li>CSS</li>
    <li>JS</li>
    <li>C#</li>
</ol>

<div>
    <div>Meus horários de Estudo</div>
    <div>
        <tr>
            <th> Manhã </th>
            <th> Tarde </th>
            <th> Noite </th>
            <th> Madrugada </th>
        </tr>
    </div>
    <div>
        <tr>
            <td> HTML </td>
            <td>Exercício de HTML</td>
            <td colspan="2" rowspan="3"> Descansar </td>
        </tr>
        <tr>
            <td> CSS </td> 
            <td>Exercício de CSS</td>           
        </tr>
        <tr>
            <td> JS </td>
            <td>Exercício de JS</td>
        </tr>
    </div>
</div>

<picture>
    <!-- Só irá mostrar até 500px -->
    <source media="(max-width: 500px )" srcset="./imgs/imgMobile.jpg">

    <!-- Só irá mostrar depois de 501px -->
    <source media="(min-width: 501px)" srcset="./imgs/imgDesktop.png">
    <img src="" alt="">
</picture>

<div>Tipos de Linguagens Estudadas</div>
<div>
    <dt>HTML</dt>
    <dd>Linguagem de marcação de texto.</dd>
    <dt>CSS</dt>
    <dd>Linguagem de estilização em cascata.</dd>
    <dt>JS</dt>
    <dd>Linguagem de programação.</dd>
</div>

<div>
    <img src="./imgs/triade.jpg" alt="">
    <div> Tríade das linguagens Front-end.</div>
</div>

<div>HTML, CSS e JavaScript são três linguagens fundamentais para o desenvolvimento 
de páginas web.</div>

<div> HTML (HyperText Markup Language) é uma linguagem de marcação utilizada para 
criar o conteúdo e a estrutura de uma página web. Com HTML, é possível adicionar
textos, imagens, vídeos, links, formulários, tabelas e outras estruturas básicas 
de uma página. </div>

<div> CSS (Cascading Style Sheets) é uma linguagem de estilo utilizada para definir
 a aparência e o layout de uma página web. Com CSS, é possível controlar a cor, 
o tamanho, a fonte, a posição e outras propriedades visuais de cada elemento da 
página, criando uma experiência visualmente atraente e coerente para o usuário.</div>

<div> JavaScript é uma linguagem de programação usada para criar interatividade 
e dinamismo em uma página web. Com JavaScript, é possível adicionar comportamentos
 e efeitos especiais aos elementos da página, validar formulários, realizar animações,
 criar jogos e aplicativos web, e muito mais. </div>

<div> Juntas, essas três linguagens formam a base da programação web moderna, 
permitindo a criação de páginas e aplicativos web interativos e responsivos. Cada 
uma delas tem sua própria função e é essencial para a criação de uma experiência de 
usuário envolvente e eficiente.</div>

<video width="320" height="240" controls>
    <source src="./videos/htmlvideo.mp4" type="video/mp4">
</video>
```

Por incrível que pareça, por mais que por baixo dos panos role um “atenção, você está fazendo besteira” por parte do navegador, a página exposta com o código acima é extremamente parecida com a página feita com as tags corretas. Caso entrássemos com CSS fazendo as devidas correções de layout, o resultado seria idêntico.

O fato é que usar div em tudo não é nada intuitivo nem para nós, nem para os navegadores. Por conta disso, é extremamente importante o aprendizado das tags semânticas para deixar o html bem estruturado, de fácil leitura e costumização. Vamos às tags semânticas de setorização.

- Header
    - Responsável pelo cabeçalho da página, ficando no topo. Podem englobar barras de navegação, imagens tema de abertura da página, conteúdos que ficam no topo.
- Main
    - Responsável por englobar o conteúdo principal da página.
- Footer
    - Responsável por englobar o conteúdo do rodapé da página.
- Aside
    - Responsável por englobar o conteúdo secundário ou lateral da página. Geralmente são parte contendo links para outra página, anúncios, conteúdos que saem do fluxo principal.
- Article
    - Responsável por englobar um conteúdo que é independente de outros. Um tópico principal, um trecho que é, como um todo, independente.
- Section
    - Responsável por englobar um conteúdo que é dependente ou uma continuação de outro. Um subtópico que faz sentido estar com outros subtópicos.
- nav
    - Responsável por englobar um conjunto de links capazes de fazer com que possamos navegar pelo site. Antes era usado uma lista não ordenada para tal. Veremos mais detalhes em breve.

O uso delas vai depender de como você vai estruturar sua página. Pode ser que você tenha uma barra de navegação lateral - diferente, mas possível - ou pode ser que você não use o aside pois não tem um conteúdo secundário. Vai depender muito do seu caso de uso. Vamos Adicionar essas tags em nossa página e adicionar nomes em cada seção:

```html
<header id="cabecalho"> 
    <nav id="navegacao">
        <a href="#">- Quem sou </a>
        <a href="#">- Meus horários </a>
        <a href="#">- tipos de linguagem </a>
    </nav>
    <p id="cabecalho_titulo">superTítulo</p>
</header>

<main id="container_principal">
    <article id="container_sobre">
        <section id="container_apresentacao">
            <h1> Oi, eu sou o Itallo! </h1>
            <h2> Prazer! </h2>
            <p>
                Sigo estudando para conseguir minha <strong> vaga de estágio.</strong> 
                Moro no <i>rio de janeiro.</i> <br> Não vejo a hora de uma oportunidade!
            </p>
      </section>

      <section id="container_linguagensPreferidas">
          <h3>Minhas linguagens preferidas</h3>
          <ol>
              <li>CSS</li>
              <li>JS</li>
              <li>C#</li>
          </ol>
      </section>
    </article>

    <article id="container_estudo">
        <section id="container_linguagensEstudadas">
            <picture id="container_imagemTema">                
                <source media="(max-width: 500px )" srcset="./imgs/imgMobile.jpg">
                <source media="(min-width: 501px)" srcset="./imgs/imgDesktop.png">
                <img src="" alt="">
            </picture>

            <h3>O que já estudei</h3>
            <ul>
                <li> <s> Html básico </s> </li>
                <li>Html intermediario</li>
                <li>Html avançado</li>
            </ul>

            <h1>Tipos de Linguagens Estudadas</h1>
            <dl>
                <dt>HTML</dt>
                <dd>Linguagem de marcação de texto.</dd>
                <dt>CSS</dt>
                <dd>Linguagem de estilização em cascata.</dd>
                <dt>JS</dt>
                <dd>Linguagem de programação.</dd>
            </dl>
        </section>

        <section id="container_tabela">
            <table>
                <caption>Meus horários de Estudo</caption>
                <thead>
                    <tr>
                        <th> Manhã </th>
                        <th> Tarde </th>
                        <th> Noite </th>
                        <th> Madrugada </th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td> HTML </td>
                        <td>Exercício de HTML</td>
                        <td colspan="2" rowspan="3"> Descansar </td>
                    </tr>
                    <tr>
                        <td> CSS </td> 
                        <td>Exercício de CSS</td>           
                    </tr>
                    <tr>
                        <td> JS </td>
                        <td>Exercício de JS</td>
                    </tr>
                </tbody>
            </table>   
        </section>
  </article>

  <article id="container_triade">
      <figure id="container_imagemTriade">
          <img src="./imgs/triade.jpg" alt="">
          <figcaption> Tríade das linguagens Front-end.</figcaption>
      </figure>

      <section id="container_texto">
          <p>HTML, CSS e JavaScript são três linguagens fundamentais para o 
					desenvolvimento de páginas web.</p>

          <p> HTML (HyperText Markup Language) é uma linguagem de marcação 
					utilizada para criar o conteúdo e a estrutura de uma página web. Com HTML, 
					é possível adicionar textos, imagens, vídeos, links, formulários, tabelas e 
					outras estruturas básicas de uma página. </p>

          <p> CSS (Cascading Style Sheets) é uma linguagem de estilo utilizada 
					para definir a aparência e o layout de uma página web. Com CSS, é possível 
					controlar a cor, o tamanho, a fonte, a posição e outras propriedades visuais 
					de cada elemento da página, criando uma experiência visualmente atraente e 
					coerente para o usuário. </p>

          <p> JavaScript é uma linguagem de programação usada para criar 
					interatividade e dinamismo em uma página web. Com JavaScript, é possível 
					adicionar comportamentos e efeitos especiais aos elementos da página, 
					validar formulários, realizar animações, criar jogos e aplicativos web, 
					e muito mais. </p>

          <p> Juntas, essas três linguagens formam a base da programação web
					moderna, permitindo a criação de páginas e aplicativos web interativos e 
					responsivos. Cada uma delas tem sua própria função e é essencial para a 
					criação de uma experiência de usuário envolvente e eficiente.</p>
      </section>

      <video id="videoTriade" width="320" height="240" controls>
          <source src="./videos/htmlvideo.mp4" type="video/mp4">
      </video>
  </article>
</main>
```

Código infinitamente melhor arrumado. Conseguimos ver cada seção e entender sobre o que ela se trata não só por conta dos id’s informando seus nomes mas principalmente por conta da segmentação semântica utilizada. Agora fica mais fácil de estilizar, mais fácil de ler e entender o código e mais fácil para que pessoas que dependem de acessibilidade do navegador, consumam o conteúdo. Lembre-se: um HTML bem estruturado vai poupar muita dor de cabeça no futuro.

Tópico: [[HTML]]