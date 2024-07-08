Como dito anteriormente o fastify é um `*microframework*`. Utilizaremos ele para que possamos desenvolver nossos próximos projetos. Para instalarmos o `*fastify*` é muito simples:

```jsx
npm init -y
npm i fastify
npm i -D typescript @types/node
npm i tsx
```

Depois disso, devemos criar um script para rodar nossa aplicação. Já que ficar encerrando ela e startando toda hora é muito chato, vamos usar um script que cuidará disso para nós: basta salvar a aplicação. Coloque no package.json

```jsx
  "scripts": {
    "start": "tsx watch src/server.js"
  },
```

E vamos só modificar o target do TSConfig:

```jsx
"target": "ESNext",  
```

Para um primeiro momento, para subir um servidor é muito simples. Precisamos apenas importar os módulos do `*fastify*`, e ativá-lo passando para uma variável.

Chamaremos de `*app*` . Essa variável nos proporcionará muitos métodos e propriedades necessárias para configurarmos nosso servidor. Por exemplo, podemos utilizar o método `*listen*` para iniciar o servidor com um objeto de configuração como host, porta e etc. Assim como podemos definir rotas com métodos HTTP.

```jsx
// código deve ser colocado na pasta src/

// importando todos os módulos de fastify
import fastify from "fastify";

// iniciando o fastify
const app = fastify()

// iniciando o servidor na porta 3333
app.listen({
    port: 3333
}).then(()=>{
//quando o servidor estiver no ar, dar console.log
    console.log('server running!')
})
```

## Configuração de Rotas

Agora nosso servidor está no ar, porém não há nenhuma rota configurada. Podemos definir rotas de duas formas: Com o método da requisição desejada - `*app.post()*`, `*app.get()*`, `*app.update()`* etc. _-_ ou utilizando um método chamado `*app.route()*` que configura a rota. Vejamos: **

> OBS.: lembre-se de reiniciar o servidor ou dar `*—watch*` para que o servidor seja de fato atualizado.

```jsx
import fastify from "fastify";

const app = fastify()

//definindo uma rota get
app.get('/hello', async ()=> {
    return 'hello world!'
})

app.listen({
    port: 3333
}).then(()=>{
    console.log('server running!')
})
```

Ou podemos utilizar:

```jsx
import fastify from "fastify";

const app = fastify()

//definindo uma rota get
app.route({
    method: "GET",
    url: '/',
    handler: async()=>{
        return 'Hello World!!'
    },
})

app.listen({
    port: 3333
}).then(()=>{
    console.log('server running!')
})
```

Ambas as formas fazem a mesma coisa, são apenas approaches diferentes.

## Separando as rotas

Como já sabemos, uma rota é responsável por manipular um determinado segmento dentro da lógica da nossa aplicação. Então se temos uma rota chamada `*users*` , subentende-se que todas as requisições relacionadas à ela consumirão recursos relacionados aos usuários como login, listagem de um usuário específico, todos os usuários e assim por diante.

Assim como se tivermos uma rota `*movies*` ela seja responsável por manipular recursos de filmes. Dito isso, em uma aplicação teremos muitas rotas e subrotas, e mantê-las em um mesmo arquivo é ruim para legibilidade e manutenção. Pensando nisso podemos criar rotas em um arquivo separado e registrá-las no nosso arquivo principal.

```jsx
// src/routes/usersRoute.ts

import {FastifyInstance} from "fastify";

// é basicamente uma função que terá as rotas 
// relacionadas a um determinado recurso

// para que tenhamos o intelissense do ts, devemos
// tipar o app com a interface FastifyInstance
export async function usersRoutes(app: FastifyInstance){

    app.get('/', async ()=>{
        return 'essa rota retorna todos os usuários..'
    })

    app.get('/login', async ()=>{
        return 'essa rota é responsável pelo login'
    })
}
```

E agora devemos registrar essa rota no nosso servidor.

```jsx
import fastify from 'fastify'
import {usersRoutes} from "./routes/usersRoutes";

const app = fastify()

// passamos a função e um objeto de config
// onde recebe uma propriedade chamada 'prefix'
// toda vez que esse prefixo for usado, chamará 
// a função desejada
app.register(usersRoutes, {
    prefix: 'users',
})

app.listen({
    port: 3333
}).then(()=>{
    console.log('Servidor No ar!')
})
```

Pronto, agora ao chamar a rota `*/users*` chamará a função de rotas e consequentemente chamará as subrotas desejadas. Se passarmos, por exemplo, `*/users/login*` chamará o segundo `*get`.* Agora se precisarmos de uma outra rota, de filmes, por exemplo - pensando em uma api que lida com cadastro de usuários e filmes - podemos fazer o mesmo processo: criar um documento com uma função de rotas, e depois registrar essa função no server.ts.

## Parâmetros e Query Strings

Agora que já configuramos e separamos nossas rotas podemos aprender como lidamos melhor com elas. Para capturar rotas dinâmicas é muito simples. Basta adicionar `*:*` antes do parâmetro. Depois, ele estará disponível em um objeto chamado `*params*` dentro do objeto `*request*` . Vejamos no exemplo abaixo: vamos supor que queremos pegar o usuário por id.

```jsx
import {FastifyInstance} from "fastify";

export async function usersRoutes(app: FastifyInstance){
    // dois pontos antes de id
		app.get('/:id', async (request, reply)=>{
        return `ID escolhido: ${request.params.id}`
    })
}
```

Podemos ver que a função anônima assíncrona pode vir a receber dois parâmetros, `*request*` e `*reply*` . Esses parâmetros são passados da função `register` lá do documento server.ts. São objetos que contém informações da requisição e da nossa resposta, consecutivamente.

E nossos parâmetros estão dentro da requisição, dentro do objeto de parâmetros. Basta acessar seus valores com a notação de ponto - `*request.params.propriedadeDesajada*`

Muito simples. Para acessar uma query string é muito parecido. Estará dentro da requisição, no objeto `*query*`. Por exemplo, se quisermos pesquisar usuários mas que tenham a idade igual a X anos:

> localhost:3333/users?idade=23

```jsx
app.get('/',async (request, reply)=>{
        return `Retornando usuários onde a idade é igual a ${request.query.idade}`
    })
```

## Validações

A manipulação é bem simples. A questão é que nem sempre tudo pode acontecer como deveria. Por exemplo, pode ser que o parâmetro id devesse aceitar apenas número e foi enviado uma `*string*`. Ou a query `*string*` estava com o valor vazio ou inexistente. O fastify proporciona um sistema de schema nativo para esse tipo de situação. Vejamos:

O objeto `*schema*` possui a seguinte estrutura:

```jsx
// tipando o nosso schema
const schema: FastifySchema = {
		querystring: {
        properties: {
            idade: { type: 'number'}
        },
        required: ['idade']
    }
}
```

O que pdemos validar:

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/571090e7-79be-4cd7-86fc-33b029425d57/Untitled.png)

O schema acima molda a requisição e obriga que ela tenha uma querystring, e essa querystring deve ter a propriedade idade, e o seu valor deve ser um número. Para aplicar esse schema podemos passar um objeto de configuração na rota e passar na propriedade equivalente:

```jsx
app.get('/', {
        schema: schema
		    }, 
				async (request, reply) => {
		        return `Retornando usuários onde a idade é igual a ${request.query.idade}`
		    })
```

Agora quando chamamos a rota de maneira errada ela mostra a seguinte mensagem:

Sem querystring

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/7c3e8074-f27c-4d1b-a7a1-0f57c88736c4/Untitled.png)

idade com letras

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/1267465d-e0de-4445-80cb-3c74cd5074bf/Untitled.png)

## Validação com ZOD

Zod é uma biblioteca incrível de validação de dados. Possui uma documentação bem simples e completa. Com ela podemos fazer essa validações de uma forma bem simples também. Depois de instalado, podemos fazer da seguinte forma:

```jsx
// criamos um schema que é um objeto zod. 
// Ele possui o campo idade.
// esse campo deve receber um número, 
// e esse número deve ser maior que 0
const schema = z.object({
    idade: z.coerce.number({
        invalid_type_error: 'Valor de idade precisa ser um número.',
    }).min(1, {message: 'O valor precisa ser maior que 0'})
})
```

```jsx
app.get('/', async (request, reply)=>{
			
				// função safeParse valida sem dar throw no erro
        const dataParsed = schema.safeParse(request.query)
				
				// caso a validação tenha dado errado, retornamos o objeto
				// que informa tudos os problemas na validação
        if(!dataParsed.success){
            return dataParsed.error.issues
        }

				// caso contrário podemos desestruturar os campos
        const {idade} = dataParsed.data
        return `essa rota retorna todos os usuários onde a idade é maior que ${idade}`

    })
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/43b507db-3312-4ecc-93fb-c06142d72d5e/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/9a95c774-d947-4c27-887e-8a0b1b2c817b/Untitled.png)

Com o zod acaba ficando muito simples de fazermos uma série de validações e manter suas mensagens de erros personalizadas. É bem simples e a biblioteca é muito leve. Caso queira fazer de modo nativo não tem problema, é bem completa e também dá conta do recado.

node: [[Node]]
