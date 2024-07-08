Um dos tópicos mais importantes de qualquer linguagem, funções são responsáveis por realizar determinadas tarefas específicas, são blocos de código reutilizáveis onde podemos executar em diversas partes do código sem que tenhamos que reescrever tudo novamente.

Vamos supor que temos uma tarefa simples: somar dois números. Perceba que o código abaixo tem vários problemas. Temos que re-associar um novo valor cada vez que formos realizar um novo cálculo, o que pode se tornar bem trabalhoso. Além disso, vamos supor que futuramente nós queiramos ao invés de somar, subtrair.

Teremos que ir em cada lugar e trocar cada trecho de código que antes somava para agora subtrair. Percebe que o código fica complicado de realizar manutenções e mudanças?

```jsx
let n1 = 5, n2 = 5
console.log(n1 + n2) // output: 10

n1 = 10
n2 = 15
console.log(n1 + n2) // output: 25

n1 = 20
n2 = 20
console.log(n1 + n2) // output: 40
```

### Estrutura Base

Veremos que temos diversos tipos de funções. A estrutura básica delas incluem a palavra reservada _function_ + _nome da funcão._ Depois disso dizemos se ela irá receber algum parâmetro ou não, e depois criamos um bloco de código com suas tarefas. Uma função pode ou não retornar um valor. Caso ela retorne, será um ponto de escape da função, ou seja, tudo o que vier depois, não será executado. Vamos reescrever o código acima:

```jsx
function calculo(valor1, valor2)
{
	return valor1 + valor2
}

 
console.log(calculo(5,5))        // output: 10
console.log(calculo(10,15))      // output: 25
```

Agora caso tenhamos que mudar, ou mesmo acrescentar outros cálculos, podemos fazer a mudança em apenas um lugar, que ele será reaproveitar em todos os outros. Nosso código está mais limpo e é mais rápido - e fácil - de mexer.

### Funções Anônimas e Arrow Functions

São funções que não possuem nome, geralmente chamadas assim que são criadas. Podem também ser vinculadas à uma variável para que sejam usadas como _funções de callback -_ veremos melhor sobre elas no próximo tópico.

Por exemplo, o método _AddEventListener_ é capaz de atribuir uma função a determinada ação feita no navegador. Neste caso iremos escrever no console quando o botão for clicado. O primeiro parâmetro desta função é a ação que irá disparar a tarefa, e o segundo parâmetro é a tarefa em si.

```jsx
// capturamos o botão
const btn = document.querySelector('button')

btn.addEventListener('click', function(){
	console.log('botão clicado!')
})
```

Como podemos ver, a função não possui nome, apenas a palavra reservada e o seu bloco de código. Com a atualização do ES6 foi implementado uma maneira ainda mais curta de escrever funções anônimas: _arrow functions._ Servem o mesmo propósito, mas sua sintaxe é mais curta.

```jsx
// capturamos o botão
const btn = document.querySelector('button')

//                              arrow
btn.addEventListener('click', ()=>{
	console.log('botão clicado!')
}))
```

### Funções de Callback

São funções passadas como parâmetro para outras funções. Elas são executadas dentro das funções principais. O método _addEventListener,_ como dito, tem como parâmetros a ação e uma função de _callback._

Podemos passar esse _callback_ como função anônima/arrow function no mesmo lugar, ou definir nossa função anônima em outro lugar e chamá-la no callback. Vejamos:

```jsx
// capturamos o botão
const btn = document.querySelector('button')

let callback = ()=>{
	console.log('callback chamado!')
}

btn.addEventListener('click', callback)
```

Outro exemplo: temos uma função principal que pega o nome do usuário através do _prompt_ e com esse nome chama uma outra função para mostrar no console.

```jsx
let dizNome = (n) =>{
	console.log('Oi, ' + n)
}

function principal(callback)
{
	let nome = prompt('Qual seu nome?')
	
	callback(nome)
}

principal(dizNome)
```

### Closures

> “_Quando se tem uma função definida dentro de outra função, a função interna tem acesso a variáveis e ao escopo da função externa, mesmo que a função externa tenha acabado de ser executada e suas variáveis não estejam mais acessíveis.” - Kyle, Web Dev Simplified_

Para entender o conceito de _closures,_ devemos ter claro como o escopo de javascript funciona. Javascript trabalha com o conceito de escopo léxico, o que quer dizer que blocos de código internos possuem acesso a blocos de código externo, mas o caminho contrário não acontece. Você pode ver uma explicação mais detalhada [aqui](https://www.notion.so/Declara-es-Escopos-e-Condicionais-1598689445c44bcf8b035e795abdb831?pvs=21).

Vamos imaginar um cenário como um jogo, por exemplo. Vamos supor que você tem uma função que toda vez que é chamada, ela checa se você possui dinheiro suficiente para comprar um item. Todos os jogadores começam com o mesmo valor.

Usando uma função básica, podemos perceber que apesar de funcionar, ela não alcança o resultado esperado. Isso porque com o valor declarado dentro da função, toda vez que chamamos ela, _o montante de dinheiro reseta._ Então se comprarmos um item e depois comprarmos outro, na segunda compra será como se tivéssemos de volta as 10 moedas.

```jsx
function checkDinheiro(compra)
{
	let dinheiro = 10
	dinheiro = dinheiro - compra 

	if(dinheiro <= 0)
	{
		console.log('Você não tem dinheiro suficiente!')
	}
	else{
		console.log(`Compra realizada, você ainda tem ${dinheiro}`)
	}
}

let meuPersonagem = checkDinheiro
meuPersonagem(5) // Compra realizada, você ainda tem 5
meuPersonagem(2) // você ainda tem 8
meuPersonagem(4) // você ainda tem 6
```

Movendo a variável “dinheiro” para fora da função, conseguimos chegar no resultado desejado - por ora. Imagine que nesse jogo você possui mais de um personagem. Caso chamemos a função “checkDinheiro” novamente nos deparamos em um novo problema. Já que a variável “dinheiro” está global, o primeiro personagem já usou todo o valor. Ela está sendo compartilhada com o primeiro personagem e o segundo personagem.

```jsx
let dinheiro = 10
function checkDinheiro(compra)
{
	dinheiro = dinheiro - compra 

	if(dinheiro <= 0)
	{
		console.log('Você não tem dinheiro suficiente!')
	}
	else{
		console.log(`Compra realizada, você ainda tem ${dinheiro}`)
	}
}

let meuPersonagem = checkDinheiro
meuPersonagem(5) // Compra realizada, você ainda tem 5
meuPersonagem(2) // Compra realizada, você ainda tem 3
meuPersonagem(4) // Você não tem dinheiro suficiente!

console.log("")

let segundoPersonagem = checkDinheiro
segundoPersonagem(2) // Você não tem dinheiro suficiente!
segundoPersonagem(5) // Você não tem dinheiro suficiente!
```

Para corrigir isso temos várias possibilidades. Poderíamos criar outra variável “dinheiro” e passar como parâmetro na função. Mas e se você tiver 10 personagens? E se você quiser que ao invés de começarem com 10 moedas, eles comecem com 5? E o trabalho para manter todos esses valores atualizados? Código complicado, manutenção ruim.

Neste momento podemos utilizar as _closures_. Definimos a quantia de dinheiro na função externa e retornamos uma função interna que recebe o valor da compra. Depois é só associar essa função ao personagem que você quiser.

```jsx
function checkDinheiro()
{
	let dinheiro = 10

	return (compra)=>{
		dinheiro = dinheiro - compra 

		if(dinheiro <= 0)
		{
			console.log('Você não tem dinheiro suficiente!')
		}
		else{
			console.log(`Compra realizada, você ainda tem ${dinheiro}`)
		}
	}
}

let meuPersonagem = checkDinheiro()
meuPersonagem(5) // Compra realizada, você ainda tem 5
meuPersonagem(2) // Compra realizada, você ainda tem 3
meuPersonagem(4) // Você não tem dinheiro suficiente!

console.log("")
let segundoPersonagem = checkDinheiro()

segundoPersonagem(2) // Compra realizada, você ainda tem 8
segundoPersonagem(5) // Compra realizada, você ainda tem 3
```

Essa é uma das possibilidades das _closures_ serem usadas: quando queremos encapsular um valor e separá-lo para que possamos chamar outras instâncias que vão usá-lo de formas diferentes. Veremos outras aplicações quando estudarmos JS Assíncrono.

### Rest Parameters

Como vimos anteriormente, podemos fazer com que uma função receba vários parâmetros expondo na sua assinatura. Usando o operador `*...`* podemos indicar que os valores recebidos serão transformados em um vetor para melhor manipulação dentro da função. Por exemplo:

Vamos criar uma função que recebe o nome de uma empresa e lista os funcionários dela. Tanto a empresa como esses funcionários serão passados como parâmetro da função. Só que imagine que podemos passar como argumento 2 funcionários, mas também podemos passar 6,7.

Nesse caso, como a quantidade de argumentos é variável, podemos usar o `*rest operator`* e indicar que independente da quantidade de parâmetros, eles serão transformados em um vetor.

```jsx
function listaFuncionarios(empresa, ...funcionarios){

	console.log(`A empresa ${empresa} possui os seguintes funcionários:`)
	  
	funcionarios.forEach((funcionario, i)=>{
	      console.log(`${i}: ${funcionario}`)
	  })
}

// o primeiro argumento é a empresa, e depois do primeiro tudo será
// associado ao vetor "funcionários"
listaFuncionarios('google', 'fernando', 'carlos', 'joao', 'vitor')

// output:
// A empresa google possui os seguintes funcionários:
// 0: fernando
// 1: carlos 
// 2: joao  
// 3: vitor
```

Linguagem: [[Javascript]]