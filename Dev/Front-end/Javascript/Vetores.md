Vetores são um conjunto de dados reunidos em uma variável. Geralmente esses valores possuem um tema semelhante, e isso ajuda não apenas na organização do nosso código mas para executarmos algumas tarefas de maneira dinâmica. Vamos aos exemplos:

```jsx
// Para declarar nosso vetor usamos colchetes, 
// e dentro deles seguimos passando os valores.

// Estrutura Básica
let vetor = [
valor1,
valor2,
valor3
]

// Exemplo:
let generos = [
'ação',
'terror',
'aventura'
]
```

Os vetores possuem uma estrutura interna onde se tem um valor indexado inteiro a outro valor. Destrinchando o vetor acima temos a seguinte estrutura:

- Vetor: generos
    - Posição 0: ação
    - Posição 1: terror
    - Posição 2: aventura

Ou seja, temos um vetor com um tamanho de 3 valores, onde podemos chamar seus valores passando sua posição entre colchetes para acessar o valor. Podemos também vincular um novo valor à uma nova posição ou uma posição antiga fazendo o mesmo.

```jsx
// Mostra o que há na posição 1 do vetor
console.log(generos[1])
// output: terror

// vincula "suspense" à posição 3 do vetor
generos[3] = 'suspense'

// substitui "drama" na posição 1 do vetor
generos[1] = 'drama'
```

### Manipulando Vetores

Agora veremos algumas propriedades e métodos úteis e mais utilizados na manipulação de vetores, assim como alguns exemplos. Vejamos:

### Array.push e Array.pop

Para adicionar e remover elementos de um vetor podemos usar os métodos push e pop, consecutivamente. Eles manipulam a última posição do vetor.

```jsx
// Exemplo:
let nomes = [
'itallo',
'thaissa',
'vitória'
]

// Propriedade length: mostra o tamanho do vetor
console.log(nomes.length)
// output: 3

// Método push: adiciona valores no final do vetor
nomes.push('edu')

// Método unshift: adiciona valores no início do vetor
nomes.unshift('pedro')

// Estado atual do nosso vetor
nomes = [
'pedro',
'itallo',
'thaissa',
'vitória',
'edu'
]

// Método pop: retira o último valor do vetor
nomes.pop()

// Método shift: retira o primeiro valor do vetor
nomes.shift()

// Método splice: adiciona, altera ou exclui um valor
// vetor.splice(valor de inicio, quantidade a excluir, valor a ser adicionado)

// substitui o valor "itallo" por "júlia"
nomes.splice(1, 1, 'júlia')

// exclui o valor "thaissa" do vetor
nomes.splice(2, 1)
```

### Array.join e Array.Split

O Método _Join_ é responsável por pegar um vetor e concatenar seus dados retornando uma _string_. Podemos passar uma _string_ de vírgula, espaço ou qualquer outra coisa para que ele adicione entre os valores. Já o método s_plit_ é responsável por realizar o caminho inverso: ele separa os elementos de uma _string_ e retorna um vetor.

```jsx
let nomes = 'itallo, thaissa, pedro, eduardo'

//             string que separa um valor do outro
let vetorNomes = nomes.split(', ')

console.log(vetorNomes)
// output: ['itallo', 'thaissa', 'pedro', 'eduardo']

// -------------------

let vetorNomes = ['itallo', 'thaissa', 'vitoria']

//        string que vai separar os valores do vetor
let nomes = vetorNomes.join(', ')

console.log(nomes)
// output: itallo, thaissa, vitoria

```

### Array.reverse e Array.Sort

O método _reverse_ serve, como o nome sugere, reverter a ordem de um vetor. O método _sort_ serve para reorganizar o vetor. Por padrão ele retorna um vetor organizado alfabeticamente, mas podemos passar uma função que retorna um valor positivo ou negativo e baseado nesse valor, reorganiza nosso vetor.

```jsx
let vetorNomes = ['itallo', 'thaissa', 'vitoria']

vetorNomes.reverse()

console.log(vetorNomes)
// Output: ['vitoria', 'thaissa', 'itallo']

//--------------------

let vetorNomes = ['joaquin', 'alberto', 'barbara']

// valor padrào
vetorNomes.sort()

console.log(vetorNomes)
// Output: ['alberto', 'barbara', 'joaquin']
```

Agora imagine que ao invés de colocar em ordem alfabética, queremos colocar do menor nome para o maior nome. Faremos uma função que recebe dois valores, e verificamos se um valor é menor ou igual ao outro. Atenção:

- Para colocarmos o primeiro valor antes do segundo, devemos retornar um número negativo.
- Para colocarmos o segundo valor antes do primeiro, devemos retornar um número positivo.
- Para mantermos a ordem inalterada devemos retornar 0.

```jsx
let vetorNomes = ['whelinghton', 'ema', 'adria', 'ricardo']

// funcão responsável por retornar se o valor a é
// maior ou menor que o segundo
function organizaNomes(a, b)
{
    if(a.length < b.length )
    {
				// coloque o primeiro valor antes do segundo
        return -1
    }
    else if(a.length > b.length)
		{
				// coloque o segundo valor antes do primeiro
        return 1
    }

		// não altere a ordem
    return 0
}

console.log(vetorNomes.sort(organizaNomes))
// output: ['ema', 'adria', 'ricardo', 'whelinghton'] 
```

### Array.concat, Array.slice e Array.splice

O método `concat`, como bem podemos sugerir, é responsável por concatenar - juntar - dois vetores diferentes.

Já o `*slice*` é responsável por dividir e retornar uma parte específica de um vetor. Basta dizermos qual o índice de início e qual índice de fim. Caso o fim não seja especificado, ele retornará todos os valores até o final do vetor.

O método `*splice`* retira determinada quantidade de valores a partir de um ponto especificado.

```jsx
// concat
let vetorNomes = ['whelinghton', 'ema', 'adria', 'ricardo'] 
let maisNomes = ['vitor', 'silva', 'edu']

let todosNomes = vetorNomes.concat(maisNomes)

console.log(vetorNomes)
// output: ['whelinghton', 'ema', 'adria', 'ricardo']
console.log(maisNomes)
// output: ['vitor', 'silva', 'edu']
console.log(todosNomes)
// output: ['whelinghton', 'ema', 'adria', 'ricardo', 'vitor', 'silva', 'edu']
```

```jsx
// slice

let novoVetor = vetorNomes.slice(1,3)
console.log(novoVetor)
// output: ['ema', 'adria']
```

```jsx
// splice

// start / delete count
vetorNomes.splice(1, 1)
console.log(vetorNomes)
// output: [ 'whelinghton', 'adria', 'ricardo' ]
```

### Array.map e Array.filter

O método _map_ é responsável por capturar cada valor e adicionar a uma função passada como parâmetro, retornando um novo vetor. Já o método _filter retorna um vetor de valores que tiveram em sua função de verificação a resposta como verdadeira_

**

```
let par = [2, 4, 6, 8]

function soma(n)
{
    return n + 1
}

impar = par.map(soma)

console.log(impar)
// output: [3, 5, 7, 9]

//---------------------------------

let par = [2, 4, 6, 8]

// funcão que filtra se o número é maior que 5
function filtro(n)
{
    return n > 5 ? true : false
}

let maior5 = (par.filter(filtro))

console.log(maior5)
// output: [6, 8]

```

Linguage: [[Javascript]]