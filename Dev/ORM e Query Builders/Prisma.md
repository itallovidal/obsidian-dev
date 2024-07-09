# O que é?

O prisma é um ferramenta utiliza do _orm_ e _query builder_ para conectar ao banco de dados. Ele possui uma boa integração com o typescript e migrations automatizadas
### Instalação e configuração

Primeiro é necessário instalar o _prisma_ como uma dependência de desenvolvimento e baixar a extensão dele

```bash
npm i prisma -D
```

![[Pasted image 20240708205155.png]]

Depois disso é necessário gerar o arquivo de conexão com o banco de dados, para isso basta rodar o seguinte código.

```node
npx prisma init
```

Ao rodar esse comando uma pasta _prisma_ será criada, dentro dela serão guardadas as informações sobre o banco. Nela virá um arquivo _schema.prisma,_ e ele será responsável por armazenar o schema das tabelas do banco.
![[Pasted image 20240708205238.png]]

Além disso é importante adicionar nas configurações do editor o seguinte trecho de código. Ele diz que para todos os arquivos do tipo _prisma_ será feita uma formatação com o objetivo de formatar o código, assim como o _eslint_ faz.

```json
"[prisma]": {
    "editor.formatOnSave": true
  },
```

Para criar a conexão com o banco será necessário instalar o `*prisma client*`

```jsx
npm i @prisma/client
```

Depois de instalado, basta criar uma variável que será responsável por guardar essa conexão. Para isso, basta instanciar ela como um objeto do tipo `PrismaClient()`
![[Pasted image 20240708205316.png]]
Pronto! agora com essa variável é possível conectar e alterar as tabelas do banco. Como por exemplo, no código abaixo, utilizando essa variável `prisma` é possível acessar a tabela `user` e criar uma data

![[Pasted image 20240708205457.png]]

### Criação de tabelas (Model)

No prisma uma tabela é chamada de _model_ e para criar uma basta seguir a seguinte sintaxe

```jsx
model User{
  id String @id @default(uuid())
  email String @unique? // ? = opcional

  @@map("users")
// 1 @ é configuração da coluna, 
// 2 @ é configuração da tabela
}
```

Nesse exemplo está sendo criada uma tabela(model) chamada _User,_ que possui as colunas _id, nome e email._ A coluna id é do tipo string e possui os atributos `@id` - _informa que é a chave primaria -_ e `@default()` _- informa o valor default._ Já o `@@map()` é utilizado para renomear algo, nesse caso está renomeando a tabela, se estivesse apenas com 1 @ estaria renomeando a coluna _email_


> [!NOTE] Para saber mais:
> ["Documentação do Prisma"](https://www.prisma.io/docs/orm/prisma-schema/data-model/models#defining-attributes)

Com a criação da tabela, no caminho `node_modules/.prisma/client` terá um arquivo _index.d.ts_ que criará um tipo pra tabela e alguns métodos para utilizar nela

![[Pasted image 20240708205550.png]]

### Relacionamento

O relacionamento é a conexão entre dois models(tabelas). Para exemplificar como é realizado esses relacionamentos, vamos supor que existam duas tabelas, `*user` e `post` .* Nesse relacionamento*(1 : N)*, um _user_ pode possuir diversos _posts_ mas um _post_ só pode possuir um _user._

```jsx
model User {
  id    Int    @id @default(autoincrement())
  posts Post[]use
}

model Post {
  id       Int  @id @default(autoincrement())
  user     User @relation(fields: [userId], references: [id])
  userId Int // relation scalar field  (used in the `@relation` attribute above)
}
```

Dessa maneira, a tabela _User_ tem um relacionamento 1:N com a tabela _Post_, ou seja, um usuário poderá possuir diversos posts, por isso a tabela _User_ receberá um vetor de _posts_ do tipo _Post._

![[Pasted image 20240708210206.png]]

Já a tabela _Post_ tem um relacionamento 1:1 com a tabela _User,_ ou seja, um post é possui apenas um usuário, por isso a tabela _Post_ receberá um relacionamento do tipo _User,_ para isso será utilizado o atributo `@relation` ele recebe por parâmetro o campo que será a chave estrangeira na tabela _post_ e o campo da tabela _User_ que irá fazer a relação. Nesse caso, a chave estrangeira _userId_ da tabela _Post_ faz relação com o _id_ da tabela _User_

<aside> 💡 A variável _userId_ não será criada no banco, ela é responsável apenas pelo relacionamento, para ligar as tabelas

</aside>

## Migrations

As migrations são os históricos dos containers. Para gerar uma migration é preciso rodar o seguinte comando

```jsx
npx prisma migrate dev
```

Ao rodar esse comando, o prisma vai ler o arquivo `schema.prisma` e guardar uma migration das alterações que foram feitas nesse arquivo em comparação com o que existe no banco. Assim que for rodado esse comando, ele irá pedir um nome para a _migration,_ e ai é necessário escrever as alterações que serão feitas com esse novo arquivo

![[Pasted image 20240708210529.png]]

E dessa forma é gerada uma nova _migration_ na pasta de _migrations_

## Acessando o banco

Para acessar as informações do banco basta rodar o seguinte comando, e ele abrirá uma interface na web com os dados do banco

```jsx
npx prisma studio
```

![[Pasted image 20240708210850.png]]

node: [[ORM e Query Builders]]
node: [[Node]]