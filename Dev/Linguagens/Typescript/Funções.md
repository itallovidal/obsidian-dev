Nesta seção iremos abordar como funcionam as funções em TS e suas diferenças e adições em relação ao JS Padrão. Com a acréscimo de uma tripagem forte, nossas funções agora devem especificar qual tipo de variáveis elas esperam e podem opcionalmente explicitar seu retorno.

```jsx
//   							tipo       tipo    tipo retorno
function soma(a: number, b: number) : number {
    return a+b
}

// funcão deve obrigatoriamente receber dois valores do tipo number
// e retornar um valor do tipo number também
soma(10,20)
```

Isso é bom pois estrutura melhor definindo os tipos de dados que aquela função vai trabalhar e o que ela vai retornar. Uma função com o tipo definido de retorno precisa obrigatoriamente o retornar. Ou seja, caso nossa função de soma apenas fizesse o cálculo e não retornasse nada, o TS informaria um erro.

Enquanto os parâmetros precisam obrigatoriamente ter seus tipos, o retorno da função pode ser escrito opcionalmente. Isso acontece pois TS infere pelo contexto quais tipos aquela função está retornando.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e2b9225c-7ae2-459f-8c96-d9f7a4751a74/Untitled.png)

### Parâmetros opcionais

Podemos utilizar parâmetros opcionais com a notação de `?` **. Quando fazemos isso a funcão pode ou não receber determinado valor:

```jsx
function soma(a: number, b: number, c?: number )  {
    return a+ b + (c ? c : 0)
}

console.log(soma(10,20,10)) // 40 
console.log(soma(10,20))    // 30
```

### Utilizando Types e Interfaces

Conseguimos sem problemas nenhum utilizar tipos e interfaces para indicar os parâmetros recebidos na funcão, estruturando ela ainda melhor.

```jsx
// definindo uma variável do tipo cor
type Cor = 'azul' | 'preto'

// capturando o fundo da página
const fundo = document.querySelector('body') as HTMLBodyElement

// funcõa que pinta o fundo com a cor selecionada
//                                tipo cor
function pintaFundo(corSelecionada: Cor){
    fundo.style.background = corSelecionada
}

// aceita apenas preto e azul
pintaFundo('preto')

// erro: 
// Argument of type '"bege"' is not assignable to parameter of type 'Cor'
pintaFundo('bege') 

```

### Function _Overload_

Às vezes temos algumas funções que retornam um tipo de dado caso recebam um determinado valor, ou outro tipo de dado caso seja um valor de tipo diferente. Para deixar isso mais estruturado, TS nos permite fazer `*Overload*` de funções .

Ou seja, podemos indicar qual tipo de dado a função vai retornar caso ela receba valor do tipo X ou do tipo Y, acima da assinatura genérica da funcão. Abaixo temos uma funcão que recebe uma string ou vetor de `*strings*` e pode, dependendo do que receber, devolver uma string única ou esse vetor normalizado - neste caso apenas sem espaços desnecessários antes e depois da palavra.

```jsx
function normalize(str: string | string[]) : string | string[]{
    if(typeof str === "string"){
        return str.trim()
    }
    else{
        return str.map(value => value.trim())
    }
}
```

```jsx
let vetor = ['  thaissa', ' manu   ']
console.log(normalize('  itallo  ')) // 'itallo'
console.log(normalize(vetor)) ['thaissa', 'manu']
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/344bbce3-7381-4f41-bfac-12db0ed077eb/Untitled.png)

```jsx
// escrevemos a mesma funcão porém com o tipo explícito
function normalize(str: string[]): string[]
function normalize(str: string):string
function normalize(str: string | string[]) : string | string[]{
    if(typeof str === "string"){
        return str.trim()
    }
    else{
        return str.map(value => value.trim())
    }
}
```

Agora, caso passemos o mouse na função que recebe uma `*string*` única, sua assinatura dirá o que ela vai retornar: uma `*string*` única.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/897a9b04-0e9b-4190-99a7-47387708a4d1/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/76585d85-d205-427f-a21f-5e43b67d5e05/Untitled.png)

E caso passemos o mouse na funcão que recebe um vetor, também temos a informação que neste caso a função vai retornar um vetor de `*strings*`.

Subtópico: [[Typescript]]