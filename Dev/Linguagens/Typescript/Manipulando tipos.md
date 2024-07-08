### _Type Annotation_

Um dos pontos positivos de usar `*typescript`* é que ele nos dá a possibilidade de prevenção de erros antes da compilação pelo fato dele aceitar anotações de tipo em nossas variáveis. Ou seja, iremos agora manipular um `*javascript*` não mais com uma `*tipagem fraca*`, mas com variáveis baseadas no tipo recebido.

Por exemplo, agora podemos declarar que determinada variável pode apenas receber uma string, ou um número. Ou quem sabe identificá-la que só poderá receber valores booleanos. Em funções, conseguimos identificar quais valores aquela função deverá receber para que funcione corretamente, assim como dizer o que retornará.

```jsx
// precisamos apenas usar *:tipo*
let nome: string = 'Isso é Typescript!'

let n:number = 100

function soma(a:number, b:number) : number{
    return a+b
}

soma(5,10)
```

E isso é excelente! Por exemplo, se tentarmos vincular uma string na variável n, o typescript antes de compilar vai identificar o erro e nos informar o que estamos fazendo de errado:

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8fb3e7df-cbd1-499d-8c33-9c700205b4b6/Untitled.png)

Assim como ao chamar funções nos informa seu retorno e parâmetros:

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ee1a5642-2120-47ee-b976-957822616990/Untitled.png)

### Inferência

Para que não precisemos explicitar o tipo de valor que determinada variável irá receber toda vez que formos declarar uma nova variável, o `*typescript*` é inteligente o suficiente para fazer a inferência daquele valor. Ou seja, ele deduz pelo primeiro valor recebido que aquela variável é do tipo x, então ele só vai aceitar novos valores do tipo x.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b4151c5a-a6d1-4eab-b871-fb05755a50bc/Untitled.png)

Os objetos são a mesma coisa. No caso visualmente fica um pouco estranho, mas a lógica é a mesma. Você diz que determinada variável é um objeto e não só, você diz também o que as propriedades daquele objeto irão receber. Depois você pode associar valores se desejar.

```jsx
const user : {
    nome: string;
    idade: number;
} = {
    nome: 'itallo',
    idade: 20
}
```

Iremos ver depois com detalhes sobre objetos, classe e POO.

### _Union Types_

Muitas vezes temos variáveis ou funções que podem receber um valor ou outro dependendo do contexto, e as vezes como o contexto é diferente os tipos dele também são. No `*Typescript*`podemos utilizar o operador `|` para dizer que uma variável pode receber x ou y tipos.

```jsx
let total: number | boolean

// neste caso, total pode receber 
// tanto valores booleanos quanto números
total = 100
total = false
```

Assim como funções que podem receber dois tipos de valores:

```jsx
function isBoolean(value: string | boolean){

    if(typeof value === "boolean"){
        return true
    }
    else{
        return false
    }
}

const valor = true
isBoolean(valor) // true
```

### Criando Tipos

Uma das adições muito interessantes que temos é a possibilidade de criar nossos próprios tipos. Eles podem ser úteis em diversos cenários diferentes. Um exemplo de introdução é uma variável que pode receber uma cor. Mas imagine que você deseja receber apenas x, y e z cores. Podemos utilizar `*Union Types*` em conjunto para que possamos criar variáveis que só aceitam determinadas cores.

É um exemplo simples mas muito interessante para entendermos como a criação de tipos funciona.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ea394cf0-b598-4419-9635-f7b5baed62a3/Untitled.png)

Um cenário mais recorrente do uso do `*type`* seria para lidar com funções.

Por exemplo: vamos estender o exemplo acima para uma função que faz algo a partir da cor.

```jsx
type Cor = 'azul' | 'vermelho' | 'roxa'
let minhaCor: Cor
minhaCor = 'azul'

function corExemplo(corEscolhida: Cor){
    if(corEscolhida === 'azul'){
        console.log('Azul da cor do mar!')
    }
    else if(corEscolhida === 'roxa'){
        console.log('Você gosta de beringelas?')
    }
    else{
        console.log('grrrrrr')
    }
}

corExemplo(minhaCor) // Azul da cor do mar!
corExemplo('vermelho') // grrrrrr

// erro!
// ele não compila pois preto não faz
// parte das strings aceitas no tipo Cor
corExemplo('preto') 
```

### Generics

A utilização de `*Generics*` serve para casos em que temos uma função ou um tipo de dado que pode ter tipos diferentes dependendo do momento em que é executado ou do contexto que está inserido.

Vamos supor que eu tenha uma função que retorna os três primeiros elementos de um vetor. Passando um vetor de `*strings*`, precisamos dizer que o parâmetro recebido é do tipo vetor de `*string*`, e nossa função irá ser executada normalmente.

```jsx
const nomes: string[] = ['itallo', 'vitoria', 'joao', 'thaissa']

function primeirosTres(vetor: string[]){
    return vetor.slice(0,3)
}

console.log(primeirosTres(nomes))
// ['itallo', 'vitoria', 'joao']
```

Agora pense que você possui um vetor de números, e quer capturar os três primeiros números. Você poderia fazer de duas formas:

`*1**º**:*` Criando uma segunda função que receberia um vetor de números.

Daria certo mas você teria duas funções que executam o código idêntico com parâmetros idênticos mas tipos diferentes, então não é uma boa ideia por conta da duplicação de código e problemas para manutenção.

`*2**º:`*** Utilizando `*Union Types.*`

Daria certo também, mas você poderia vir a ter um parâmetro cheio de tipos para dar match em todos as possibilidades que poderia vir a ter.

```jsx
function primeirosTres(vetor: string[] | number[]){
    return vetor.slice(0,3)
}
```

`*3**º:*`** Utilizando `*Generics*`:

Como dito anteriormente, a utilização de `*generics*` serve basicamente para ao invés de passar o valor do dado manipulado, passar seu tipo. Neste exemplo cai como uma luva:

```jsx
//                  tipo genérico    vetor do tipo passado
function primeirosTres <tipo>(vetor: tipo[]){
    return vetor.slice(0,3)
}
```

Para fazer esse informe, passamos o tipo entre o sinal de **`*<tipo>*` .**

```jsx
const nomes: string[] = ['itallo', 'vitoria', 'joao', 'thaissa']
const nums: number[] = [10,20,30,40,50]

console.log(primeirosTres(nomes)) // [ 'itallo', 'vitoria', 'joao' ]
console.log(primeirosTres(nums)) // [ 10, 20, 30 ]
```

Agora veja que interessante, ao verificar as informações da função, dependendo do dado que ela recebe temos um informe diferente:

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7901e6d0-2e8e-4a14-ad6d-f3d43b71f007/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ed35ae30-1ffc-4f7b-819e-8bfc04a1c4de/Untitled.png)

Essa notação aparece também na declaração de vetores:

```jsx
// forma 01
//            tipovetor
const vetor1:string[] = ['a', 'b']

// forma 02
//            vetor  tipo
const vetor2: Array<string> = ['a', 'b']
```

### Filtrando seu uso

As vezes queremos usar um tipo genérico de um determinado grupo de tipos, e desta forma, a função acaba recebendo qualquer tipo genérico existente. Por exemplo, vamos supor que temos uma função que pinta o fundo de um elemento do DOM.

```jsx
function mudaFundo<tipo>(el: tipo){
    el.style.background = 'blue'
}

const link = document.querySelector('a')
mudaFundo(link)
```

O problema do código acima é que o `*el*` pode ser uma `*string*`, um `*boolean*`, um `*number*`, porque ele é genérico demais. Para filtrar podemos especificar qual classe esse elemento herda suas propriedades.

Neste caso podemos dizer que essa função só pode ser usada por elementos que estendem - `*extends*` - da classe `*HTMLElement*` .

```tsx
// agora nossa função só trabalhará com elementos que forem HTML
function mudaFundo <tipo extends HTMLElement>(el: tipo){
    el.style.background = 'grey'
}

const link = document.querySelector('a')

if(link){
    mudaFundo(link)
}
```

E vai ser muito comum vermos aquele nome do tipo ter um T, ou uma variável bem pequena.

```tsx
//              desta forma 
function mudaFundo <T extends HTMLElement>(el: T){
    el.style.background = 'grey'
}

```

### Any Vs Unknown

Vamos analisar o código abaixo:

```jsx
const el = document.querySelector('#link')

function mudaCor(el){
    el.style.color = 'red'
}
```

Primeiro é capturado o elemento com o `*id*` de `*#link*` do DOM, e depois criamos uma funcão que muda a cor de um elemento recebido. Agora nosso código está dando um _warning_ dizendo que o elemento é do tipo `*Any*` .

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9edf94ba-6f18-4673-bf34-0676a288c37f/Untitled.png)

Ou seja, o TS indica que esse pode ser qualquer elemento, e isso é ruim pois ele não sabe como manipular esse elemento, não consegue sugerir seus métodos e propriedades e não é capaz de analisar o código para adiantar possíveis erros.

Tanto que ao colocar a notacão de ponto para acessar as propriedades e métodos do elemento, nos é sugeridos valores que não podem ser utilizadas em um elemento do DOM - como é o exemplo do slice, que é um método de vetores. Por isso que veremos as funções tendo em sua assinatura, o tipo que elas recebem.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c48d78e1-e6c8-4f59-bfe7-1464cfe163d0/Untitled.png)

`*el` com type `any` implícito*

Um outro tipo de dado que temos no TS é o `*unkown*`. Ele informa ao `*typescript*` que o dado recebido é de um tipo desconhecido. Este tipo exige que, para que possamos manipular esse valor, devemos utilizar `*typeguards*` para que seja garantido a segurança daquele tipo - `*type safety*`.

### _Type Guards_ e _Type Safety_

Ou seja, o código de baixo dará um erro, pois como o tipo do elemento é desconhecido, ele mostrará um _warning_ dizendo que o `*el*` não teve verificação e é do tipo unknown.

```jsx
function mudaCor(el: unknown){
        el.style.color = 'green'
}
```

Mas caso nós façamos uma verificação de tipo - mais conhecida como `*type guard*` - e assegurar que o que estamos manipulando é um tipo de, por exemplo, HTMLElement, aí tudo bem.

```jsx
function mudaCor(el: unknown){
    if(el instanceof HTMLElement)
    {
        el.style.color = 'green'
        return 'pintado!'
    }
    return 'não é um HTML Element'
}
```

### Type Predicate

Vamos supor o seguinte contexto:

No topo do código temos uma função assíncrona que captura um conselho de uma API. Desestruturamos essa resposta e retornamos o conselho em forma de `*string`.* Para prevenir possíveis erros no futuro caso a estrutura dessa API mude e ela tenha um retorno diferente, podemos utilizar um `*type guard*` para que seja mostrado apenas quando o resultado do `*fetch*` for do tipo _`string`._

```jsx
// função que captura o conselho
async function getAdvice(){
    const response = await fetch('<https://api.adviceslip.com/advice>')
    const {slip:{advice}} = await response.json()
    return advice
}

// função que mostra o conselho 
function showAdvice(data: unknown){

		// type guard
    if(typeof data === 'string'){
        console.log(data.toUpperCase())
    }
}

	getAdvice().then(showAdvice)
```

O código acima funciona maravilhosamente bem. Agora vamos retirar esse `*type guard*` dali e colocá-lo em uma função separada.

```jsx
async function getAdvice(){
    const response = await fetch('<https://api.adviceslip.com/advice>')
    const {slip:{advice}} = await response.json()
    return advice
}

// função responsável por verificar se o tipo 
// é string ou não
function checkData(value: unknown){
    return typeof value === 'string';
}

    function showAdvice(data: unknown){
    if(checkData(data)){
									// erro
        console.log(data.toUpperCase())
    }
}

getAdvice().then(showAdvice)
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7fa254c9-b6a4-42df-a45d-0c58e8cda0b9/Untitled.png)

A lógica é exatamente a mesma, porém, temos um erro dizendo que o tipo data é desconhecido. Isso ocorre porque o `*typescript`* não executa o código, então como colocamos a verificação fora da função atual, ele não consegue inferir pelo contexto se o tipo de data é `*string`* ou não.

Para resolver esse problema, temos que indicar ao `*typescript`* que o retorno da função `*checkData*`, caso for verdadeiro, indica que a variável `*data`* é uma `*string*`.

```jsx
//                                   valor é string caso seja true
function checkData(value: unknown) : value is string{
    return typeof value === 'string';
}
```

Isso faz com que o data dentro do bloco do `*checkdata`* seja invariavelmente verdadeiro.

### Segundo Exemplo:

Temos uma função que retorna o `*fetch*` de uma api. Esse `*fetch*` deve retornar um vetor de cursos. Esses cursos devem ter, pelo menos, `*nome*`, `*tags*` e `*horas*` para que possamos mostrar na tela.

Abaixo faremos a função `*getCursos*` e a interface deles.

```jsx
// função que retorna os cursos
async function getCursos(){
    const response = await fetch('<https://api.origamid.dev/json/cursos.json>')
    return await response.json()
}

interface Curso{
    nome: string
    aulas: number;
    gratuito: boolean;
    horas: number;
    idAulas: number[];
    nivel: string;
    tags: string[];
}
```

Podemos fazer uma função de verificação para ver se o item recebido é do tipo `*Curso*` ou não.

```jsx
// function com type predicate 
function checkCurso(data: unknown) : data is Curso
{
    return !!(data && 'nome' in data && 'tags' in data && 'horas' in data && typeof data === 'object');
}
```

Agora na nossa função principal nós verificamos se o que nosso `*fetch*` retornou é um vetor e caso seja, passamos seus itens para a checagem.

```jsx
function showCursos(data: unknown){

    if (Array.isArray(data)){
        data.filter(checkCurso).forEach((item)=>{
            document.body.innerHTML +=
            `<h1>${item.nome}</h1>
            <p>${item.tags}</p>
            <p>${item.horas}</p>`
        })
    }
    else{
        console.log('algo deu errado!')
    }
}

getCursos().then(showCursos)
```

### Tuples

`*Tuples*` são vetores que possuem índices com tipos fixos.

```jsx
const livro: [string, number] = ['A culpa é das Estrelas', 120]
```

Agora ao acessar o índice 0 do livro o TS sabe que é do tipo `*string*` e nos autocompleta com propriedades e métodos de `*string*`, e no índice 1 terá propriedades e métodos de `*number*`.

Subtópico: [[Typescript]]