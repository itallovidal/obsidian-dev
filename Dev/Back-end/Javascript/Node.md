## Preparando o Ambiente

Não precisamos de nada específico além do node para poder rodar nossos testes. Para criar um servidor podemos utilizar o seguinte código:

```jsx
// utilizando ES6 Modules
import http from 'node:http'

// utilizando o método createServer podemos criar o servidor
// passando uma funcão com resposta e requisição

// esse servidor vai devolver como resposta apenas hello world
const server = http.createServer((request, response)=>{
    return response.end('hello World')
})

// podemos "ouvir" o servidor passando o nome da porta
// que desejarmos 
server.listen(3333)
```

```jsx
// para iniciar o servidor devemos executar o código acima

// para fazer isso basta ir ao terminal e executar o arquivo com o node
node src/server.js 
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/5654b122-b275-42e4-b11f-1af481038aa8/Untitled.png)

Para não depender do navegador para ver nossas respostas, podemos executar o servidor diretamente do terminal com ferramentas como curl ou HTTPie. Pela sua facilidade de execução e configuração podemos utilizar no momento a segunda opcão.

HTTPie é **um cliente HTTP de linha de comando**. Esta ferramenta se destina a _testar e depurar APIs, servidores HTTP e serviços da web_. Ele vem com JSON, HTTPS, proxies e suporte para autenticação. É baseado em Python e lançado sob uma licença BSD.

Sua configuração é mais rápida utilizando `*chocolatey:`* podemos instalá-lo colocando o comando abaixo no powerShell:

```jsx
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('<https://community.chocolatey.org/install.ps1>'))
```

Com o chocolatey uma vez instalado, é simplesmente dizer para ele configurar o HTTTPie:

```jsx
choco install httpie
```

```jsx
choco upgrade httpie
```

Agora com o servidor aberto, podemos utilizar outro terminal para verificar sua resposta:

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/4d55e6c3-d5b9-4d68-807f-5d7ba65c89bf/Untitled.png)

## Fundamentos

Node é uma plataforma que nos possibilita utilizar javascript no backend. Isso nos abre portas para ter diversas aplicações que utilizam de javascript para serem executadas em um ambiente fora dos Browsers como Ionic, React Native

Depois da pasta aberta, o primeiro comando que usaremos para iniciar o ambiente de desenvolvimento é o `*npm init*` , com ele criaremos um arquivo `*json*` chamado de `*package`* com todas as informações do nosso projeto. Nele podemos adicionar informações importantes como descrição, scripts, autor, nome, versão e etc..

```json
{
  "name": "fundamentos-node",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \\"Error: no test specified\\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
```

<aside> 💡 OBS.: Para fazer com que esse arquivo seja criado de forma mais automatizada, sem termos que preencher na mão na hora da sua criação, podemos utilizar `*--y*` indicando que será aceito qualquer prompt mostrado na tela.

</aside>

## Require x Import

Algo muito comum hoje em dia é a modularização: método no qual se segmenta o código como um todo em pequenos módulos responsáveis por resolver determinada questão específica, fazendo com que seja mais fácil a manutenção, inteligibilidade e organização do projeto. Com o passar do tempo o método de como fazemos importações foram se modificando, transicionando do uso do `*Require*` para o uso do `*Import.*`

O `*Require*` utiliza do sistema `*CommonJS*`, popularizado por ser o sistema padrão do Node, enquanto o `*Import`* utiliza do sistema ES6 Modules introduzido na atualização ES6 do `*javascript*`. Ambos realizam a mesma tarefa: criar trechos de código e exportar para serem reutilizados evitando a repetição em diversos lugares. O fato do ES6 Modules serem carregados de forma Asssíncrona, garante uma performance melhor, pois os módulos são carregados de forma independente, e não um por um como na utilização do `*CommonJS*`

Como dito anteriormente, o sistema padrão do Node é o Commonjs, mas podemos trocá-lo facilmente configurando o nosso arquivo package.json.

```json
{
  "name": "fundamentos-node",
	
	// alterando o sistema de módulos default do node
	"type": "module",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \\"Error: no test specified\\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
```

## Scripts

Uma vez criado o servidor, ele executará aquelas instruções contidas nele no momento de sua execução, ou seja, se iniciarmos o servidor com `*Hello World*` e depois mudarmos para `*oi!*`, o resultado sempre será o mesmo `*Hello Word.*`

Mas podemos mudar esse comportamento adicionando o `*--watch*` na frente do arquivo a ser executado. Isso fará com que o servidor seja reiniciado toda vez que tiver alguma alteração.

```jsx
node --watch src/server.js
```

Porém esse é um comando extenso e que provavelmente se tornará cansativo de utilizar. Podemos então criar um script em nosso package.json para automatizar essa tarefa.

```json
{
  "name": "fundamentos-node",
	
	// alterando o sistema de módulos default do node
	"type": "module",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
		// criando o script de dev 
    "dev": "node --watch src/server.js"
  },
  "author": "",
  "license": "ISC"
}
```

```jsx
// agora só precisamos dizer ao gerenciador 
// de pacotes o que ele deve executar, que no caso
// é o script "dev"
npm run dev
```

## Instalação do Typescript

```jsx
// instalando typescript como uma dependência de desenvolvimento
npm install -D typescript 
```

Para que possamos desenvolver um código node com typescript, precisamos baixar o pacote de tipos, pois o TS não reconhece por padrão seus métodos e propriedades específicos.

```jsx
npm install -D @types/node 
```

```jsx
// criando arquivo de configuração do typescript
npx tsc --init
```

Com o typescript instalado podemos executar o código TS de duas formas.

- Compilando com `*npm tsc arquivo*` : que irá compilar o código em um arquivo js
- Ou podemos executar o comando `*npx tsx arquivo*` : ele irá executar o arquivo TS diretamente. Ajuda no desenvolvimento, mas para produção devemos compilar para o arquivo js.

```jsx
// criando arquivo de configuração do typescript
npm install -D tsx
```

```json
{
  "name": "fundamentos-node",
	
	// alterando o sistema de módulos default do node
	"type": "module",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
		// executando o arquivo sem compilar
    "dev": "tsx src/server.ts"
  },
  "author": "",
  "license": "ISC"
}
```

## Frameworks e Microframeworks

Geralmente, para que nosso código fique mais organizado, mais robusto e seja mais rápido de desenvolver nossa API, utilizamos de frameworks e/ou _microframeworks_ para ajudar nesse processo. Além disso a utilização de `typescript` **no contexto atual é imprescindível para desenvolvermos um código mais seguro e com mais qualidade.

Hoje os _microframeworks_ mais conhecidos e utilizados são o `*Fastify.js*` e o `*Express.js*`. São chamados de micro pois não possuem uma opinião muito forte quanto a organização de código e pastas. Ajudam na abstração de algumas configurações e adiantam algumas outras, mas não trazem uma mudança de paradigma tão intensa no desenvolvimento. São muito bons para casos de pequeno até médio porte, ou para quem está começando no desenvolvimento de APIs.

Ao falar de _frameworks_ maiores podemos citar o `*Adonis.js*` e o `*Nest.js*` , que são frameworks que trazem já uma estrutura de código e de pastas própria para ser seguida, implementando uma opinião mais presente no nosso desenvolvimento. São indicados para casos de médio à grande porte.

> Veremos como utilizar essas frameworks mais a frente. Por ora, o importante é entender conceitos gerais do node.

# Streams

Streams coleções de dados onde podem ser manipulador por pacotes. Ou seja, vamos supor que temos uma grande quantidade de dados para adicionar em um banco de dados. Ao invés de o servidor ler o arquivo inteiro e só depois começar a adicionar os valores no banco, ele pode fazer esse processo simultaneamente com a leitura.

Ou seja, a medida que o arquivo é mandado, ele já será enviado para o banco de dados. Isso nos trás performance e flexibilidade para nossas operações.

## Readable , Writable, e Transform Streams

Elas são divididas em `*Writables Streams*` e `*Readable Streams` - s*treams de escrita e streams de leitura, sucessivamente.

<aside> 💡 _**É de extrema importância entender que tanto a requisição quanto a resposta são automaticamente streams.**_

</aside>

Ou seja, o servidor pode enviar a resposta aos poucos, fazendo com que o cliente receba a requisição de pouco em pouco e vice versa.

### Exemplo

Vamos criar um documento chamado `*fake-upload.js*`. Com ele iremos simular o envio de dados aos poucos para o servidor. O objetivo será enviar um número a cada 1 segundo e no servidor tornar esse número negativo e retorná-lo.

Para isso criaremos uma classe que vai herdar os métodos de leitura de streams.

```jsx
//importando Readable do módulo de streams do node
import {Readable} from 'node:stream'

class OneToHundredStream extends Readable{
    index = 1

		// toda stream de leitura deve ter obrigatoriamente
		// um método de leitura - obviamente
    _read(){
        const i = this.index++

        setTimeout(()=>{
            if(i > 10){
								// ao darmos push nulo a stream é finalizada
                this.push(null)
            }
            else{

								// caso não tenhamos atingido o limite
								// iremos dar um push no vetor de stream *
                const buffer = Buffer.from(String(i))
                this.push(buffer)
            }
        }, 1000)
    }
}

// criando a conexão e enviando a requisição
fetch('<http://localhost:3333>', {
    method: 'POST',
    body: new OneToHundredStream(),
    duplex: 'half'
})
```

Note que ao dar push no vetor de streams utilizamos o `*Buffer.from()*` e dentro dele convertemos o dado para string. Mais a frente veremos com detalhes o que é um buffer, mas por agora podemos entendê-lo como uma forma de transitar informações de uma stream para outra, e ele só aceita strings.

> _Ou seja, o código acima faz o seguinte caminho:_

⇒ Faz a conexão com o [localhost:3333](http://localhost:3333), utilizando do método POST.

⇒ Esse POST possui em seu corpo uma stream que será enviada um número a cada 1 segundo

⇒ Caso o número seja menor que 10 ele enviará um buffer contendo o número atual. Caso o número seja igual ou maior que 10 ele cessará a stream.

> _**Agora precisamos manipular essa requisição do lado do servidor.**_

Para transformar streams, nós possuímos uma classe chamada Transform. Iremos importá-la e criar uma classe de transformação.

O construtor `*_transform*` aceita 3 parâmetros: `*chunk*`, `*encoding*` e `*callback*`.

- _**O `chunk` é o pacote atual relativo à coleção.**_ Ou seja, o pedaço atual em relação ao dado que estamos enviado. No nosso caso, dos 10 números, é o i atual do somatório.
- _O `encoding` ficará para um outro momento._
- _**O `callback` é uma função de escrita que será chamada quando a função de escrita terminou de realizar sua tarefa.**_ Serve também para retornar erros.

```jsx
import {Transform} from 'node:stream'

class InverseNumberStream extends Transform{

		// o construtor _transform aceita 3 parâmetros.*
    _transform(chunk, encoding, callback){
        const transformed = Number(String(chunk)) * - 1

        console.log(transformed)

				// neste caso não terá erros, então o primeiro
				// parâmetro será nulo

				// o segundo parâmetro envia o valor transformado
				// para a próxima stream
        callback(null, Buffer.from(String(transformed)))
    }
}
```

Até agora temos uma stream de leitura sendo enviada, e uma stream de transformação que manipulará os dados recebidos. Agora temos que, no servidor, receber, manipular e retornar.

```jsx
const server = http.createServer((request, response)=>{
					// encaminha para                   // encaminha
					// stream de transformação   				// para o cliente
    return request.pipe(new InverseNumberStream()).pipe(response)
})

server.listen(3333)
```

> _Ou seja, o código acima faz o seguinte caminho:_

⇒ Criamos primeiro o servidor, que irá receber uma requisição e uma resposta.

⇒ Esse servidor deve retornar o número de forma negativa na sua resposta. Para isso utilizamos o método `*pipe()` .*

<aside> 💡 Basicamente com ele encadeamos a resposta dos métodos enviando para novos métodos. Porém devemos utilizar a nomenclatura correta de cada coisa. Ou seja:

Encadeamos `*streams*`, transportando `*chunks*` em formato de `*buffer` .*

</aside>

⇒ Pegamos o buffer da requisição - o número 1, por exemplo - e encaminhamos para a stream de transformação que inverte esse número negativamente - se tornando -1 - e com essa resposta nós devolvemos ao cliente.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/df624a65-c543-47b5-99eb-7b9e50800202/Untitled.png)

## Leitura Integral de dados

O método acima é excelente para momentos onde temos informações como videos, fotos, textos mas não é indicado quando consumimos um arquivo JSON, com um objeto, por exemplo. Pensando nisso podemos utilizar do mesmo exemplo acima com essa outra abordagem.

```jsx
class OneToThreeStream extends Readable{
    index = 1

    _read(){
        const i = this.index++

        setTimeout(()=>{
            if(i > 3){
                this.push(null)
            }
            else{
                const buffer = Buffer.from(String(i))
                this.push(buffer)
            }
        }, 1000)
    }
}

fetch('<http://localhost:3333>', {
    method: 'POST',
    body: new OneToThreeStream(),
    duplex: 'half'
}).then((response)=> response.text()).then(console.log) // dando console.log da resposta
```

```jsx
const server = http.createServer(async (request, response)=>{
   const buffers = []
    console.log('Lendo dados..')

		// fazendo um for para juntar todos os chunks
		// vindos da requisição em um buffer só
    for await (const chunk of request){
        buffers.push(chunk)
    }

													// tomar cuidado pois aqui usamos o concat
													// do Buffer, que é responsável por concatenar buffers
    const fullStreamContent = Buffer.concat(buffers).toString()
    return response.end(fullStreamContent)
})
```

## Buffers

Durante os exemplos acima lidamos com os buffers. Podemos entendê-los como representações de espaços de memória do computador, utilizado para transitar dados de uma maneira muito muito rápida.

O node utiliza desse modelo pois é mais performático ler/escrever binários do que qualquer outro tipo. Importante salientar que os buffers convertem strings em binários, sendo assim, caso tenhamos que transitar outros tipos de dados que não são strings, devemos converter primeiro para o tipo que ele aceita - ou seja, uma cadeia de caracteres.

[Fastify.js](https://www.notion.so/Fastify-js-d22d0be4ae144d9eb8b6081ae2a79566?pvs=21)

node: [[Backend]]