### Interfaces vs Types: trabalhando com objetos

Quando se trata de objetos, ocorre uma mudança sutil porém importante: o uso da palavra `*interface*`. Vamos supor que temos uma função que recebe um objeto com vários parâmetros:

```jsx
// veja que a assinatura da funcão ficou bem complexa, e gerou
// um código difícil de ler 
function listaUser(user:{
    nome: string;
    idade: number;
    plano: string;
}){
    console.log(`O usuário ${user.nome} possui ${user.idade} anos. 
		Está atualmente no plano ${user.plano}.`)
}

let user: {
    nome: string;
    idade: number;
    plano: string;
} = {
    nome: 'itallo',
    idade: 25,
    plano: 'Premium',
}

listaUser(user)
```

Para resolver isso podemos usar um tipo completamente criado por nós e passá-lo como parâmetro da função. Porém levando em consideração elementos de POO, ao invés de criarmos um tipo `*user`* iremos criar uma interface do tipo usuário.

Lembrando que uma interface é basicamente uma estrutura que define como um objeto será criado e manipulado. É uma abstração em relação a uma futura instância. Este tema é abordado com mais profundidade na seção de **classes no guia de JS.**

```jsx
// definimos que o listaUser irá receber um 
// valor com as características de *user*
function listaUser(user: User){
    console.log(`O usuário ${user.nome} possui ${user.idade} anos. 
    Está atualmente no plano ${user.plano}.`)
}

// a estrutura do objeto muda um pouco
interface User {
    nome: string;
    idade: number;
    plano: string;
}

// criamos um usuário novo com base na interface
const usuarioNovo: User = {
        nome: 'itallo',
        idade: 21,
        plano: 'Premium',
}

listaUser(usuarioNovo)
// O usuário itallo possui 21 anos. Está atualmente no plano Premium.
```

Importante dizer que geralmente `*types`* personalizados são colocados com letra maiúscula para que possamos identificar mais facilmente que aquele é um tipo nosso.

### Propriedade opcionais

Uma das possibilidades que temos ao criarmos interfaces são propriedades opcionais com o uso do operador `?` . Basta colocá-lo antes da propriedade que ao criar um elemento herdando a interface desejada ela será vista como opcional.

```jsx
interface Curso{
    nome: string;
    horas: number;
	// propriedade opcional
    gratuito?: boolean;
}

const meuCurso: Curso = {
    nome: 'teste',
    horas: 10,
}
```

### Classes em Typescript

O uso de classes em Typescript pega tudo o que vimos em JS e adiciona o uso de uma linguagem fortemente tipada, acrescenta a possibilidade de modificadores,

```jsx
class Pessoa{
		// possibilidade de usarmos modificadores
    protected nome: string = ''
    public idade: number

    constructor(n: string, i: number) {
        this.Nome = n
        this.idade = i
    }

    set Nome(n: string){
        if (n.length >= 3){
            this.nome = n
        }
        else{
            this.nome = ''
        }
    }

    get Nome(){
        return this.nome
    }

    apresentar() : string{
        return `Oi, eu sou o ${this.nome} e tenho ${this.idade} anos!`
    }
}
```

```jsx
class Trabalhador extends Pessoa{

    public trabalho: string
    constructor(n: string,i: number, t:string) {
        super(n,i);
        this.trabalho = t
    }

    mostraTrabalho(){
        return `Eu sou o ${this.nome} e trabalho com ${this.trabalho}`
    }
}

const eu = new Trabalhador('itallo', 20, 'Desenvolvimento')
console.log(eu.mostraTrabalho()) // Eu sou o itallo e trabalho com Desenvolvimento
```

### Classes: Modificadores - `*Public*`, `*Protected*` e `*Private*`

A diferença é muito simples: enquanto elementos `*public*` podem ser acessados diretamente fora da classe, elementos com `*protected*` e `*private*` ficam disponíveis apenas dentro de seu escopo. Elementos `*private*` só podem ser acessados na classe em que foram criados, não podendo ser herdados para classes filhas. Elementos com `*protected*` podem ser herdados, mas continuam não podendo ser acessados fora do escopo de classe.

### _Private_ e _Hash_ são a mesma coisa?

**Não!** `*Private*` é um modificador disponível apenas em `*typescript*`, que indica à ele que aquele elemento não pode ser acessado fora do escopo da classe, porém como não é uma função nativa existente no JS padrão, quando o typescript _transpila_ o código para JS puro, não possuímos nenhum erro.

Ou seja, em tempo de compilação temos o erro vindo do `*typescript*`, porém no tempo de execução não temos erro pois o resultado final do código não possui este modificador e o elemento é criado como público.

Com o uso de `Hash`, o elemento é de fato criado e manipulado como privado já que essa é uma _feature_ dentro do `*Javascript*` atual - por mais que seja recente. Lembrando que ao usar `*Hash*`, o elemento não poderá ser herdado, então o uso de um ou outro irá depender da necessidade.

### Desestruturação de objetos

Para desestruturar objetos temos que, como de costume, informar o tipo de elementos que estamos capturando. A estrutura é levemente diferente do costume:

```jsx
class Pessoa {
    nome: string
    constructor(n: string) {
        this.nome = n
    }
}

const eu = new Pessoa('itallo')

//                     interface contendo valores
function showPessoa({nome}:{nome: string}){
    console.log('>' + nome)
}

showPessoa(eu) // itallo
```

### Intersection

Nós podemos fazer com que uma função receba um dado que é uma interseção de duas outras interfaces ou dois outros tipos. Por exemplo:

```jsx
interface Pessoa {
    nome: string;
    idade: number;
}

interface Estudante{
    faculdade: string
    semestre: number
}
```

```jsx
//  data é do tipo Pessoa e ao mesmo tempo Estudante
//  contendo todos os seus métodos e propriedades combinados
function showData(data: Pessoa & Estudante){
    console.log(data.nome)
    console.log(data.idade)
    console.log(data.faculdade)
    console.log(data.semestre)
}
```

```jsx
const eu: Pessoa & Estudante = {
    nome: 'itallo',
    idade: 22,
    faculdade: 'UVA',
    semestre: 1
}

showData(eu)
```

Subtópico: [[Typescript]]