### Promises

Um código pode ser executado de duas formas. De forma síncrona e de forma assíncrona. A forma síncrona é por bloco: o programa é executado linha por linha, e quando se tem um bloco de código, o restante da execução só ocorre quando aquele bloco de código termina de executar. Já a execução assíncrona faz com que um determinado trecho de código ocorra de forma independente para que não trave a execução do código. Vamos aos exemplos:

Vamos supor que você tem uma função que pega determinada informação de alguma base de dados, um servidor. Geralmente essa requisição demora alguns instantes: seja por conta da internet, do servidor, do download, ou quaisquer motivos que seja. Para simular essa demora, vamos usar uma função chamado `*setTimout*`. Ele recebe uma função e um parâmetro da quantidade de segundos que aquele código deve esperar para ser executado.

> [!Leitura Adicional]
> [JS Async vs Sync](https://medium.com/@yfaria/fundamentos-backend-2-sync-vs-async-43ba423bb9b8#:~:text=Tarefa%20S%C3%ADncrona%3A%20%C3%A9%20uma%20tarefa,tempo%20que%20outra%20tarefa%20ocorre.)

A função abaixo ela retorna uma `*string*` dizendo que a informação está capturada depois de 2 segundos. Chamamos essa função logo abaixo mostrando no console. O problema é que o retorno dela ocorre muito depois de quando ela é solicitada. Isso faz com que ela tenha valor indefinido assim que é chamada. Seu valor só é atualizado depois.

```jsx
function getInfo(){
    setTimeout(()=>{
        return 'informação capturada!'
    }, 2000)
}

console.log(getInfo()) // undefined
```

E não é isso que nós queremos. O objetivo é mostrar a informação só depois dela ser capturada. Vamos ver as opções que temos para resolver esse problema.

Podemos colocar o console dentro da função `*getInfo*`:

```jsx
function getInfo(){
    setTimeout(()=>{
        info = 'informação capturada!'
        console.log(info) 
    }, 2000)
}

getInfo()
```

Só que isso é bem problemático: agora uma função que deveria apenas pegar as informações, está pegando **e** escrevendo na tela. E caso queiramos fazer outras ações, teremos que fazer dentro dela. E uma função que faz várias ações diferentes geralmente não é uma boa ideia.

[Aqui você pode ver o porquê.](https://www.notion.so/Fun-es-b9ab264afbe34f86ac2295b5094c56da?pvs=21)

Adicionando a função `*mostraInfo*`dentro da função `*getInfo*` é uma maneira um pouco mais organizada. Fica mais fácil de fazer a manutenção do código, mas ainda não está bom o suficiente já que fazendo isso, todas as vezes que pegarmos a informação, teremos que mostrar na tela, as duas funções estão **sempre** conectadas.

```jsx
function getInfo(){
    setTimeout(()=>{
        mostraInfo('informação capturada!')
    }, 2000)
}

function mostraInfo(msg){
    console.log(msg)
}

getInfo()
```

Uma forma de corrigir esse problema é usar uma função de **`*callback*`**, fazendo com que esse `*callback*` dependa de acordo com o que queremos fazer. Podemos ou verificar se a msg é igual a `*null*`, ou mostrar no console dependendo da função parâmetro passada.

```jsx
function getInfo(callback){
    setTimeout(()=>{
        callback('informação capturada!')
    }, 2000)
}

function mostraInfo(msg){
    console.log(msg)
}

function verificaInfo(msg){
    if(msg == null){
        console.log('Não foi possível capturar a informação.')
    }
}

getInfo(verificaInfo) // nenhum output
getInfo(mostraInfo) // informação capturada!
```

Com a lógica das `*Promises*` podemos levar esse exemplo a um novo nível. Uma `*Promise*` nada mais é do que um objeto que recebe dois parâmetros, um `*resolve*` e um `*reject*`.

- Se a informação que desejamos for capturada com sucesso, retornaremos com o `*resolve.*`
- Enquanto não temos resposta, o status fica como `*pending.*`
- Caso no meio do processo tenha algum erro, retornaremos com o `*reject.*`

```jsx
function getInfo(){
	
		// retornando um objeto promise 
		// que recebe uma função com resolve e reject
    return new Promise(function(resolve, reject){
        setTimeout( ()=>{
            if(true)
            {
                resolve(true)
            }else{
                reject(false)
            }
        }, 2000)
})}

```

Para que possamos realizar alguma ação com os dados retornados podemos utilizar o método `*then`* passando as funções relativas caso a `*Promise*` tenha retornado com sucesso ou não nosso objeto. Para lidar com isso temos duas formas:

```jsx
function onError(){
    console.log('Erro ao capturar')
}
function onSuccess(){
    console.log('informação capturada!')
}

// forma 1: passando o resolve e o reject
// como parâmetros do then
getInfo().then(onSuccess, onError)
```

Essa é a estrutura básica das `*promises`.* Agora, imagine que você tem mais de uma função aguardando esse resultado. Você naturalmente terá mais de um `*then` :*

```jsx
function mostraDelay(){
    console.log('a informação demorou 2s')
}

getInfo()
    .then(onSuccess, onError)
    .then(mostraDelay)
```

O problema dessa estrutura é que se a informação não vier, será executado o `*reject`* passado dentro do primeiro `*then*`, e depois independe de ter dado errado o segundo `*then`* vai ser executado. Isso pode gerar alguns problemas. Para resolver isso, podemos usar o método `*catch*`

```jsx
function mostraDelay(){
    console.log('a informação demorou 2s')
}

getInfo()
    .then(onSuccess)
    .then(mostraDelay) // caso dê erro esse then não será executado
		.catch(onError)
```

O método `*catch*` lida com os erros e faz com que caso haja algum, tenha uma ruptura na sequência do código onde ele ocorreu. Ou seja, se o resultado da `*promise`* for um erro, ele pulará todos os `*then*` - que por sua vez teriam um `*resolve*` - associados aquela `*promise.`* Não dá para “resolver” o que não está de fato resolvido, não é mesmo?

Para finalizar temos o método `*finaly`* que roda terminada função depois de tudo que deveria já ter acontecido. Mesmo que o resultado seja um resolve ou um `*reject*`, o `*finaly*` vai ser chamado e rodado. Ele serve para caso queiramos no final de todas as tarefas remover alguns eventos, limpar algumas variáveis ou fazer uma ação no final de tudo.

### API: O que é?

Para que possamos ver as `*promises`* aplicadas em um exemplo real, precisamos antes entender o que é uma API.

> “_API é um acrônimo para Application Programming Interface, ou Interface de Programação de Aplicação, em português. Trata-se de um conjunto de rotinas e padrões que facilitam a comunicação e troca de informações entre sistemas.”_

[O que é uma API? [Guia para iniciantes] – Tecnoblog](https://tecnoblog.net/responde/o-que-e-uma-api-guia-para-iniciantes/)

As APIs servem basicamente para que dois sistemas distintos se conectem e troquem informações. Você poderia usar a API do google para usar funcionalidades fornecidas por ele para mapas, ou conectar a um servidor de previsão do tempo que retorna a previsão da região do usuário, ou quem sabe conectar a um servidor que hospeda produtos e suas informações para que possamos mostrá-los em nosso site.

### RestFul API

////

### Fetch

O `*fetch*`é um método capaz de se conectar a um determinado servidor e capturar dados. O problema é que essa ação pode demorar alguns momentos, gerando erro no fluxo de nossa aplicação. Algo bem parecido com o problema que tivemos anteriormente com o `*setTimout`.*

O `*fetch*`trabalha diretamente com o uso de `*Promises*`, criando e devolvendo uma em sua execução, por conta disso é fundamental o entendimento de como elas funcionam.


Linguagem:  [[Javascript]]