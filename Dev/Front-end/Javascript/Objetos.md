Objetos são agregadores de propriedades, métodos e outros objetos que tem uma lógica comum. Cada elemento deste conjunto possui um nome relacionado. Os objetos estão em toda parte!

Cada elemento na linguagem que não está entre os tipos primitivos são objetos. É muito comum um objeto herdar propriedades e métodos de outros objetos.

### Prototype Chain, **proto** e Herança

Quando nós criamos um vetor, assim como as strings e outros tipos, temos à nossa disposição um conjunto de métodos e propriedades para que possamos manipular o vetor criado.

Isso porque um vetor herda essas propriedades de um objeto chamado _Array,_ assim como as strings herdam de um objeto chamado _String._

Ou seja, todo objeto - com uma exceção - herda propriedades e métodos de um outro objeto que chamamos de _protótipo._ Para vermos de qual objeto nosso objeto atual herda suas propriedades, podemos usar a palavra reservada _**proto**._ Vejamos:

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e6872e0a-a96f-463c-b786-d4949bde74bc/Untitled.png)

Podemos perceber que ao criar a variável ‘a’ ela herda do objeto _String_ diversos outros métodos. _Prototype Chain_ é a cadeia que se cria quando um objeto herda valores de outro objeto que herda valores de outro objeto e assim sucessivamente. O único objeto que não herda nada de ninguém é o objeto.. _Object._

### Objeto Literal

Podemos criar um objeto literal passando suas propriedades para uma variável através dos colchetes. A linguagem cria e instancia esse objeto.

```jsx
let objeto = {
	propriedade1: valor,
	propriedade2: valor2,
	funcao(){
		console.log('sou uma funcao do objeto')
	},
	outroObjeto: {
		propriedade1: valor,
		propriedade2: valor
	}
}
```

### Usando _new_

O operador _new_ também cria e instância um novo objeto. Com ele devemos indicar o que está sendo criado. Neste caso, usaremos o objeto _Object_ que indica qual tipo dessa variável, já que podemos usar o operador _new_ para inicializar e criar vetores, dates e outros tipos. Falaremos mais sobre o New daqui a pouco.

```jsx
let objeto = new Object({
	propriedade1: valor,
	propriedade2: valor2,
	funcao(){
		console.log('sou uma funcao do objeto')
	},
	outroObjeto: {
		propriedade1: valor3,
		propriedade2: valor4
	}
})

```

### Object.Create()

Esta é uma função que cria um objeto novo, como já pode imaginar. Ela recebe um protótipo a ser herdado e opcionalmente você pode adicionar as propriedades novas deste objeto atual.

```jsx
let primeiroObjeto = {
	propriedade1: 1,
	propriedade2: 2,
	funcao(){
		console.log('sou uma funcao do objeto')
	},
	objetoInterno: {
		propriedade1: 3,
		propriedade2: 4
	}
}

let segundoObjeto = Object.create(primeiroObjeto)
```

Como podemos ver abaixo, o “segundo objeto” foi criado e herdou todas as propriedades e métodos do “primeiro objeto”, assim como as propriedades e métodos do objeto “Object”

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c85b7e44-2f02-4b5d-b03a-db61cbf7c9d6/Untitled.png)

### Factory function e _this_

Vamos pensar em um cenário onde você deve criar dois objetos contendo informações de um usuário, por exemplo. Vamos analisar o código abaixo:

```jsx
let usuario01 = {
	nome: 'itallo',
	admin: true,
	showUser()
	{
		console.log(`Olá, eu sou o(a) ${this.nome}!`)
	}
}

let usuario02 = {
	nome: 'Thaissa',
	admin: false,
	showUser()
	{
		console.log(`Olá, eu sou o(a) ${this.nome}!`)
	}
}

usuario01.showUser() // Olá, eu sou o(a) itallo!
usuario02.showUser() // Olá, eu sou o(a) thaissa!
```

De cara podemos notar que há duplicação no código. Toda vez que temos trechos extensos duplicados provavelmente poderíamos realizar a mesma tarefa de uma forma mais apropriada. Para corrigir esse problema, podemos confeccionar uma função que cria o objeto e nos devolve ele pronto.

```jsx
function criaUsuario(n, a){
	return {
		nome: n,
		admin: a,
		showUser()
		{
			console.log(`Olá, eu sou o(a) ${this.nome}!`)
		}
	}
}

let usuario01 = criaUsuario('itallo', true)
let usuario02 = criaUsuario('Thaissa', false)

usuario01.showUser() // Olá, eu sou o(a) itallo!
usuario02.showUser() // Olá, eu sou o(a) thaissa!
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/412d44e6-8e4e-4bec-851d-d563ad324525/Untitled.png)

Você pode notar no código acima que fizemos uma função que recebe dois parâmetros e as vincula nas propriedades de “nome” e “admin”, assim como as chama dentro da função. Podemos notar que uma palavra reservada nova está sendo usada: _this._

### This: o que é isso?

A palavra reservada _this se refere ao objeto atual do escopo._ Neste caso, _this_ faz referência ao objeto que acabou de ser criado. Podemos acessar o valor de um objeto através da estrutura “objeto.propriedade”, só que como o _this_ implica neste objeto atual, escrevemos “this.propriedade”, no caso, “nome.”.

### Constructor Function

Construtores são geralmente mais usados na lógica de _classes -_ que veremos em breve - mas que também podem ter seu espaço na programação funcional. São funções bem parecidas com as factory porém tem algumas particularidades que veremos agora.

```jsx
function Usuario(n, a){
	this.nome =  n
	this.admin = a
	this.showUser = ()=> {
		console.log(`Olá, eu sou o(a) ${this.nome}!`)
	}
}

let usuario01 = new Usuario('itallo', true)
let usuario02 = new Usuario('Thaissa', false)

usuario01.showUser() // Olá, eu sou o(a) itallo!
usuario02.showUser() // Olá, eu sou o(a) thaissa!

console.log(usuario01.nome) // itallo
```

Por ser uma função construtora devemos colocar o nome em _Pascal Case -_ primeira letra maiúscula de cada palavra - e dentro definimos as propriedades com a palavra reservada _this._

Estruturando corretamente, por padrão a linguagem javascript entende que é um construtor e faz duas coisas por baixo dos panos:

- Criar um objeto vazio para que as propriedades e métodos sejam adicionados
- Retorna o objeto montado, mesmo que “pareça” que não tem retorno

Então na verdade nossa função está assim:

```jsx
function Usuario(n, a){
	// criacão do objeto omitida
	this = {}

	this.nome =  n
	this.admin = a
	this.showUser = ()=> {
		console.log(`Olá, eu sou o(a) ${this.nome}!`)
	}

	// retorno omitido do objeto criado
	return this
}
```

O interessante de fazer desta forma é que se formos ver o _**proto**_ do objeto retornado, podemos notar que a linguagem nos informa qual o tipo do objeto que criamos, que no nosso caso, é do tipo “Usuario”. Vejamos o resultado do tipo da criação com _constructor function_ e _factory function_, sucessivamente:

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d664f7a7-63a3-4634-85f9-550f0937d2d1/Untitled.png)

Podemos inclusive acessar seus construtores e ver que usando _factory functions_ não conseguimos ver como o objeto é construído já que essa forma não trabalha diretamente com construtores como a outra trabalha:

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ed80af93-7cca-4960-b436-6bf5ee25ea63/Untitled.png)

Isso trás um impacto significativo no nosso programa: _a ausência do uso de herança._.

O que acontece é que quando se cria uma função que retorna um objeto, eles se tornam independentes pois não herdam nada de um objeto comum criado por nós - apenas do objeto Object.

Ou seja: você está criando dois objetos diferentes com a mesma “roupagem” e colocando cada um em um espaço de memória diferente.

Quando um objeto é criado a partir de um protótipo, ele leva consigo métodos e propriedades do protótipo que ele se baseou, logo, caso façamos alterações ou adicionarmos métodos e propriedades no protótipo - vulgo objeto pai - todos os objetos que herdam elementos dele também serão atualizados.

```jsx
function criaUsuario(n, a){
	return {
		nome: n,
		admin: a,
		showUser()
		{
			console.log(`Olá, eu sou o(a) ${this.nome}!`)
		}
	}
}

let usuario01 = criaUsuario('thaissa', false)
let usuario02 = criaUsuario('pedro', false)

usuario01.showUser() // Olá, eu sou o(a) thaissa!
usuario02.showUser() // Olá, eu sou o(a) pedro!
 
usuario02.showUser = function(){
	console.log('método modificado')
}

usuario01.showUser() // Olá, eu sou o(a) thaissa!
usuario02.showUser() // método modificado
```

Usando uma função construtora, podemos definir propriedades nela que serão implementadas nos objetos filhos e caso precisemos adicionar mais uma propriedade no pai, todos os filhos serão atualizados.

```jsx
function Usuario(n, a){

	this.nome =  n
	this.admin = a
	this.showUser = ()=> {
		console.log(`Olá, eu sou o(a) ${this.nome}!`)
	}

}

let usuario01 = new Usuario('itallo', true)
let usuario02 = new Usuario('thaissa', false)

// adicionando um método no protótipo 
Usuario.prototype.adminCheck = function(){
	console.log(this.admin)
}
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1be2a40c-2f55-44df-a91e-7964b7bf70e3/Untitled.png)

### Métodos úteis:

- `*Object.entries()*`
    - Retorna um vetor com a chave e o seu valor. [chave, valor] = `*object.entries()*`

Linguagem: [[Javascript]]