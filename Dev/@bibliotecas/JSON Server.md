Essa é uma biblioteca perfeita para projetos onde não temos um back-end, porém precisamos de uma API que nos forneça informações e dados para que o nosso front-end seja alimentado. Com ela torna-se possível criar um `*json*` local com as informações de rotas e dados e consumi-las como se fosse uma API real, podendo ordenar, paginar, fazer `*querys*`, fazer método POST e muito mais.

### Instalação

```tsx
npm i json-server -D
```

### Setup

Para configurar é muito simples:

- Precisamos primeiro criar um arquivo `*json*` chamado de `*Server.JSON*`.
- Nele, criaremos um objeto onde terá todas as rotas de nossa aplicação.
- Depois de criar nossas rotas, passaremos o que essa rota irá devolver quando requisitada.

### Iniciar o servidor

Para inicializar essa “API”, devemos utilizar o seguinte comando:

```tsx
npm json-server nome-do-documento.json 
```

Note que nós utilizaremos abaixo dois parâmetros opcionais:

- O `*-*w` que significa “watch”, que basicamente informa para o `*JSON.Server*` ficar verificando se há mudanças no nosso arquivo para ele atualizar o servidor.
- O `-d` que significa “delay”, que fará com que o `*JSON.Server*` demore x ms para devolver nossa requisição. Isso é excelente pois faz parecer uma API mais próxima à realidade.

```tsx
npm json-server server.json -w -d 500
```

Para não precisarmos escrever tudo isso toda vez que formos mexer no projeto, podemos facilmente criar um script no `*package.JSON*` na área de `*scripts` .*

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4f9b5876-d305-4abb-966b-10c5f4715642/Untitled.png)

```json
"json-server": "json-server server.json -w -d 500",
```

### Exemplo

Vamos supor que temos o seguinte JSON:

```json
{
  "users": [
    {
      "id": 1,
      "name": "alfredo",
      "age": 20
    },
    {
      "id": 2,
      "name": "Giorgina",
      "age": 34
    },
    {
      "id": 3,
      "name": "Antonio",
      "age": 13
    },
    {
      "id": 4,
      "name": "ZéPedro",
      "age": 10
    }
  ]
}
```

Podemos acessar nossos usuários pela URL:

```json
<http://localhost:3000/users>
```

Se fosse só o que foi apresentado já seria incrível, porém essa biblioteca vai muito além.

Podemos pesquisar:

Por um valor genérico:

```json
// retornará o terceiro usuário
<http://localhost:3000/users?q=24>
```

Por um valor de uma propriedade específica:

```json
// retornará o quarto usuário
<http://localhost:3000/users?name=ZéPedro>
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7069de47-5565-4c7a-b866-ac4304c75115/Untitled.png)

Ordenação:

```json
// retornará todos os usuários 
// com base na propriedade X
<http://localhost:3000/users?_sort=age>
```

> Obs.: Podemos ordenar de forma decrescente utilizando `*_order=desc*` .

```json
/users?_sort=age&_order=desc
```

Paginação:

```json
// retornará todos os usuários 
// com base na propriedade X
<http://localhost:3000/users?_page=1>
```

> Obs.: Por padrão, a paginação retorna os primeiros 10 elementos. Mas podemos alterar esse limite com `*_limit*`

```json
/users?_page=1&_limit=2
```

node: [[Bibliotecas]]