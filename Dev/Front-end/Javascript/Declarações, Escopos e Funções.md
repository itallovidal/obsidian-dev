Palavras Chave: [[Javascript]]

## Introdução e conceitos básicos

### Uma Linguagem Fracamente Tipada

A primeira coisa que é importante saber quando falamos de _Javascript_ é que ela tem como característica ser uma linguagem fracamente tipada. Ou seja, variáveis declaradas podem mudar seu tipo conforme o valor que recebem. Por exemplo, uma variável que antes continha uma _string,_ pode vir a receber um _int_ sem problemas, apenas recebendo esse novo valor numérico.

Diferentemente de C# - que é uma linguagem fortemente tipada - não precisamos nos atentar, em sua declaração, ao tipo de dado que essa nova variável irá receber. Percebe-se abaixo que apenas usamos a palavra reservada indicada, sem nenhum tipo antes do nome da variável. O que podemos e devemos indicar é se a variável poderá ter um novo valor relacionado à ela ou não, com as diretivas _var, let ou const_.

```csharp
// C#
string nome = 'Itallo'
int numero = 10
boolean valor = true
```

```jsx
// Javascript
var nome = 'Itallo'    // string
var idade = 20         // int
var faculdade = false  // boolean
var time               // undefined
var cor = null;        // nulo
var simbolo = Symbol() // simbolo
var obj = {}           // objeto

let nome2 = "pedro"   // variável poderá ter nova associação
const pi = 3.14 // variável não poderá ter uma nova associação

// Para sabermos qual tipo da variável: type of
console.log(typeof nome)
// output: string
```

Podemos notar que independente do tipo de dado a declaracão pode ser a mesma. Logo abaixo podemos notar que usamos a palavra reservada _const_ para indicar que a variável “pi” ** não poderá ser modificada. Faz sentido já que “pi” é um valor que é imutável, constante, não varia.

### Template String

Concatenar - juntar - textos geralmente é algo bem chato e trabalhoso. Antes do ES6 teríamos que pegar a variável desejada e literalmente somar com um pedaço de texto quantas vezes fosse necessários para que formasse uma frase. Com a atualização da linguagem, hoje temos disponível as _Template Strings._ Agora, podemos criar uma frase e inserir nossa variável dentro dela de forma mais simples e direta. Só precisamos usar aspas em conjunto com cifrão e chaves. Vejamos:

```jsx
var nome = 'itallo'
var idade = 12
// método antigo
console.log('Meu nome é ' + nome + ' e tenho ' + idade + ' anos.')

// novo método, bem mais rápido e intuitivo
console.log(`Meu nome é ${nome} e tenho ${idade} anos.`)
```

### Tipos Primitivos e Tipos de Objeto

Em javascript temos 5 tipos primitivos:

- String
- Undefined
- Number
- Boolean
- Null

Tudo que não seja um texto (conjunto de caracteres), número, um valor booleano (verdadeiro ou falso), nulo ou indefinido é considerado um objeto. Um objeto é um conjunto de propriedade e métodos onde se possui um nome e um valor primitivo relacionado à ele - ou outro objeto.

Javascript possui alguns objetos especiais, dentre eles temos o vetor - que nada mais é do que um conjunto de dados indexados e iterativos - e as funções - que são blocos de código que executam determinada tarefa.

Tipos primitivos são _imutáveis, mesmo que nós possamos alterar seus valores._ Vejamos: vamos supor que eu inicialize uma variável “texto” com o valor “oi!”. Depois eu alterei seu valor adicionando o valor “Tudo bem?”:

```jsx
let texto = "oi!"
texto = texto + " Tudo bem?"

console.log(texto)
//output: Oi! Tudo bem?
```

O que acontece é que a linguagem busca na memória onde o valor do “texto” está, adiciona o outro valor e associa o novo valor - no caso “Oi! Tudo bem?” - a um novo espaço de memória. Como não precisamos nos preocupar em fazer a coleta de lixo - ou seja, limpeza na memória de variáveis e dados inúteis - o JS retirará da memória a variável com o valor antigo.

### IF-Statement

É muito comum na programação encontrarmos pontos de bifurcação no fluxo do código. Dependendo do valor, façamos X coisa ou Y coisa. Para isso, precisamos fazer a verificação de estado daquela variável ou expressão. Neste ponto é que lidamos com o _If-Statement._ Ele seria um bloco de código que só será executado SE determinada condição for atendida.

```jsx
// estrutura base
//caso algo for verdadeiro
		if (     expressão      )
		{
			// faca alguma coisa	

		}
		else{
			// caso não seja verdadeiro faca outra coisa	
		}
```

```jsx
let n = 10
		if ( n > 5)
		{
			console.log('o número é maior que 5 sim')	
		}else{
			console.log('o numero não é maior que 5 não')	
}
```

### Else-If

As vezes é necessário que tenhamos mais de uma estrutura de condição. Para isso usamos _Else if._

```jsx
// estrutura base
// caso algo for verdadeiro
		if (     expressão      )
		{
			// faca alguma coisa	

		}
		else if(outra expressão) {
			// se essa outra expressão for verdadeira faca isso aqui
		}
		else{
			// se não for, agora sim faca isso aqui
}

```

```jsx
let n = 3
		if ( n > 5)
		{
			console.log('O número é maior que 5')	
		}else if( n < 0 ){
			console.log('o numero é menor que 0')	
		}else{
			console.log('o numero está entre 0 e 5')
		}
```

Podemos resumir um _If-statement usando os operadores lógicos ternários_ da seguinte forma:

```jsx
let n = 10

// caso o número for menor que 5 eu retorno verdadeiro, caso contrário eu retorno falso
let valor = n < 5 ? true : false
```

O que estiver após o interrogação será o valor atribuído quando for verdadeiro, o que tiver após os dois pontos será o valor atribuído caso o resultado da expressão for falsa.

### Tipos de Escopo em Javascript

O escopo nada mais é do que o local de visibilidade da variável. É a delimitação de onde a variável poderá ser acessada em relação ao código. Nós temos três tipos de escopo: _Escopo de Função, Escopo Léxico e o escopo de Bloco._ Vamos começar com o escopo de função primeiro.

### Escopo de Função

Veremos melhor sobre funções detalhadamente em breve. Por agora, é interessante saber que as funções são - geralmente - trechos de código voltados a realização de tarefas que se repetem muitas vezes. No escopo de função, as variáveis declaradas dentro da função podem ser utilizadas apenas dentro da função, e não fora. Caso chamemos uma variável que foi declarada dentro da função no fluxo do código de fora dela, resultará em um erro, já que a variável não é encontrada.

```jsx
function minhaFuncao()
{
	var variavel = 10

	console.log(variavel)
	// output: 10
}

// erro, pois a variável só está disponível dentro da funcão
console.log(variavel)
```

### Escopo Léxico

O escopo léxico se refere à visibilidade da variável dentro de um aninhamento de funções. Quando Possuímos uma função dentro da outra, javascript procurará a variável solicitada dentro do escopo atual - ou seja, onde foi solicitado. Caso a linguagem não ache a variável, ela procurará no escopo pai. Caso não ache, ela procurará no “pai do pai”, e assim por diante. Vale enfatizar que é uma procura _do escopo interno para o escopo externo, já que o contrário não acontece. Por exemplo:_

```jsx
function recebeNumero(valor)
{
    var numero = valor

    function soma()
    {
			// nesta função não possuímos nenhum "numero"
			// mas no escopo pai sim
       return numero + 10    
    }

    console.log(soma())
}

recebeNumero(10)
// output: 20
```

### Escopo de Bloco

Da sua criação em 1997 até meados de 2015 - quando a linguagem recebeu sua atualização para a ES6 - o Javascript não possuía a lógica de escopo de Bloco. Ou seja, variáveis declaradas em blocos de _If-Statement -_ por exemplo - tinham sua visibilidade disponível dentro e fora do bloco. Elas “vazavam”. Para entender melhor o porquê isso acontecia e o motivo de hoje em dia ser encorajado o uso de _let,_ temos que entender o que é hoisting.

### Hoisting

Apesar de não declararmos o tipo da nossa variável, temos diferentes palavras reservadas para sua criação. Antigamente, na maior parte dos códigos de Javascript, usava-se _var_ para se criar uma variável, mas essa é uma prática que vem decaindo com o passar do tempo, sendo até mesmo desencorajada pelos desenvolvedores.

Para que possamos entender seus motivos, precisamos entender primeiro o que é _Hoisting_ - _içamento_, em português. Vejamos o exemplo abaixo: nele foi declarado dentro de um escopo de _IF-Statement u_ma variável chamada “valor”, e logo depois imprimimos no console seu conteúdo.

```jsx
var n = 5

if(n == 5)
{
    var valor = 1
}

console.log(valor) 
// mesmo o "valor" sendo declarado dentro do escopo do IF, ele
// poderá ser acessado fora deste bloco 
```

Por padrão, javascript “iça” as variáveis declaradas com _var_ para a memória durante a fase de compilação. Com isso, falamos que ela vai para o “topo do código”, pois seria como se elas fossem declaradas no começo do programa. Essa característica faz com que as variáveis fiquem globais, podendo ser acessadas em qualquer lugar do código, mesmo que elas ainda - teoricamente - não tenham sido declaradas. Elas foram declaradas, apenas ainda não foram inicializadas com o valor fornecido por você. Por exemplo:

```jsx
// js declara a variável porém sem inicialização
console.log(frase) 
//output: undefined

// inicializamos a variável com um texto
var frase = "Agora possui valor." 

// agora printamos na tela a variável
console.log(frase)  
// output: Agora possui valor.
```

Além disto, com _var_ temos a possibilidade de redeclarar variáveis, o que também não é uma boa prática. Para solucionar esse problema, foi introduzido a palavra reservada _let,_ responsável por delimitar a variável apenas ao escopo de bloco. Por conta disso, hoje é encorajado o uso de _let_ ao invés de _var._




