## Knex - Query Builder

Para fazer as requisições com o banco de dados, podemos fazer de forma mais baixo nível enviando as _querys_ da forma mais parecida com o que um banco de dados manipula ou podemos utilizar de _query Builders_ que é o caso do _KNEX_. Neste segundo caso nós utilizamos da linguagem em questão - no caso _Java Script_ - para formular nossas consultas. Isso trás uma sintaxe que estamos mais habituados, sendo mais fácil para manipular.

Por exemplo: Para pegar um usuário com o nome de ‘João’.

```jsx
SELECT id FROM users WHERE name='joão'
```

Com Knex podemos fazer de uma forma ligeiramente diferente:

```jsx
Knex('users').where({
	name: 'joão'
}).select('id')
```

Note que é a mesma consulta, porém com uma sintaxe de objetos que já estamos acostumados. Esse modelo é muito usado também em banco de dados como _supabase_ e _firebase_. A diferença é que os _Query Builders_ apenas montam a consulta, enquanto os outros dois fornecem todo um objeto de configuração do banco, abrangendo não apenas a consulta, mas sendo o banco de dados também.

### Instalação e configuração

Para instalar precisamos, depois do _Knex_, adicionar o nome do banco de dados para que o ele faça a configuração necessária.

```jsx
npm install knex --save
```

```jsx
npm install sqlite3
```

Depois vamos criar um documento onde iremos configurar algumas coisas como o nome do banco, o objeto de configuração, e etc. Aqui iremos informar ao _Knex_ qual o _client_ que iremos utilizar - _mysql_, _sqlite_, _mariaDB_ etc. - e qual o endereço para que ele faça a conexão. O _SQLite3_ possui a diferença de ter a possibilidade do banco ser localizado na nossa própria máquina, sendo um arquivo local, não precisando se conectar a um servidor.

Ou seja, cada _client_ possui uma forma ligeiramente diferente de conexão, o importante é entender que esse objeto deve identificar essa forma de se conectar o nosso app ao banco.

```jsx
import { knex as knexSetup } from 'knex'

export const knex = knexSetup({
	client: 'sqlite',
	connection:{
		//localização do arquivo
		filename: './temp/app.db'
	}
})
```

### Migrations

Como funciona o controle de versões do banco pelo _Knex?_

Para que o _Knex_ seja usado junto com TS, precisamos mudar algumas coisinhas.

```jsx
import knex, { Knex } from 'knex';

export const config: Knex.Config = {
    client: 'sqlite',
    connection:{
        //localização do arquivo
        filename: './temp/app.db'
    },
		migrations:{
			extension: 'ts',
			directory: './db/migrations'
		}
    useNullAsDefault: true
}
export const knexObj = knex(config)
```

```jsx
// script do knex
"knex": "node --loader tsx ./node_modules/knex/bin/cli.js"
```

```jsx
// criamos nossa migration agora desta forma
npm run knex -- migrate:make create-documents
```

Foi criado um documento desta forma:

```tsx
import { Knex } from "knex";

// para atualizar o banco de dados 
export async function up(knex: Knex): Promise<void> {
}

// para remover essa atualização
export async function down(knex: Knex): Promise<void> {
}
```

Repare que se no `*up*` nós criamos uma tabela e preenchemos suas colunas, no `*down*` nós desfazemos essa operação. Desta forma é mais simples de manipular as atualizações e ter um histórico delas.

```tsx
export async function up(knex: Knex): Promise<void> {
    await knex.schema.createTable('transactions', (table) =>{
        table.uuid('id').primary()
        table.text('title').notNullable()
    })
}

export async function down(knex: Knex): Promise<void> {
    await knex.schema.dropTable('transactions')
}
```

Agora basta executar as _migrations_:

```tsx
npm run knex -- migrate:latest
```

Para dar _rollback_ é só utilizar

```tsx
npm run knex -- migrate:rollback
```

node: [[Bibliotecas]]