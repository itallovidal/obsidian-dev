# Contexto: Compartilhando Informações

## _**useContext**_

Imagine que você possui vários componentes, e você precisa que um estado ou função esteja disponível em todos eles. Passar como _props_ pode ser extremamente trabalhoso, além de fazer com que o código fique mais complexo de se entender.

Para resolver isso, o React nos disponibiliza um _**Hook de contexto**_. Com ele, criamos uma variável de contexto que será responsável por prover os valores que desejamos passar, e englobamos os componentes necessários com o contexto criado.

Vamos supor que temos dois componentes no nosso documento _app.jsx_. Um componente de barra de navegação e um componente chamado ‘content’, que é responsável por mostrar qual página foi clicada. Note que ao invés de passar como props duas vezes - uma em cada componente - nós passamos uma vez só através da tag de contexto.

```jsx
// app.jsx

import React from 'react';
import Navbar from "./navbar.jsx";
import Content from "./content.jsx";

// primeiro criamos um contexto
export const GlobalContext = React.createContext()

function App() {
    const [page, setPage] = React.useState(1)

    return (
				
				// chamamos esse contexto passando como valor as variáveis desejadas
        <GlobalContext.Provider value={{page, setPage}}>
            <Navbar/>
            <Content/>
        </GlobalContext.Provider>
    )
}

export default App
```

Lembrando que devemos usar _‘.Provider’_ obrigatoriamente para que o componente passe os valores desejados para seus componentes filhos. Agora, se formos ver na `*navbar*`, podemos acessar o _setter_ da seguinte forma:

```jsx
// navbar.jsx

import React from 'react';
// importando o contexto novamente
import {GlobalContext} from "./App.jsx";

function Navbar() {
		// utilizando o contexto e desestruturando o valor desejado
    const {setPage} = React.useContext(GlobalContext)

		// utilizando normalmente dentro do botão
    return (
        <nav>
						
            <button onClick={(e)=>setPage(e.target.textContent)}>Home</button>
            <button onClick={(e)=>setPage(e.target.textContent)}>Produtos</button>
        </nav>
    );
}

export default Navbar;
```

Importamos o contexto global, e o usamos dentro do Hook `*useContext` .* Desestruturamos esse contexto capturando apenas os valores que desejamos. Pronto, depois é só utilizarmos normalmente dentro do nosso componente.

Em nosso componente de conteúdo que mostra a página, a lógica é a mesma. Neste caso, para facilitar o entendimento, estamos apenas mostrando o índice da página, mas poderíamos mostrar um componente X ou um Y de acordo com nossa necessidade.

E o melhor: caso precisemos acessar nos componentes filhos de _navbar_ ou _content_ esses valores, basta importar o contexto que conseguiremos acesso. Usarmos `*useContext`* e entender seu funcionamento é vital para que possamos compartilhar estados e variáveis através de todo nosso aplicativo.

```jsx
// content.jsx

import React from 'react';
import {GlobalContext} from "./App.jsx";

function Content() {
    const {page} = React.useContext(GlobalContext)

    return <h1> Esta é a página {page}</h1>
}

export default Content;
```

Agora que já entendemos o funcionamento base do `*useContext` ,* podemos ver um método muito utilizado para deixar nosso código ainda mais limpo. O resultado é o mesmo, porém vamos tentar organizar melhor separando variáveis globais do resto do fluxo do _app.jsx._

Criaremos um documento à parte chamado _globalContext.jsx._ Nele, criaremos nosso contexto e as variáveis globais. Depois, criaremos um componente chamado `GlobalStorage` **e nele iremos retornar nosso contexto envolto do _{children},_ com os valores que queremos que o _children_ - ou seja, os componentes filhos - possam acessar.

Muito cuidado para não confundir os nomes.

```jsx
// GlobalContext.jsx

import React from 'react';

export const GlobalContext = React.createContext()

function GlobalStorage({children}) {
    const [page, setPage] = React.useState('')

    return (
        <GlobalContext.Provider value={{page, setPage}}>
            {children}
        </GlobalContext.Provider>
    )
}

export default GlobalStorage;
```

```jsx
// app.jsx

import React from 'react';
import Navbar from "./navbar.jsx";
import Content from "./content.jsx";

import {GlobalStorage} from "./globalContext.jsx";

function App() {

    return (
        <GlobalStorage>
            <Navbar/>
            <Content/>
        </GlobalStorage>
    )
}

export default App
```

Podemos perceber que o nosso App.jsx tem uma sintaxe mais limpa e fácil de entender, e as variáveis globais estão separadas em um documento apenas delas.

Linguagem: [[Front-end/React/React]]