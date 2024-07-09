`*Axios*` é uma biblioteca para requisições HTTPS. Ela é uma alternativa à API `*Fetch*` nativa do JS, onde possibilita uma manipulação mais fácil e com mais opções.

### Instalação

```json
npm i axios
```

### Setup

Para usarmos o axios precisamos criar um objeto onde configuraremos o básico das nossas requisições. Criarem os um objeto que irá conter informações gerais do nosso fetch. Por exemplo, informamos a URL Base, indicando que todos os fetchs utilizando essa variável serão para esse endereço. Podemos explicitar uma autorização também, caso necessário. Vejamos:

```json
import axios from "axios";

export const Api = axios.create({
							// url base
    baseURL: '<http://localhost:3000/>'
})
```

Pronto, agora podemos fazer nossos métodos GET, POST, DELETE etc. etc. etc. de uma forma um pouco mais direta e fácil. Exemplo:

### GET

```jsx
															//url a add na url base
const response = await Api.get('transactions')

// não precisamos passar para json, 
// apenas acessar a propriedade "data"
return response.data
```

Abaixo podemos ver o objeto retornado pelo `*get*`

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e454d558-ce47-4f11-b5ce-3e20cd04798f/Untitled.png)

### Adicionando Parâmetros

Podemos adicionar um objeto de configurações contendo os parâmetros da nossa query String.

```jsx
const response = await Api.get('transactions', {
        params:{
            q: query
        }
    })
```

Você pode adicionar neste objeto outras propriedades que sua API aceita, como campos neste caso `*_order*` e `*_sort*`, para ordenar de forma descendente.

```jsx
const response = await Api.get('transactions',{
        params:{
            q: query,
            _order: 'desc',
            _sort: 'createdAt'
        },
    })
```

### Post

Com a estrutura similar ao método `*GET*`, aceita uma rota e um objeto com todos os campos que usaremos para fazer o `*POST*` em nosso servidor. Retorna código 201 - elemento criado - caso tudo ocorra da forma correta.

```jsx
const response = await Api.post('transactions', {
            type: transferType,
            price, description,
            category,
            createdAt: new Date()
        })
```

# Axios Exceptions

```jsx
try{
    const {data} = await Api.post('/users', {
        name,
        password,
        email,
		})
      console.log(data)
  }catch (e){
      if(axios.isAxiosError(e))
          console.log(e.response?.data.message)
  }
```

node: [[Bibliotecas]]