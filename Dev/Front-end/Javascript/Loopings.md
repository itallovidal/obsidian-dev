Loopings são estruturas que permitem que blocos de código possam ser executados diversas vezes sem que sejam repetidos. Conhecidos também como _laços_, são usados para percorrer uma _string_, fazer verificações em um conjunto de dados, percorrer vetores e muito mais. Possuímos diversas estruturas diferentes e todas elas são válidas, a única coisa que define quando usar uma ou quando usar a outra é o contexto.


### for

Para que essa estrutura funcione devemos informas 3 valores: o _ponto de início, o fim, e o valor a ser incrementado_. Uma das coisas que difere essa estrutura das outras é o fato de que deve-se obrigatoriamente ser trabalhado com um contador, já que esse contador é que vai mostrar qual o valor atual do looping. Por exemplo, vamos supor que queremos percorrer um vetor e mostrar na tela todos os seus valores.

Começaremos no índice 0, vamos até o tamanho dele, e iremos mostrar cada valor, então vamos incrementar no nosso contador de 1 em 1.

```jsx
let nomes = ['itallo', 'thaissa', 'vitoria']

//                contador deve ser     contador será 
//                menor que o tamanho   incrementado de
//     inicio ;   do vetor            ; 1 em 1
for(let cont = 0; cont < nomes.length; cont++)
{
	console.log(nomes[cont])
}

// output:itallo
//        thaissa
//        vitoria
```

### forEach

Esta estrutura é usada em vetores, sendo muito fácil e muito útil. Ela faz parte do conjunto de métodos herdados do objeto Array - não se preocupe, falaremos a fundo sobre herança em um outro momento - ou seja, toda vez que criamos um vetor esse método já está embutido. Com ele podemos passar uma função para que seja aplicada a cada valor do vetor, extremamente parecido como o método _map_ faz. Vejamos um exemplo:

```jsx
let nomes = ['itallo', 'thaissa', 'vitoria']

nomes.forEach(function exibeNome(valor){
    console.log(valor)
})

// output:itallo
//        thaissa
//        vitoria
```

### For.. of

Esta estrutura é uma versão bem parecida com o _for_ convencional, porém com ela não precisamos usar um contador explícito. _Dado um vetor, é percorrido retornando os valores do vetor._

Vejamos novamente o exemplo dos nomes:

```jsx
let nomes = ['itallo', 'thaissa', 'vitoria']

// variável criada 
// para mostrar os nomes
for(nome of nomes)
{
    console.log(nome)
}

// output:itallo
//        thaissa
//        vitoria
```

### For.. in

Já o for…in usa uma lógica super parecida com o _for…of,_ com a diferença que ele não mostra o valor dos índices e sim os próprios índices em si. Ao invés dele mostrar o nome, ele vai mostrar a posição do vetor que o nome ocupa. Esse laço é muito útil se usado em conjunto com o _for…of_ para mostrar o conteúdo de dentro de um objeto.

```jsx
let nomes = ['itallo', 'thaissa', 'vitoria']

// variável criada 
// para mostrar os nomes
for(indice in nomes)
{
    console.log(indice)
}

// output:0
//        1
//        2
```

### While

Esta estrutura tem como o intuito repetir determinado trecho de código até que dada expressão seja considerada como falsa. Muito importante se atentar no uso deste laço já que se não pensarmos na lógica correta e não usarmos um contador da forma certa, nosso looping ficará infinito, acarretando o travamento da aplicação. Segue o exemplo:

```jsx
let nomes = ['itallo', 'thaissa', 'vitoria']

let cont = 0 
while(cont < nomes.length)
{
    console.log(nomes[cont])

    cont++
}
```

### Do While

Bem parecido com o seu irmão, o _Do While_ tem como objetivo _primeiro rodar o código que está no bloco_ _e_ _depois fazer a verificação_ da expressão para saber se rodará novamente. O _while primeiro verifica a expressão, e depois roda o trecho de código._

```jsx
let nomes = ['itallo', 'thaissa', 'vitoria']

let cont = 0 

do{
    console.log(nomes[cont])
    cont++
}while(cont < nomes.length)
```

Linguagem: [[Javascript]]