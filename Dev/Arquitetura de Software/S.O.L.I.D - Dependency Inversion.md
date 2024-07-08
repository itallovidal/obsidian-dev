Os princípios S.O.L.I.D. são muito famosos no paradigma orientado a objetos para manter o código limpo e manutenível, mantendo o código bem separado, facilitando a refatoração e o reaproveitamento de código. Criado por Robert Martin _- mais conhecido como Uncle Bob -_ qual também foi muito importante para princípios de clean code.

- **S.O.L.I.D.** é um acrônimo para:
    - **S →** Single Responsability Principle ****_(Princípio da responsabilidade única)_
    - **O →** Open-Closed Principle ****_(Princípio Aberto - Fechado)_
    - **L →** Liskov Substitution Principle ****_(Princípio da substituição de Liskov)_
    - **I →** Interface Segregation Principle ****_(Princípio da Segregação da Interface)_
    - **D →** Dependency Inversion Principle ****_(Princípio da inversão da dependência)_

## D - Dependency Inversion

Segundo o próprio **`*Uncle Bob:*`**

> “_Módulos de alto nível não devem depender de módulos de baixo nível. Ambos devem depender da abstração.”_

> “_Abstrações não devem depender de detalhes. Detalhes devem depender de abstrações.”_

Ou seja, o _Princípio da Inversão de Dependências_, tem o intuito de fazer com que determinadas classes não sejam dependentes de uma determinada instância para funcionar corretamente.

Por exemplo, vamos supor que temos uma classe que adiciona um usuário ao banco de dados `*mySQL*`. Nesta classe, instanciamos o objeto de conexão ao banco `*mySQL*` e o utilizamos para registrar o usuário.

```jsx
class RegisterUser {
    private dbConnection;
    
    construct()
    {       
        this.dbConnection = new MySQLConnection();           
    }
    
    // pense que temos aqui um método de registro.
}
```

O problema de fazer isso é que mais tarde, caso precisemos trocar o banco, utilizando por exemplo um `*SQLServer*`, teremos que mexer na nossa classe que cadastra o usuário. Ela está diretamente dependente do banco de dados que ela está recebendo.

O _Princípio da Inversão de Dependências_ faz com que mudemos um pouco essa lógica. Ao invés da nossa classe que cadastra o usuário manipular um banco do tipo X ou Y especificamente, ela irá receber um objeto a qual infere que terá essa conexão.

Isso faz com que o nosso código não dependa de um banco em específico, não fazendo diferença se é `*SQLServer*`, `*mySQL*` ou `*postgreSQL*`, por exemplo.

```jsx
// a interface dita que para um banco funcionar
// ele deve necessariamente implementar uma funcão 
// de conexão
interface DBConnectionInterface
{
    connect();
}

class MySQLConnection implements DBConnectionInterface
{
    connect()
    {
        // ...
    }
}

class OracleConnection implements DBConnectionInterface
{
    connect()
    {
        // ...
    }
}

class RegisterUser {
    
		// agora o construtor receberá um objeto de  banco de dados
		// que ele sabe que terá uma conexão. Não importa o banco.
    construct(private dbConnection: DBConnectionInterface){}
    
    // pense que temos aqui um método de registro.
}
```

Então ao utilizar o `*RegisterUser`* nós podemos escolher qual dependência ele irá utilizar sem que ele necessariamente dependa de uma em específico.

```jsx

const db = new MySQLConnection()
const registerUser = new RegisterUser(db)
```

node: [[Arquitetura de Software]]