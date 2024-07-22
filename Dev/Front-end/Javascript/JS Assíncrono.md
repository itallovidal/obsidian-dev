Palavras Chave: [[Javascript]]
### Diferenças entre Código Assíncrono e Código Síncrono

- Código síncrono é aquele que começa no topo do arquivo e vai executando linha por linha até chegar ao fim, em ordem. Cada linha de código aguarda a anterior para ser executada. 
- No código assíncrono, a execução acontece linha a linha até que se chegue à algum bloco de código assíncrono, e neste momento, aquele bloco de código é executado ao mesmo tempo que o restante do código síncrono. Isso trechos assíncronos dependem de processos que possuem algum tipo de delay, uma demora onde poderia travar o fluxo da aplicação.

### Exemplo

Vamos ver um exemplo simples de um código síncrono: ele executa linha a linha, sendo assim, nosso output é bem direto.
```typescript
let a = 1  
let b = 2  
  
console.log('Síncrono')  
console.log(a)  
console.log(b)
```
![[Pasted image 20240722170758.png]]
Podemos classificar a maioria de blocos de código assíncronos como sendo:
- Promises 
- Browser API/Wer API: funções como setTimout e event handlers (click, scroll, mouseOver e etc)

Vamos começar de forma simples, adicionando um setTimout. 
```js
let a = 1  
let b = 2  
  
setTimeout(()=>{  
    console.log('Assíncrono!')  
}, 100)  
  
console.log('Síncrono')  
console.log(a)  
console.log(b)
```
![[Pasted image 20240722170849.png]]
Percebe-se que mesmo com a função setTimout antes dos console.log, como ela possui um delay de 100ms, o print de sua função ocorre apenas depois. 

### Callbacks, Requisições HTTP e Event Listeners

Por exemplo, vamos supor que queremos fazer um fetch em alguma API. 
- Queremos mostrar um loading
- Fazer o fetch para pegar um conselho em uma API de conselhos
- Pegar o resultado
- E mostrar na tela

```js
let advice = "Loading"  
console.log(advice)  
advice = fetch('https://api.adviceslip.com/advice')  
console.log(advice)
```

O problema do código acima é que o FetchAPI - função built-in do JS para fazer requisições HTTP - é assíncrona,  ou seja, mesmo dando console.log **depois** da função, ainda não temos o resultado no tempo de execução do código. Cenário parecido com o primeiro exemplo.
### Callbacks

Como podemos ver aqui,  [[Funções]] de callbacks são funções que são passadas como parâmetro para outras funções, e nesse cenário, elas podem nos ajudar a manter uma ordem desejada no código. Vamos refatorar o código acima para utilizar callbacks.

```js
function fetchAdvice(){  
    return fetch('https://api.adviceslip.com/advice')  
}  
  
function transformBody(response){  
    return response.json()  
}  
  
function showAdvice(adv, p){  
    const advice = adv.slip.advice  
    p.innerHTML = advice  
}  
const button = document.querySelector('#button')  
  
button.addEventListener('click', ()=>{  
    const p = document.querySelector('#advice')  
    p.innerHTML = "Loading..."  
    fetchAdvice()  
        .then((response)=>{  
            transformBody(response)  
                .then((body)=>{  
                    showAdvice(body, p)  
            })  
        })  
})
```

Como podemos ver, ao longo do código uma funcão vai chamando a outra, temos primeiro a função de callback evento do clique do botão, depois temos o callback da resposta da api, depois temos o callback da transformação do body desta resposta e depois finalmente passamos o callback para mostrar o conteúdo na tela.

Como podemos ver, embora utilizar funções de callback faça com que o nosso código tenha a ordem desejada, o código não fica intuitivo e acaba ficando difícil de dar manutenção por ter muito níveis aninhados - embora estejamos fazendo algo extremamente simples.

O aninhamento profundo em alguns casos até possui nome: **callback hell**.
![[Pasted image 20240722180947.png]]

# Promises

Se repararmos no código acima, vemos muito o uso de uma função chamada **then**. Isso porque códigos assíncronos, principalmente requisições HTTPs, retornam uma Promise. 

Toda vez que você faz uma requisição HTTP, uma promessa é realizada, obtendo  três estados:
- Pending - Quando a promessa ainda não obteve retorno.
- Fullfilled - Quando o retorno da promessa é um valor.
- Rejected - Quando o resultado é um erro.

Ou seja, a resposta pode acontecer, ou pode haver algum erro no processo.

Vamos voltar ao exemplo básico utilizando setTimout:
Abaixo temos uma criação manual de uma Promise. Ela recebe um função de callback com dois parâmetros, **Resolve** e **Reject**. Dentro dela temos um setTimout onde soma o valor de A e B.

- Caso o valor seja menor que 5, tudo certo! Vamos resolver a promessa. 
- Caso o valor seja maior ou igual a 5, não pode, vamos rejeitar a promessa.

Abaixo temos duas funcões, uma chamada **onFulfilled**, onde vai lidar com caso que a promessa seja resolvida, e uma chamada **onError**, onde lidará com promessas que teve algum tipo de erro.

```js
let a = 1  
let b = 4  
  
const result = new Promise((resolve, reject) => {  
    setTimeout(()=>{  
        if(a + b < 5){  
            resolve(a + b)  
        }  
        else{  
            reject("Algo deu errado")  
        }  
    }, 100)  
})  
  
function onFulfilled(result) {  
    console.log("Tudo certo! O resultado foi:")  
    console.log(result)  
}  
  
function onError(error){  
    console.log("Opsie!")  
    console.log(error)  
}  
```

Estamos guardando essa promessa em uma variável chamada **result**. Uma das formas de lidar com Promessas foi abordado acima, com callbacks. Toda promessa possui um método **then**, responsável por passar o resultado da promessa assim que ela tiver algum tipo de resultado, seja ele qual for. 

Esse método recebe dois parâmetros, **onFulfilled** e  **onError**, então podemos passar cada função criada para o respectivo lugar:
```js
result.then(onFulfilled, onError)
```

### Requisições HTTP

Voltando ao exemplo da API de conselhos, repare que além dos problemas do uso de callbacks, temos também um **then** aninhado com outro: ora, precisamos fazer o fetch, **então** transformar o body, para só **então** mostrar na tela o resultado.

```js
button.addEventListener('click', ()=>{  
    const p = document.querySelector('#advice')  
    p.innerHTML = "Loading..."  
    fetchAdvice()  
        .then((response)=>{  
            transformBody(response)  
                .then((body)=>{  
                    showAdvice(body, p)  
            })  
        })  
})
```

O que deixa o código ainda mais confuso. Poderíamos lidar com essas informações refatorando o código para que ao final de um **then**, ele retorne o resultado. 

```js
button.addEventListener('click', ()=>{  
    const p = document.querySelector('#advice')  
    p.innerHTML = "Loading.."  
  
    fetchAdvice()  
        .then((response)=>{  
            return response  
        })  
        .then((response)=>{  
            return transformBody(response)  
        })  
        .then((body)=>{  
            showAdvice(body, p)  
    })  
})
```

Isso faz com que não tenhamos mais thens aninhados, pois ao pegar a resposta de uma promessa concluída, retornamos para o then externo.  Isso faz com que nosso código fique mais legível e fácil de entender.

Além disso poderíamos adicionar um catch no fim dos thens, para caso algum dos processos darem errado.

```js
button.addEventListener('click', ()=>{  
    const p = document.querySelector('#advice')  
    p.innerHTML = "Loading.."  
  
    fetchAdvice()  
        .then((response)=>{  
            return response  
        })  
        .then((response)=>{  
            return transformBody(response)  
        })  
        .then((body)=>{  
            showAdvice(body, p)  
        }).catch(()=>{  
		    // neste caso, caso algum dos processos acima derem errado
		    // o parágrafo vai informar que não foi possível fazer
		    // a requisição. Tente escrever URL errado para testar.
            p.innerHTML = 'Não foi possível se conectar à api.'  
    })  
})
```

### Async & Await 

Com a atualização do JS ES6, foram introduzidas as funções async/await. São funções que visam facilitar a leitura e a manutenção do código com uma estrutura simples: você literalmente pede para determinada instrução no código ser lida e aguardada. Vejamos:

```js
async function handleClick(){  
    const p = document.querySelector('#advice')  
    p.innerHTML = "Loading...!"  
    
    try{  
        const response = await fetchAdvice()  
        const advice = await transformBody(response)  
        showAdvice(advice, p)  
    }catch(e){  
        p.innerHTML = e.message  
    }  
}  
  
button.addEventListener('click', ()=>{  
    handleClick()  
})
```

A função em sua assinatura deve possui **async** e em momentos assíncronos utilizamos a palavra reservada **await** para aguardar seu retorno. Sempre interessante envolver esses trechos de código com Try/Catches para tratativas de erros.

> [!Leitura Adicional]
> [JS Async vs Sync](https://medium.com/@yfaria/fundamentos-backend-2-sync-vs-async-43ba423bb9b8#:~:text=Tarefa%20S%C3%ADncrona%3A%20%C3%A9%20uma%20tarefa,tempo%20que%20outra%20tarefa%20ocorre.)
> [Callbacks](https://dev.to/rodcast/callbacks-understanding-javascript-api-requests-and-responses-in-the-data-fetching-lifecycle-41b9)



Linguagem:  [[Javascript]]