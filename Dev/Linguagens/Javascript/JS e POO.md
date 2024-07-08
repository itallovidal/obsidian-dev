### Recapitulando: _Constructor vs Factory Function_

Antes de entrarmos em conceitos de classes, vale a pena frisar o que são `*constructor functions*` e o que são `*factory functions*` e a diferença entre elas. Vamos ao exemplo:

```jsx
// constructor function
function Pessoa(n, i){
    // propriedades
    this.nome = n
    this.idade = i

    // métodos
    this.mostraNome = ()=>{
        return `Meu nome é ${this.nome}
				e tenho ${this.idade} anos.`
    }
}

// instanciação de um objeto do tipo pessoa
const eu = new Pessoa('itallo', 15)
const ela = new Pessoa('vitoria', 18)
```

```jsx
// factory function
function criaPessoa(n, i){
		
		// retornando um objeto
    return  {
        // propriedades
        nome: n,
        idade: i,

        // métodos
        mostraNome(){
            return `Meu nome é ${this.nome} e tenho ${this.idade} anos.`
        }
    }
}

const eu = criaPessoa('itallo', 15)
const ela = criaPessoa('vitoria', 18)
```

Enquanto as Factory Functions são funções que retornam um objeto literal com os valores passados como parâmetro, as `*Constructors functions*` são funções que servem de base para que um objeto seja instanciado. No caso do exemplo, temos uma `*constructor function*` _Pessoa_ que associa os valores passados ao objeto que será criado a partir dessa função.

Ao instanciar _Pessoa_, o objeto criado é do tipo _Pessoa_, e dispõe todos os métodos e propriedades definidos anteriormente.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1de4b6ec-8e66-4084-a584-fef297aacf72/Untitled.png)

### Classes: Introdução

Com o lançamento do ES6, foram introduzidas as classes e outras ferramentas que fazem que o `*javascript*` tenha um caráter menos funcional e mais voltado a POO. Uma classe é basicamente um molde que expõe a forma com que determinado objeto vai se comportar. É um `*Blueprint*` de determinado contexto.

> “_**Blueprint é mapeamento das atividades internas de uma organização e/ou dos processos de um sistema para que um serviço possa funcionar adequadamente”**_

Ou seja, as classes irão definir como o objeto quando for instanciado irá se comportar: o que os métodos irão fazer e como serão implementadas suas propriedades.

### Instanciação

Se por um lado as classes são um molde indicando seu comportamento, um objeto é o resultado final do produto desse molde com os valores preenchidos. Ou seja: o ato de instanciação é o processo de transformar o modelo abstrato em um produto concreto.

### Classes: Estrutura

```jsx
// declaracão da classe
class Pessoa {

    constructor(nome, idade) {
			// declaracao das propriedades
        this.nome = nome
        this.idade = idade
    }

		// declaracao de métodos
    apresentar(){
        return `Meu nome é ${this.nome} e tenho ${this.idade} anos.`
    }
    
}

// instanciacão da classe
const eu = new Pessoa('itallo', 15)
```

Note que agora usamos a palavra reservada `*Class*` seguido do nome em maiúscula. Dentro da classe temos a palavra reservada `*constructor*` que é uma funcão responsável por vincular os valores que vem externo para suas devidas variáveis.

Repare que o uso de `*Classes*` e o uso de `*Constructor Functions*` são muito parecidos, com a diferença de poucas palavras reservadas. O uso de `*Classes*` se assemelha mais ao paradigma de POO e faz com que possamos utilizar outras ferramentas que veremos já já.

### Classes: Disclaimer

Como dito anteriormente, classes foram introduzidas com o _**ECMAScript 2015**_ (ou famosos _**ES6**_) porém carecia de muitas funcionalidades vistas em outras linguagens baseadas em POO, como JAVA, por exemplo.

Métodos e propriedades estáticos, privados, possibilidade de iniciar propriedades fora do construtor, todas essas coisas foram adicionadas só em atualizações que vieram depois de 2019. A própria possibilidade de lidar com elementos privados para que eles não fossem utilizados fora das classes só foi ser implementada com o uso de `*#*` em 2019 e a declaração de modificadores `*private*` e `*readonly*` apenas no fim/comeco 2021/22!

Então todos esses conceitos que veremos a partir de agora, apesar de serem muito utilizados em C#, JAVA e outras linguagens que possuem o paradigma de POO mais desenvolvido, são relativamente recentes dentro do JS e não contam - apesar de já terem uma excelente cobertura - de suporte 100% de todas as versões dos navegadores. Dito isso, vamos continuar.

### Classes: _Static Methods - introdução_

Uma das palavras reservadas utilizadas no contexto de classes é a palavra reservada `*static*`. Com ela podemos acessar métodos de dentro de uma classe sem ter que instanciar um objeto. Neste caso o método está vinculado ao construtor da classe, e só podemos acessar através dele.

```jsx
// atualizando nossa classe
**class Pessoa {**

    constructor(nome, idade) {
        this.nome = nome
        this.idade = idade
    }

    apresentar(){
        return `Meu nome é ${this.nome} e tenho ${this.idade} anos.`
    }
		
		static reclamar(){
		    return `nossa ta frio demais`
		}
    
}

const eu = new Pessoa('itallo', 15)
```

Agora o método `*reclamar*` poderá ser acessado através de `*Pessoa.reclamar()*` e não mais através de um objeto instanciado. Um paralelo que podemos fazer é o `*.filter*` e o `*Array.from()*` dos vetores.

Enquanto o `*filter*` você acessa quando o vetor está pronto para ser manipulado, o `*.from*` é acessado apenas pelo construtor do objeto de vetores, e serve para criar outro vetor a partir de um `*array-like.`* como uma `*nodelist*` por exemplo.

### Classes: _Static methods -_ cenário

Um dos cenários interessantes para o uso de métodos estáticos é quando um determinado comportamento se torna padrão e para que nós não precisemos repetir ele várias vezes, criamos um template. Por exemplo:

```jsx
class Pessoa {
    constructor(nome, idade) {
        this.nome = nome
        this.idade = idade
    }

    apresentar(){
        return `Meu nome é ${this.nome} e tenho ${this.idade} anos.`
    }
    
    static criaAdolescente(nome){
        const idade = Math.round(Math.random() * (18 - 12) + 12)
        return new Pessoa(nome, idade) 
    }
}

											// a classe vai automatizar um processo 
											// e nos devolver um objeto pronto!
const primoAleatorio = Pessoa.criaAdolescente('tiago')

```

Vamos supor que desejamos gerar uma Pessoa aleatória na faixa etária de adolescente - de 12 a 18 anos. Ao invés de ter que colocar manualmente uma idade e um nome, podemos ter um método responsável por automatizar esse processo, fazendo com que nós apenas tenhamos que escolher o nome.

Isso é muito interessante! Podemos ter um botão com x, w, y e z características, mudando apenas o conteúdo escrito por exemplo. Muitas possibilidades.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1cc6b12c-865d-40a1-b01e-413cfe969021/Untitled.png)

### Classes: Set

Vamos voltar com nossa classe à sua origem.

```jsx
// declaracão da classe
class Pessoa {

    constructor(nome, idade) {
        this.nome = nome
        this.idade = idade
    }

    apresentar(){
        return `Meu nome é ${this.nome} e tenho ${this.idade} anos.`
    }
}

// instanciacão da classe
const eu = new Pessoa('itallo', 15)
```

Muito comum antes de vincularemos um valor à alguma variável é verificar se seus dados foram recebidos de maneira correta. Então poderíamos fazer um método responsável por verificar se o nome - neste caso - possui menos de 2 letras, depois tirar os espaços e colocar tudo em minúscula. Depois vincula à propriedade responsável. Resumindo, preparar o dado `*nome*` com a formatação correta.

```jsx
class Pessoa {

    constructor(nome, idade) {
			// passando o valor direto para o método
        this.verificaNome(nome)
        this.idade = idade
    }

    apresenta(){
        return `Meu nome é ${this.nome} e tenho ${this.idade} anos.`
    }

		// o método faz a verificacão e depois vincula 
		// à propriedade equivalente
    verificaNome(n){
        if(n.length >= 3){
            this.nome = n.trim.toLowerCase() // itallo
            return true
        }
        else{
            return false
        }
    }
}

// passando o nome zoado
const eu = new Pessoa(' itaLLO ', 15)
```

Conseguimos criar uma etapa na criação da nossa propriedade nome que verifica se os dados recebidos estão corretos. Geralmente, ao fazer essa definição usamos o método `*set*` . Podemos fazer de duas formas: ou criamos uma funcão `*setNome*` ou usamos o set do `*javascript*`. Diferente de outras linguagens, o `*set*`/`*get*` do _**JS**_ permite que usemos o método como uma propriedade.

```jsx
class Pessoa {

    constructor(nome, idade) {
        this.setNome(nome)
        this.idade = idade
    }

    apresenta(){
        return `Meu nome é ${this.nome} e tenho ${this.idade} anos.`
    }
		
		// método set comum
    setNome(n){
        if(n.length >= 3){
            this.nome = n.trim().toLowerCase()
            return true
        }
        else{
            return false
        }
    }
}

const eu = new Pessoa('itallo', 15)
console.log(eu.nome)
```

```jsx
class Pessoa {

    constructor(nome, idade) {
				// vinculando como se fosse propriedade
        this.Nome = nome
        this.idade = idade
    }

    apresenta(){
        return `Meu nome é ${this.nome} e tenho ${this.idade} anos.`
    }
		
		// ao colocar com espaco este método 
		// vira um método set de JS, sendo
		// utilizado como se fosse uma propriedade
    set Nome(n){
        if(n.length >= 3){
            this.nome = n.trim().toLowerCase()
            return true
        }
        else{
            return false
        }
    }
}

const eu = new Pessoa('itallo', 15)
```

### Classes: Get

Da mesma forma podemos utilizar um método get que é responsável por buscar e retornar determinado dado de dentro da nossa classe.

```jsx
class Pessoa {

    constructor(nome, idade) {
        this.setNome(nome)
        this.idade = idade
    }

    apresenta(){
        return `Meu nome é ${this.nome} e tenho ${this.idade} anos.`
    }
		
    setNome(n){
        if(n.length >= 3){
            this.nome = n.trim().toLowerCase()
            return true
        }
        else{
            return false
        }
    }

		// método set comum
		getNome(){
		        if(this.nome){
		            return this.nome
		        }
		        else{
		            return 'Propriedade não setada. Por favor, adicione um nome.'
		        }
		    }
}

const eu = new Pessoa('itallo', 15)
```

```jsx
class Pessoa {

    constructor(nome, idade) {
        this.setNome(nome)
        this.idade = idade
    }

    apresenta(){
        return `Meu nome é ${this.nome} e tenho ${this.idade} anos.`
    }
		
		
    set Nome(n){
        if(n.length >= 3){
            this.nome = n.trim().toLowerCase()
            return true
        }
        else{
            return false
        }
    }

		// ao colocar com espaco este método 
		// vira um método set de JS, sendo
		// utilizado como se fosse uma propriedade
		get Nome(){
		        if(this.nome){
		            return this.nome
		        }
		        else{
		            return 'Propriedade não setada. Por favor, adicione um nome.'
		        }
		    }
}

const eu = new Pessoa('itallo', 15)
```

### O problema..

Agora nossa classe `*Pessoa*` possui um construtor que recebe `*nome*` e `*idade*`, e o nome possui um método `*set*` que é responsável por filtrar o dado recebido direto no construtor e nos informar caso esse procedimento tenha sido executado com sucesso ou não. Para que possamos mostrar a propriedade fora da classe nós então criamos um método `*get*` que nos mostra o nome caso exista e caso não exista nos informe com uma mensagem para que possamos vincular.

Essa seria a forma correta de utilizar a classe criada, porém o grande problema é que todas as propriedades e métodos criados com a estrutura de classes são _**públicos, por padrão.**_ Isso significa que podemos ignorar toda a verificação e o processo de informação do nosso `*get*` e do nosso `*set*` de uma forma muito simples:

```jsx
// instanciando uma nova classe com nome correto
const eu = new Pessoa('itallo', 15)
// utilizando do método get para devolver o nome
console.log(eu.Nome) // itallo

// porém, como a propriedade é pública, eu consigo 
// sua manipulacão fora do ambiente de classes, burlando
// toda a lógica de cima
eu.nome = 'rá'
console.log(eu.Nome) // output: rá
```

### Classes: Privando Métodos e Propriedades

Até a implementação de elementos privados, usava-se _underscore_ antes do no nome para indicar que teoricamente aquela variável não deveria ser utilizada fora do escopo de classe - `*_nome*` , no nosso caso. Embora servisse de aviso para outros desenvolvedores, nada fazia para impedir de fato com que os elementos fossem invocados fora da classe.

Logo depois - 2019/2020 - foi implementado o uso de `*#*` no começo do nome da variável para indicar ao `*javascript*` que seu acesso deveria ser limitado para apenas dentro da classe. Seu uso se dá na declaração que deve ocorrer no topo do código.

Diferentemente de outras linguagens, `*javascript*` puro não nos fornece a possibilidade de trabalhar com modificadores como `*private*`, `*public*` e `*protected*` como já é costume de outras linguagens.

```jsx
class Pessoa {
		// declarando variável nome
		// indicando que ela será privada
    #nome

    constructor(nome, idade) {
        this.Nome = nome
        this.idade = idade
    }

    apresenta(){
        return `Meu nome é ${this.#nome} e tenho ${this.idade} anos.`
    }
		
		// setando
    set Nome(n){
        if(n.length >= 3){
            this.#nome = n.trim().toLowerCase()
            return true
        }
        else{
            return false
        }
    }
		
		// retornando
    get Nome(){
        if(this.#nome){
            return this.#nome
        }
        else{
            return 'Propriedade não setada. Por favor, adicione um nome.'
        }
    }
}
```

```jsx
const eu = new Pessoa('itallo', 15)
console.log(eu.Nome) // itallo

eu.#nome = 'rá' 
console.log(eu.Nome) // erro
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/924eccd5-9514-4d64-9d2d-34332762118f/Untitled.png)

### Classes: Herança

Muito comum termos classes que herdam elementos de uma outra classe e ao mesmo tempo adicionam elementos específicos relacionados ao seu contexto. Por exemplo, vamos criar uma classe `*Trabalhador*`. Um trabalhador definitivamente deve saber se apresentar, ter um nome e uma idade, além de que um trabalhador é uma pessoa.

Levando isso em consideração, a classe trabalhador deve herdar esses métodos e propriedades da classe pessoa, e apenas adicionar seus elementos próprios. A classe `*Trabalhador*` é uma _**extensão**_ da classe `*Pessoa` ,* assim como uma eventual classe `*Patrão*`, ou `*Estudante*` seria.

```jsx

// Estrutura da classe Pessoa
class Pessoa {
    constructor(nome, idade) {
        this.Nome = nome
        this.idade = idade
    }

    apresenta(){
        return `Meu nome é ${this.nome} e tenho ${this.idade} anos.`
    }

    // setando
    set Nome(n){
        if(n.length >= 3){
            this.nome = n.trim().toLowerCase()
            return true
        }
        else{
            return false
        }
    }

    // retornando
    get Nome(){
        if(this.nome){
            return this.nome
        }
        else{
            return 'Propriedade não setada. Por favor, adicione um nome.'
        }
    }
}
```

```jsx
// classe trabalhador extende (ou seja, herda) a classe Pessoa
class Trabalhador extends Pessoa{

    mostraTrabalho(trabalho){
        return `Eu sou o ${this.nome} e trabalho como ${trabalho}.`
    }
}
```

Quando dizemos que uma classe herda elementos de outra, isso quer dizer que tudo que estava disponível na classe pai se transporta e se diz disponível na classe filha - retirando, obviamente, elementos privados - `*#elemento*` que comentamos acima.

Isso quer dizer que o construtor é o mesmo, os métodos `*get*`, `*set*`, o `*apresentar*`, tudo se torna disponível nessa classe `*Trabalhor*`. E se quisermos modificar? É só rescrever o método/propriedade que ao acioná-lo, o JS vai procurar primeiro por ele na classe atual e apenas caso não o ache irá para classe pai.

Para adicionar novos elementos ao construtor fazemos da seguinte forma:

```jsx
class Trabalhador extends Pessoa{
    
    constructor(nome, idade, trabalho) {
				// palavra reservada super
        super(nome, idade);
        this.trabalho = trabalho 
    }
    mostraTrabalho(){
        return `Eu sou o ${this.nome} e trabalho como ${this.trabalho}.`
    }
}
```

A palavra reservada `*super()*` serve para que acessemos diretamente na classe filha um elemento da classe pai. Neste caso, criamos um construtor que vai receber `*nome*`, `*idade*` - como já estava recebendo, porém antes o construtor estava implícito - e agora irá receber uma variável adicional que indica o trabalho exercido.

Neste caso estamos passando `*nome*` e `*idade*` utilizando como base o construtor do pai, e adicionando trabalho como já estávamos fazendo.

Linguagem: [[Javascript]]