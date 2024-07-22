Considerando um cenário onde temos um link - ou qualquer outro elemento - em nosso arquivo html, vamos capturá-lo diretamente pela tag:

```jsx
// capturando o link disponível no html pela tag a
const link = document.querySelector('a')
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/496e6931-90ea-4ae0-9020-eba1848841aa/Untitled.png)

O typescript nos fornece a informação através do Union Type que aquele elemento pode ser um `*HTMLAnchorElement*` - ou seja, uma tag âncora de link - ou ele pode ser `*null*` . Se o elemento existe no nosso DOM e estamos capturando ele corretamente, por que o typescript informa que ele pode ser um tipo nulo?

Isso acontece, novamente, no compile-time. TS não executa o código, apenas analisa seu contexto. Sendo assim, aquele elemento pode ser uma âncora - já que estamos o capturando pela `*tag*` de âncora - mas pode vir a ser também um elemento nulo caso ele não existe no DOM.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/16033cea-ceab-466a-8d90-ce111328c5a7/Untitled.png)

Tanto que ao acessar a propriedade `*href*` que está disponível em elementos de âncora, o typescript nos dá um _warning_ informando que como aquele elemento tem a possibilidade de ser nulo, utilizar a propriedade `*href*` pode não funcionar - já que elementos nulos não possuem essa propriedade.

### Instance of

Uma das formas de resolver esse problema é utilizar `*instance of*` para fazer a verificacão para saber se o elemento em si é uma instância da classe responsável por criar âncoras, e caso for, execute um determinado código. Isso faz com que nosso código fique mais seguro e bem estruturado.

```jsx
const link = document.querySelector('a')

if(link instanceof HTMLAnchorElement){
    console.log(link.href)
}
```

Como podemos ver, cada tipo de elemento do DOM possui uma classe responsável por definir métodos e propriedades para que nós possamos os manipular.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/051f0f76-3570-4dc4-85fc-365c34c88bee/Untitled.png)

Podemos analisar o sistema de herança do HTMLElement e do SVGElement na árvore abaixo:

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/25e2b696-794b-48f9-a453-bb81b94b4a7e/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/219bcf39-e523-4462-8aa9-b9a588b7e59e/Untitled.png)

Note que ambos são instâncias do tipo `*Element*`, porém, depois disso eles herdam de classes diferentes. Então temos que ter cuidado ao verificar as instâncias, para que consiguemos filtrar da forma correta.

### Capturando de forma específica

Veja que ao utilizar um querySelector - ou poderia ser qualquer outra forma de captura, seja por classe, id, atributo e etc. - o que nos é informado é que é do tipo `*Element*` ou nulo. Novamente, `*typescript*` verifica o contexto e nos diz que o que será retornado daquela captura pode ser qualquer elemento - por isso tipo `*Element*`, já que essa é uma classe presente nos elementos do DOM - ou pode vir a ser nulo caso não exista.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/df0acf8a-29e1-48ed-a4d3-17a6fa155271/Untitled.png)

Utilizando a verificação anterior, agora `*typescript*` se assegura de que aquele elemento é do tipo âncora e nos auto completa com a propriedade que desejarmos.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bdddd9f1-f73f-470a-918d-e0eecdca7971/Untitled.png)

### Type Assertion

Caso tenhamos certeza que determinado elemento que iremos capturar existe no DOM e que não precisamos fazer nenhuma verificação, podemos utilizar a palavra reservada `*as*` para indicar o tipo do elemento retornado.

`*Typescript*` confiará em nós e vai dispor as propriedades e métodos de links.

```jsx
const link = document.querySelector('.link') as HTMLAnchorElement
```

Subtópico: [[Typescript]]