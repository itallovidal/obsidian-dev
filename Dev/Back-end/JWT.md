# Fluxo de Autenticação

Em uma aplicação onde há um sistema de cadastro, é muito comum que tenhamos que estar logados para que possamos realizar determinadas tarefas e ter acesso a determinadas informações. O sistema deve saber quem é o usuário para que ele possa avaliar se será possível liberá-lo ou não.

[JWT (JSON Web Token), why do we need it ? and how does it work ? | by Haytam Benayed | Medium](https://medium.com/@haytambenayed/jwt-json-web-token-why-do-we-need-it-and-how-does-it-work-bf1744e57db5)

# Etapas

- O usuário faz uma requisição ao backend com email e senha - por exemplo.
- O backend então, verificando que o usuário existe, e se sim, devolve um token de autenticação.
- Com esse Token de autenticação, o usuário poderá fazer outras requisições junto com ele para mostrar que ele está autenticado a realizar determinadas tarefas.

No processo de geração do Token é que entra o Jason Web Token - ou JWT.

# Estrutura

Um JWT é dividido em três partes:

- Header: Responsável por descrever o algoritmo criptográfico aplicado e opcionalmente mais informações.
- Payload: Responsável por conter informações sobre o cliente. **
- Signature: Parte onde o servidor verifica a integridade do token. É uma chave encriptada resultante da encriptação definida no header + uma chave secreta.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/05613e39-2dfb-4dbe-b37d-2c1b7610c933/Untitled.png)

# Autenticação VS Identificação

_**A autenticação**_ é o processo de confirmação da identidade de um usuário ou dispositivo. É o processo de validar de o usuário faz parte de um determinado sistema ou não.

_**A identificação**_ é o processo de liberação de quais recursos aquele usuário pode vir a manipular. Com o usuário ou dispositivo já autenticado, é nessa parte que o sistema irá conceber permissões para ele manipular, modificar, deletar, ver os recursos.

# Processo de Geração de Token

Instalação via NPM:

```tsx
npm i jsonwebtoken
```

Para gerar um Token, precisamos primeiramente de gerar um `*secret`* para ser usado na hora da criptografia e defini-lo nas variáveis de ambiente.

<aside> 💡 Dica: Podemos utilizar no terminal a biblioteca crypto para gerar uma string randomica:

</aside>

```tsx
[require('crypto').randomBytes(64).toString('hex')](AsyncStorage)
```

Geraremos duas chaves: uma para acesso e uma para refresh.

```tsx
ACCESS_TOKEN_SECRET=a8cb29583bc531ea8aa807b4ae4f19497dc593d4f64ae3e6f65252cbbd1857a268f6d51b5661f7bc81de7c78c5864514c22d4a28e95b7c16c98a87b4a5353645
REFRESH_TOKEN_SECRET=bc5ba8984a9cdbc154110468a3e46e5cccbae39eab014ea1bdd4c67299e017c3e1dfcb3d4377c2b5b3c4aa676f2b46855054cadd33d7558107bf51bd5c0fb35f
```

Depois podemos importar essas variáveis de ambiente e utilizar o método `*sign*` disponível na biblioteca do JWT. Esse método é responsável por pegar o segredo e as informações para encriptografar.

```tsx
*sign*(user, process.env.ACCESS_TOKEN_SECRET)
```

require('crypto').randomBytes(64).toString('hex')

node: [[Backend]]