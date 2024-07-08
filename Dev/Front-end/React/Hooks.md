### O que são hooks?

_Hooks_ são funções fornecidas pelo React que possuem algumas regras específicas. As regras gerais é que eles começam com a palavra `*use*` na frente de seu nome e devem ser declarados no topo de um componente. Eles não podem ser usados em outras funções, só podem ser usados dentro de um componente, acima de todo o código. Ao longo do nosso estudo veremos outras características específicas de cada componente.

O React nos disponibiliza 15 _hooks_, mas de todos os mais comuns são:

- _useState_
- _useRef_
- _useCallback_
- _useMemo_
- _useEffect_
- _useReducer_
- _useContext_

### _useState_

O _hook_ mais comum e básico que podemos utilizar é o useState. Com ele, podemos criar uma variável reativa, que ao mudar re-renderiza o componente com seu valor atualizado. Ao usar a grande maioria dos _hooks_, desestruturaremos uma propriedade e um método.

No caso do useState, iremos desestruturar o valor que queremos acessar e atualizar, e uma função que atualiza esse valor. Por conveniência, essa função sempre possui “set” na frente do valor, para que fique mais fácil de entender o código. Veremos:

```jsx
import React from 'react';
function App() {
    const [linguagem, setLinguagem] = React.useState('')

    return (
        <>
            <p>Aprendendo: {linguagem}</p>
            <button onClick={()=> setLinguagem('React')}>Incrementar</button>
        </>
    )
}

export default App
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/92d90655-2616-49e9-91c8-aa0442ce7d33/Untitled.png)

Note que temos uma variável linguagem que armazena primeiramente um valor ‘’ e uma função `*setLinguagem*`. No navegador podemos ver que o valor inicial está sendo mostrado - que no caso é uma string sem nada - e um botão. Ao clicar no botão, passamos na função `*setLinguagem*` o valor “React”, fazendo com que atualize o valor da variável originária do useState fazendo com que nosso aplicativo re-renderize com o novo valor.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2c302d81-1896-4ce6-8dcd-f117204e0d87/Untitled.png)

Bem simples! Agora vamos fazer um pouco diferente. Vamos supor que você quer atualizar um valor anterior somando +1. A função `*setter*` devolvida pelo _hook_ aceita a estrutura de função ao modificar o seu valor. Com ela você tem acesso ao valor anterior para fazer o que quiser com ele.

```jsx
import React from 'react';
function App() {
    const [contador, setContador] = React.useState(0)

    return (
        <>
            <p>Contador: {contador}</p>
            <button onClick={
								()=> setContador((valorAnterior)=> valorAnterior + 1)
						}>Incrementar</button>
        </>
    )
}

export default App
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4745c9d2-84c8-4cdf-bb36-d5faaf8dbe46/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0040d2a5-c22d-43d5-9373-0aced5ab636b/Untitled.png)

### _useEffect_

O _hook_ useEffect tem o intuito de aplicar “efeitos colaterais” no componente. Por exemplo, a o atualizar um estado, realizar determinada tarefa, ou ao montar um componente disparar uma função ou realizar algo com aquele estado que foi modificado.

```jsx
import React from 'react';
function App() {
    const [cor, setCor] = React.useState('')
    
		// toda vez que o a variável cor for mudada, ela vai trocar
		// a cor do H1 para a cor nova
    React.useEffect(()=>{
        document.querySelector('h1').style.color = `${cor}`
    },[cor])

    return (
        <>
            <h1>Modifique a cor!</h1>
            <button onClick={()=>{setCor('blue')}}>Mudar!</button>
        </>
    )
}

export default App
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f8ac0968-c697-418b-a3ff-6ab0cd6011d9/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/59b5cc3c-084d-4c05-9928-66d1df4a0266/Untitled.png)

Note que a estrutura do `*useEffect*` é: uma função para realizar determinada tarefa e um vetor de dependência. Esse vetor é a variável ou as variáveis que o `*useEffect*` terá que acompanhar para disparar a função passada.

```jsx
    // estrutura
		React.useEffect( funcao, [dependencia] )

		// estrutura aplicada
    React.useEffect(()=>{
        document.querySelector('h1').style.color = `${cor}`
    },[cor])
```

Caso passarmos um vetor de dependência vazio, o useEffect disparará toda vez que o componente for construído. Isso é útil para quando quisermos fazer requisições de um servidor toda vez que o componente for montado.

### _useRef_

Este _hook_ trabalha com referências, sendo muito útil para capturar determinados elementos do DOM. Vamos atualizar a função de anterior. Para isso, iremos utilizar um atributo no elemento desejado chamado `*ref`.* Criaremos a variável “cabecalho” chamando a função de referencia. Depois é só utilizar o conteúdo da variável cabecalho com a propriedade `*.current*`.

Veja abaixo:

```jsx
import React from 'react';
function App() {
    const [cor, setCor] = React.useState('')
		// utilizando useRef
    const cabecalho = React.useRef()

    React.useEffect(()=>{
				// utilizando a referencia capturada
        cabecalho.current.style.color = `${cor}`
    },[cor])

    return (
        <>
						// capturando a ref
            <h1 ref={cabecalho}>Modifique a cor!</h1>
            <button onClick={()=>{setCor('blue')}}>Incrementar</button>
        </>
    )
}

export default App
```

## useCallback

`*todo*`

## useMemo

`*todo*`

## useReducer

`*todo*`

## customHooks

`*todo*`

Linguagem: [[Front-end/React/React]]