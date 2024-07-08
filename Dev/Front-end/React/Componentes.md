
Uma aplicação React é composta por diversos elementos chamados componentes. Esses componentes são pedaços da interface que se juntam para formar as telas que vemos. Por baixo dos panos, são funções que possuem sua lógica interna e no fim, exportam um trecho de _HTML._

Códigos de React são, em sua maioria, escritos em uma linguagem chamada JSX, a qual vimos anteriormente na introdução à biblioteca. Abaixo vamos ver qual a estrutura necessária e algumas regras na criação dos nosso componentes.

Abaixo temos um componente de barra de navegação. Por ser uma função, sua estrutura é muito parecida com uma função comum, porém para ser considerado um componente seu nome deve, obrigatoriamente, ter a primeira letra em maiúsculo.

Então temos a nossa `*nav`* sendo retornada pelo componente, e depois ele sendo exportado. No documento principal _App.jsx_ o importamos utilizamos como se fosse uma `*tag*` personalizada.

```jsx
// navbar.jsx

import React from 'react';

function Navbar() {
    return (
        <nav>
            <button>Home</button>
            <button>Sobre</button>
            <button>Galeria</button>
        </nav>
    );
}

export default Navbar;
```

```jsx
// App.jsx

import React from 'react';
import Navbar from "./navbar.jsx";
function App() {

    return (
        <>
            <Navbar/>
        </>
    )
}

export default App
```

### Props: passando propriedades

Muitas vezes iremos nos deparar com um componente que precisa de um valor externo para que funcione corretamente. Vamos supor que temos um objeto definido no nosso _App.jsx_ que gostaríamos de mostrá-la utilizando um componente de _perfil._

Para fazer isso podemos criar um atributo que será responsável por repassar o valor do objeto com as propriedades que queremos mostrar.

```jsx
// app.jsx

import React from 'react';
import Perfil from "./perfil.jsx";

function App() {
    const obj = {
        nome: 'itallo',
        idade: 20,
        hobbie: 'Jogar'
    }

    return (
        <>
            <Perfil user={obj}/>
        </>
    )
}

export default App
```

Se você criar um componente com o auto-complete do editor, você vai perceber que ele vai adicionar na assinatura da função a variável `*props`.* Este `*props`* armazena todos os atributos passados anteriormente no documento pai. Com ele, podemos acessar - neste caso - o ‘_user_’ e, por ele ser um objeto, continuar com a notação de ponto até chegar na propriedade desejada.

```jsx
// perfil.jsx

import React from 'react';

function Perfil(props) {

    return (
        <div>
            <h1>Oi, eu sou o {props.user.nome}</h1>

            <p> Eu gosto de {props.user.hobbie}</p>
            <p>Eu tenho {props.user.idade} anos.</p>
        </div>
    );
}

export default Perfil;
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fd3ca3bd-cfe9-49c4-9ac3-2b0166c5929f/Untitled.png)

Uma das coisas muito comuns é desestruturarmos os valores de `*props`* na assinatura do componente para que possamos pegar seus valores sem ter que ficar usando notação de ponto.

```jsx
import React from 'react';

function Perfil({user}) {

    return (
        <div>
            <h1>Oi, eu sou o {user.nome}</h1>

            <p> Eu gosto de {user.hobbie}</p>
            <p>Eu tenho {user.idade} anos.</p>
        </div>
    );
}

export default Perfil;
```

Desta forma conseguimos um código mais limpo e simples de entender, com o mesmo resultado.

### Mostrando Vetores

Uma das funções mais comuns de serem utilizadas é o `*array.map`* já que ele executa um looping através de todos os elementos e retorna um vetor. Antes de entender o porquê, vamos dar uma olhada no que acontece quando retornamos um vetor diretamente:

```jsx
import React from 'react';

function Itens() {
    const frutas = ['banana', 'Amora', 'abacaxi']
    return (
        <div>
            <p>{frutas}</p>
        </div>
    );
}

export default Itens;
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/649b74fe-1559-404b-9311-5cb53b515c17/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1898a006-1abf-453c-8496-e7dbf54a48c6/Untitled.png)

Ele automaticamente faz o _looping_ em todos os elementos, porém coloca-os na mesma div, como se fosse um texto só. Pensando em resolver esse problema, o uso do `*map`* entra em ação. Com ele percorreremos todos os elementos adicionando-os na sua `*tag`* apropriada, resultando no fim um vetor de elementos com as informações encapsuladas. Vejamos:

```jsx
import React from 'react';

function Itens() {
    const frutas = ['banana', 'Amora', 'abacaxi']

    return (
        <ul>
            {frutas.map((fruta)=> <li>{fruta}</li>)}
        </ul>
    );
}

export default Itens;
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b050a167-54f2-4b56-8b45-1952d4c79163/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6a746e05-f3c9-4943-b76c-1b313cd40073/Untitled.png)

Agora, se formos verificar o console do navegador, iremos nos deparar com o React nos fazendo o seguinte alerta:

**“_Alerta: Cada elemento filho de uma lista deve ter uma chave única._**

_**Verifique o método de renderização de ‘Itens’.”**_

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/eeb5816a-3eeb-403d-89ff-91e074d9cc8d/Untitled.png)

Isso porque o React exige que cada elemento possua uma chave específica - seja em `*string`* ou em `*int*` - para que caso algo venha a ser modificado, ele saiba e possa renderizar o componente novamente. Não apenas isso, mas saiba renderizar os elementos específicos necessários que precisam ser atualizados, modificados ou deletados. A não utilização adequada de chaves em vetores pode causar eventuais bugs, ou fazer com que o app rode de forma lenta pela necessidade de renderizar uma grande quantidade de dado novamente desnecessariamente.

Linguagem: [[Front-end/React/React]]