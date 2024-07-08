## Introdução

> OBS.: para exemplos usaremos node.js

Uma requisição é o ato de conexão do cliente à um servidor com uma solicitação de alguma funcionalidade. Pode ser criação, listagem, mudança, exclusão, ou quem sabe uma ação específica. Para que o servidor saiba o que fazer, toda requisição possui uma série de configurações, mas as mais importantes para nós no momento são: _**o método e a URL.**_

Os métodos são informações sintáticas que servem para indicar qual ação o servidor irá realizar.

- **GET ⇒** Serve para solicitar um recurso do back-end.
- **POST ⇒** Serve para criar um recurso do back-end.
- **PUT ⇒** Serve para atualizar/modificar uma série de recursos no back-end.
- **PATCH ⇒** Serve para atualizar/modificar um único recurso no back-end.

Já a URL indica em qual área este método se aplica. Ou seja, caso tenhamos uma rota `*/users`* juntamente com um método de `*GET*`, nosso backend retornará uma listagem especificamente de usuários. Caso fosse um método `*GET*` mas de `*/postagens*` seria retornado uma listagem de postagens, por exemplo.

Assim como poderíamos mudar o método para `*POST*` na rota `*/users*` e solicitar ao backend para cadastrar determinado usuário, ou `*POST*` com `*/posts*` para fazer uma postagem.

## Cabeçalhos (Headers)

Os cabeçalhos servem para fornecer informação adicionais tanto para a parte da resposta quanto para a parte da requisição. Os Headers podem ter informar como determinado dado está sendo retornado, o status da requisição, quem é o cliente que está fazendo a requisição, dentre outras várias coisas. Por exemplo:

```jsx
import http from 'node:http'

// comecando com uma constante vazia
const user = []

const server = http.createServer((request, response)=>{
    const {method, url} = request

		// verificando se o método é GET e a rota é usuários
    if(method === 'GET' && url === '/users')
            return request.end(JSON.stringify(user))

		// verificando se o método é POST e a rota é usuários
    if(method === 'POST' && url === '/users'){
        user.push({
            name: 'fulano',
            id: 1
        })
        return request.end('Usuário Adicionado.')
    }

    return response.end('Hello World')
})

server.listen(3333)
```

Agora com o server iniciado, podemos fazer requisições da seguinte forma utilizando HTTTPie:

```jsx
http POST localhost:3333/users
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/af138adb-9334-4726-b614-5e4e461c5304/Untitled.png)

Agora podemos pegar o usuário:

```jsx
http GET localhost:3333/users
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/a6175e9e-7501-4cc3-a5df-0ebe0b664898/Untitled.png)

Veja que não temos nenhuma indicação de qual tipo de retorno essa solicitação obteve. Sabemos que ele retorna um JSON só porque nós que estruturamos o código. Para corrigir isso, utilizamos os cabeçalhos para retornar uma resposta mais robusta para nosso cliente.

Temos diversos headers disponíveis e que podemos utilizar em nossa aplicação. Um deles é o `*Content-type*`, que informa qual o tipo de dado retornado ou o tipo de dado solicitado para retorno. Para indicar que é um JSON, devemos explicitar com `*application/json*`

```jsx
const server = http.createServer((request, response)=>{
    const {method, url} = request

    if(method === 'GET' && url === '/users')
						// o método setHeader define um atributo e um valor
            return response
											.setHeader('Content-type', 'application/json')
											.end(JSON.stringify(user))

    if(method === 'POST' && url === '/users'){
        user.push({
            name: 'fulano',
            id: 1
        })
        return response.end('Usuário Adicionado.')
    }

    return response.end('Hello World')
})
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/746793a2-c230-46f3-b36f-72da9b6789fc/Untitled.png)

### STATUS CODE

É muito comum que na resposta de nossas requisições tenhamos um código de status retornado pelo servidor. São conjuntos de código que vão de 100 a 599 e servem para informar o cliente sobre o resultado interno da requisição.

1. [Respostas Informacionais](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#information_responses) (`100` – `199`)
2. [Respostas de sucesso](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#successful_responses) (`200` – `299`)
3. [Respostas de Redirecionamento](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#redirection_messages) (`300` – `399`)
4. [Erros pelo lado do cliente](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#client_error_responses) (`400` – `499`)
5. [Respostas de erro interno do servidor](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#server_error_responses) (`500` – `599`)

Abaixo podemos ver as mais comuns de cada categoria:

**Respostas de Sucesso - 200 - 299**

- 200 ⇒ A requisição obteve sucesso.
- 201 ⇒ A requisição obteve sucesso e foi criado um novo recurso no servidor.

**Respostas de Redirecionamento - 300 - 399**

- 301 ⇒ A URL da requisição foi movida permanentemente. A URL nova é devolvida.
- 302 ⇒ A URL da requisição foi movida temporariamente.

**Respostas de Erro do lado do Cliente - 400 - 499**

- 400 ⇒ O servidor não conseguiu processar a requisição pois há algo de errado nela. O cliente mandou algo errado.
- 401 ⇒ O cliente precisa de autorização para que a requisição seja executada.
- 403 ⇒ O cliente não possui autorização para realizar a requisição desejada.
- 404 ⇒ A rota não foi encontrada pelo servidor.

**Respostas de Erro do lado do Servidor - 500 - 599**

- 500 ⇒ Erro interno do servidor.

# Rotas e Parâmetros

Ao fazer uma requisição à uma API, seja originado de um outro backend ou um front end, temos 3 meios de adicionar informações em nossa chamada.

- Query Params
- Route Params
- Request Body

## Query Params

São parâmetros presentes no próprio endereço da requisição. Usados quando precisamos de uma `*URL Stateful` , s*ervindo para modificar a resposta da API quando os dados não são sensíveis. Utilizados para filtros, paginação, busca.

_**Exemplo:**_

<aside> 💡 [http://localhost/movies?genre=action](http://localhost/movies?genre=action)

</aside>

## Route Params

São parâmetros presentes no próprio endereço da requisição, mas que são usados para identificação de recursos. Em conjunto com o método podemos inferir o que a rota significa.

_**Exemplo:**_

<aside> 💡 GET [http://localhost/movies/1](http://localhost/movies/1)

Subentende-se que queremos capturar o filme com o ID 1

</aside>

## Body Request

Utilizado para envio de um montante de informações, geralmente de um formulário. Dados que não faria sentido adicionar nos parâmetros de rota pois ela ficaria muito grande, assim como poderia expor dados sensíveis.

node: [[Backend]]