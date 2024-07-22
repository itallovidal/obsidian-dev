Muitas coisas foram implementadas com o ES6 em umas das maiores atualizações da linguagem ocorrida em 2015. Muitas delas já foi falado durante outros tópicos - como `*Arrow Functions`, `const` e `let`, `template strings`, `map` -* e agora com toda a bagagem aprendida ficará mais fácil de aprender as novas implementações da linguagem.

### Object Destructuring: Sintaxe Básica

Desestruturação de objeto é muito útil quando queremos pegar valores de um objeto ou vetor. Não só, mas também quando estamos trabalhando com retorno e recebimento de objetos por funções. Vamos ver a sintaxe básica:

Vamos supor que você quer pegar os primeiros valores de um vetor e adicionar em duas variáveis diferentes. Naturalmente você faria o seguinte código:

```jsx
// array de valores
const valores = [1,2,'a','b','c']

let numero1 = valores[0]
let numero2 = valores[1]

console.log(numero1, numero2) // output: 1 2
```

O código acima não está errado, porém é um tanto quanto trabalhoso. Desestruturando o vetor “valores” podemos fazer isso de uma maneira mais dinâmica: os valores novos vão em colchetes - ou chaves no caso de objetos - separados por vírgula e associados ao vetor/objeto em questão.

```jsx
// array de valores
const valores = [1,2,'a','b','c']

let [n1, n2] = valores

console.log(n1, n2) // output: 1 2
```

Se quisermos naturalmente pegar mais de um valor fica muito mais prático. Quando o espaço está em branco, é indicado que os valores em questão devem ser pulados.

### Spread Operator

O `*spread operator`* é muito útil para capturar, juntar, e extrair elementos de um vetor. Com ele podemos capturar a parte das letras do vetor dos valores, pulando os primeiros valores e atribuindo as letras ao vetor equivalente:

```jsx
// array de valores
const valores = [1,2,'a','b','c']

let [,,...letras] = valores

console.log(letras) // output: [ 'a', 'b', 'c' ]
```

Podemos inclusive juntar dois vetores de uma maneira bem dinâmica, já que é como se selecionássemos valor por valor de cada vetor e passássemos para a nova variável.

```jsx
// array de valores
const nums = [1,2]
const letras = ['a','b','c']

// array vazio criado
let valores = [...nums, ...letras]

console.log(valores) // output: [ 1, 2, 'a', 'b', 'c' ]
```

Podemos usar o `*spread operator*` também com funções, você pode ver mais detalhes de como ele funciona no [módulo de funções.](https://www.notion.so/Fun-es-b9ab264afbe34f86ac2295b5094c56da?pvs=21)

### Funções: Retornando Mais de Um Valor

Agora que entendemos como a sintaxe básica funciona, podemos aplicá-la em exemplos mais úteis: funções. `*Object Destructuring*` é muito útil quando queremos retornar mais de um valor ao mesmo tempo. Vejamos:

```jsx
// funcão de calculos
function calculos(a,b)
{
    return [a+b, a*b]
}

let [soma, multiplicacao] = calculos(2,3)

console.log(soma, multiplicacao)
```

No exemplo acima temos uma função de cálculo que retorna um vetor com soma e multiplicação dos valores passados. Quando chamamos a função já associamos a duas variáveis diferentes. Outro lugar muito útil é quando estamos manipulando objetos.

### Object Destructuring: Desestruturando Objetos

Vamos supor que temos um objeto aluno onde se tem algumas informações, e você deseja pegar um valor e associar à uma variável. Vejamos:

```jsx
const aluno = {
    nome: 'itallo',
    idade: 22,
    faculdade:{
        end: 'Tijuca',
        curso: 'SI'
    }
}

// pega a propriedade nome e associa à variável nome
const {idade} = aluno

console.log(idade) // 22
```

Com objetos precisamos usar chaves ( já que estamos pegando os valores de um objeto) e passar a propriedade. Javascript automaticamente cria uma variável “idade” e vincula o valor da propriedade idade à essa variável. Podemos também criar uma variável com nome diferente, sem problema algum. Para isso temos que informar qual nome da propriedade e qual a variável que irá recebê-la.

```jsx
const aluno = {
    nome: 'itallo',
    idade: 22,
    faculdade:{
        end: 'Tijuca',
        curso: 'SI'
    }
}

const {nome: primeiroNome} = aluno

console.log(primeiroNome) // itallo
```

E podemos ir além desestruturando o objeto dentro de outro objeto. Vamos supor que queremos pegar o curso do aluno. Podemos fazer da seguinte forma:

```
const aluno = {
    nome: 'itallo',
    idade: 22,
    faculdade:{
        end: 'Tijuca',
        curso: 'SI'
    }
}

// acessando o objeto faculdade e 
// dentro acessando a propriedade curso
// e vinculando à variável "nomeCurso"
const {faculdade:{curso: nomeCurso} } = aluno

console.log(nomeCurso) // SI
```

### Object Destructuring: Combinando Objetos

Podemos também combinar dois objetos diferentes usando o _`Spread Operator`_ , assim como vimos com os vetores.

Vamos supor que temos dois alunos e queremos combiná-lo para formar um terceiro aluno. Queremos pegar o segundo aluno que possui menos informações e adicionar as informações que já temos no primeiro. Vejamos:

```jsx
const aluno1 = {
    nome: 'itallo',
    idade: 22,
    faculdade:{
        end: 'Tijuca',
        curso: 'SI'
    }
}

const aluno2 = {
    nome: 'itallo',
    faculdade:{
        end: 'Barra',
    }
}

// o aluno3 irá pegar as infos do segundo + do primeiro
const aluno3 =  {...aluno2, ...aluno1 }

console.log(aluno3) 
//  {
//     nome: 'itallo',
//     idade: 22
//     faculdade: { end: 'Tijuca', curso: 'SI' },
//   }
```

Podemos perceber que propriedades que estão presentes nos dois como “nome” não é duplicada, propriedades que não existem no segundo aluno como “idade” e “curso” são adicionadas, e propriedades como “endereco” que possuem nos dois objetos mas com valores diferentes são sobrescritas pelo segundo objeto passado.

### Destructuring Functions Calls

Uma das coisas mais interessantes que podemos realizar utilizando esse método é desestruturar objetos em chamadas de função para que o uso de propriedades dentro das funções fique mais simples. Por exemplo, digamos que queremos fazer uma função que apresenta o aluno. As únicas propriedades que vamos usar é nome, idade e o curso. Geralmente faríamos assim:

```jsx
const aluno = {
    nome: 'itallo',
    idade: 22,
    faculdade:{
        end: 'Tijuca',
        curso: 'SI'
    }
}

function apresentaAluno(aluno)
{
    console.log(`Oi, eu sou o ${aluno.nome} e 
		realizo o curso de ${aluno.faculdade.curso}!`)
}

apresentaAluno(aluno)
// Oi, eu sou o itallo, tenho 22 anos e realizo o curso de SI!
```

Percebe que temos propriedades como “idade” e “end” que não estamos utilizando? Percebe que, ao passar o objeto todo como parâmetro da função, temos todo o trabalho de chamar a propriedade usando notação de ponto? “aluno.faculdade.curso”, “aluno.nome” e etc..

Para resolver esses dois problemas, podemos desestruturar o objeto na chamada da função, e utilizar apenas as propriedades que fazem sentido para nós. Vejamos:

```jsx
const aluno = {
    nome: 'itallo',
    idade: 22,
    faculdade:{
        end: 'Tijuca',
        curso: 'SI'
    }
}

function apresentaAluno({nome, faculdade:{curso}})
{
    console.log(`Oi, eu sou o ${nome}, e realizo o curso de ${curso}!`)
}

apresentaAluno(aluno)
// Oi, eu sou o itallo, e realizo o curso de SI!
```

### Modularização: Import e Export

Uma das funcionalidades novas implementadas com o ES6 foi a possibilidade de modular nosso código: fazer com que trabalhemos com scripts separados - como módulos - e que a medida que for necessário, juntemos eles em um arquivo só.

O objetivo é fazer com que cada arquivo `*javascript*` seja focado em realizar uma determinada tarefa, e que as tarefas só se juntem caso seja necessário. Isso faz com que fique mais fácil fazer manutenção no código, e que faca com que importemos apenas o necessário para continuar trabalhando naquela determinada tarefa.

Para fazer com que o navegador entenda que estamos trabalhando com módulos, precisamos explicitar primeiro no nosso documento HTML que aquele script é do tipo módulo.

```html
<script type="module" src="./script.js"></script>
<script type="module" src="./script2.js"></script>
```

Temos dois scripts: o primeiro é onde iremos executar nosso código principal e o segundo é onde guardaremos nossas funções. Vejamos:

```jsx
// script2.js
export const media = function(vetor){
    let soma = 0
    vetor.forEach((v)=>soma += v)
    return Number(soma / vetor.length)
}

export const soma = function (a,b){
    return Number(a+b)
}

export const checkNum = function (n){
    return typeof n === 'number'
}
```

Podemos agora importar as funções no nosso código principal:

```jsx
// script.js

// passamos as variáveis/funcoes/objetos dentro de colchetes 
// indicando ***o que*** iremos importar e depois indicamos o caminho
// do documento a ser importado
import {media, soma, checkNum} from './script.js'

const nums = [10, 5, 20, 2]

console.log(media(nums))
```

Algo interessante que podemos fazer é juntar todas as funções através de um objeto e exportar apenas esse objeto, usando a palavra reservada `*default*` para indicar que por padrão é ele que será importado.

```jsx
// script2.js
// não exportamos mas as funcões, apenas o objeto*

export default const obj = {
    media,
    soma,
    checkNum
}
```

```jsx
// script.js
// neste caso não precisamos das chaves 
import obj from './script.js'

const nums = [10, 5, 20, 2]

console.log(obj.media(nums))
```

### Short Circuit Evaluation

Muito usado em bibliotecas como o React, Short Circuit Evaluation é um método de executar determinada ação caso um valor especificado seja verdadeiro. Vejamos:

```jsx
// if-statment
const n = 10

if(n > 5)
    console.log('Número maior do que 5!')
```

```jsx
// Short Circuit Evaluation
const n = 10

n > 5 && console.log('Número maior do que 5!')
```

Ambos os códigos acima mostrarão no console que o número é maior do que 5.

O que ocorre é que o operador `*&&`* apenas executa a segunda parte da expressão caso a primeira parte - neste caso a verificação do `*n*` ser maior do que 5 - seja verdadeira. Já que ela é `*true*`, a segunda parte da expressão é realizada, prém o ponto é que não é uma nova verificação e sim um comando de console.log.

Ou seja, o comando do lado direito do `*&&*` só é realizado quando a primeira parte é verdadeira, e esse comando pode ser qualquer coisa. Isso é muito útil em bibliotecas como React porque podemos mostrar ou não paginas inteiras fazendo essa verificação rápida.

Linguagem: [[Javascript]]