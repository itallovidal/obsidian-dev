# Formas De comunicação com um Banco

## Driver nativo

É a forma de construir consultas `*sql*` de forma bem baixo nível, ou seja, mais perto do banco de dados, explorando bem os conceitos e sintaxe da linguagem SQL.

Então, como exemplo, a sintaxe de uma query feita com `MySQL` ficaria assim

```jsx
// Para buscar um usuário com id = 1
SELECT * FROM usuarios WHERE id = 1
```

## Query builders

Os _query builders_, também conhecido como construtores de consultas, são ferramentas essenciais para a realização de consultas em um banco de dados.

São responsáveis por facilitar essas consultas pois, possuem uma interface intuitiva para fazer com que seja possível realizá-las de maneira intuitiva e eficiente, amenizando a necessidade de um conhecimento aprofundado na linguagem ou no banco de dados que está sendo utilizado.

Eles permitem que seja possível construir um consulta sql sem se preocupar com a sintaxe da linguagem ou o tipo de banco que está utilizando. Dessa forma, as querys serão criadas de acordo com funções disponibilizadas pela biblioteca query build que estiver utilizando, e esse comando corresponderá a um comando nativo.

Então, como exemplo, a sintaxe de uma query feita com `knex` que é um query builder de `javascript` ficaria assim

```jsx
// Para buscar um usuário com id = 1
knex('usuarios').where('id', 1) 
```

## ORM - Object Relational Mapper

Responsável por integrar POO com o banco de dados, utilizando objetos e classes. Praticamente nenhuma preocupação com a sintaxe da linguagem SQL ou o banco que está sendo utilizado. Para montar as querys será utilizado objetos e métodos, sem precisar escrever SQL diretamente. Dessa maneira, você pode manipular os dados usando objetos e métodos, sem precisar escrever SQL diretamente

Então, como exemplo, a sintaxe de uma query feita com `sequelize`, ficaria assim

```jsx
// Para buscar um usuário com id = 1
User.findByPk(1).then(user => {
   console.log(user);
}).catch(error => {
   console.error(error);
});
```

# Migrations: O que são?

São controles de versão dentro do nosso banco de dados. Bem parecido com o que fazemos com o _git_ em relação ao código como um todo, porém neste caso, são específicos para versionamento do nosso banco. Ou seja, caso tenhamos que voltar uma atualização do banco porque algo deu errado, temos esse histórico. Então cada atualização será uma nova _migration_.

