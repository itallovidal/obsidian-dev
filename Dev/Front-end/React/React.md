# Introdução

### O que é e porquê usar?

React é uma biblioteca `*javascript*` focada em criar interfaces dinâmicas de maneira simples e rápida. Criada em 2011 pelo time do facebook, tinha como objetivo otimizar o tempo e a forma com que páginas dinâmicas eram escritas. Em 2015 seu código foi aberto à comunidade e desde então só se popularizou, sendo uma das frameworks mais prestigiadas pela comunidade front-end.

O intuito é quebrar o layout da página em diversos componentes e mostrá-los de maneira dinâmica dependendo da necessidade e das interações dentro da página. A grande maioria dos projetos react são escritos com uma linguagem chamada JSX, capaz de combinar tanto HTML quanto JS de uma forma muito mais intuitiva.

### JSX

Uma das principais diferenças entre JS e JSX é que o JSX é capaz de retornar e manipular tags HTML nativamente no seu código. Isso faz com que salvemos muito tempo na hora de criar toda uma interface, já que precisamos de menos codigo para tal. Há algumas diferenças entre o HTML usado nesta linguagem e o HTML puro, que veremos em breve.

Como dito anteriormente, um código react é constituído por vários componentes - trechos do código que representam determinada área da interface. Esses componentes são funções que retornam trechos em HTML, que são chamadas em uma funcão principal que constrói nossa aplicação.

```jsx
function Header()
{
    return (
        <>
            <h1>Olá, mundo!</h1>
            <p>Primeiro APP React.</p>
        </>
    )
}

function App(){
    return (
        <Header/>
    )
}
```

Como podemos ver, a funcão Header tem em sua assinatura uma letra maiúscula para indicar que essa funcão é um componente, e ela retorna trechos diretamente em HTML. Temos que ter um pequeno cuidado quanto a estrutura do retorno - como as tags vazias para indicar que é mais de um elemento retornado e o uso de parêntesis - mas de um modo geral é infinitamente mais rápido desta forma do que escrevendo em JS puro.

Esses componentes ficam disponíveis para nós como tags com nome do componente criado. Então “Header” é chamado como se fosse uma tag dentro da funcão principal App. Essa “tag” é uma funcão que vai retornar um trecho de código HTML com suas lógicas e particularidades e assim vamos montando nossa página.

Alguns atributos sofrem pequenas alterações para não temos conflito com palavras reservadas da própria linguagem, como é o caso por exemplo do atributo HTML for e class. Nesses casos eles são escritos levemente diferente, mas o resultado no navegador é o mesmo - já veremos o porquê.

```jsx
function Header()
{
    return (
        <>
            <h1 className={"show"}>Olá, mundo!</h1>
            <p>Primeiro APP React.</p>
        </>
        
    )
}

function InputSetup(){
    return (
        <>
            <label htmlFor={"nome"}> Nome: </label>
            <input id={"nome"}/>
        </>
    )
}

function App(){
    return (
        <>
            <Header/>
            <InputSetup/>
        </>
    )
}
```

`*Class`* vira ClassName e For vira htmlFor, justamente porque já temos uma palavra reservada for no JS para loopings e temos uma palavra reservada class para classes. Então de fato temos algumas diferencas tanto no JS quanto no HTML, mas são mudancas sutis.

### Montando o APP

Toda aplicacão `*React*`possui um root: uma div raiz onde o conteúdo é montado. Então devemos capturar esse root, indicar que ele será nossa raiz e renderizar o aplicativo nela, passando a funcão principal.

```html
<!--Tag raiz onde nossa aplicacão será montada-->
<main id="root"></main>
```

```jsx
// capturando nosso root
const container = document.querySelector('#root')

// criando o root usando o método creatRoot do react
const root = ReactDOM.createRoot(container)

// renderizando nosso conteúdo passando nossa funcão principal
root.render(<App/>)
```

Uma maneira mais rápida de estabelecer esse root é fazendo de uma vez só, o que é o que geralmente o pessoal faz.

```jsx
ReactDOM.createRoot(document.querySelector('#root')).render(<App/>)
```

### Ambiente Básico

JSX não é uma linguagem suportada nativamente no browser e isso indica que devemos compilar código de `*React*`para JS puro. Para que isso aconteça, devemos manter algumas configurações básicas para que esse processo ocorra. Por ora, como os estudos acabaram de começar, vamos configurar um ambiente básico:

Essas são as tags scripts que precisam ser importadas no nosso HTML para que os elementos do react possam funcionar corretamente.

```html
<!-- Header: -->
<!-- Carrega o React, React Dom e Babel -->
<script src="<https://unpkg.com/react@18/umd/react.development.js>"></script>
<script src="<https://unpkg.com/react-dom@18/umd/react-dom.development.js>"></script>

<!-- Don't use this in production: -->
<script src="<https://unpkg.com/@babel/standalone/babel.min.js>"></script>
```

Precisamos dizer que o tipo é JSX para que o babel - compilador de js - possa identificar o código e transformar ele em código que o navegador entenda.

```html
<!-- Final do Body: -->
<script type="text/jsx" src="./main.jsx"></script>
```

**Novamente:** Essa é a forma mais simples de fazer com que o código funcione. Estamos fazendo desta forma para que não precisemos os preocupar em criar um ambiente de desenvolvimento com documentos mais complexos desnecessariamente.

# Vite

### Introdução e Criação de Ambiente

Para criar nosso ambiente é muito simples. Precisamos dos seguintes comandos dentro da pasta que faremos nosso projeto:

```html
<!-- Cria um ambiente com configs básicas -->
npm create vite@latest .

<!-- Instala as dependências e cria um template de introducão -->
npm install

<!-- Inicia um servidor e atualiza o conteúdo modificado/criado -->
npm run dev
```

Dado essa instalação, diversos arquivos irão ser gerados - pastas, arquivos JS, HTML, JSON, svgs e etc. Muitos são arquivos e estruturas que servem justamente para construir a página de placeholder que dá boas vindas ao usuário quando se instala e configura o ambiente. Podemos ver abaixo:

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/06a3d251-611f-497d-9e38-6696fc72da7d/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8d8e4530-367d-4f63-9d98-a07f8e454e63/Untitled.png)

Vamos limpar essa pasta e deixar apenas o necessário para construirmos nossa aplicação. Os documentos base são:

```markdown
*- node_modules
- public
- src
  - App.jsx
  - main.jsx
- index.html
- package.json
- package-lock.json
//- vite.config.js*
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3c7af9dd-3aa8-48aa-9cdf-5f78603e7081/Untitled.png)

```jsx
// Main.jsx

import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.jsx'

ReactDOM.createRoot(document.getElementById('root')).render(
    <App />
)
```

```jsx
// App.jsx

import React from "react";

function App() {

  return (
    <>
        <div> Olá Mundo!</div>
    </>
  )
}

export default App
```

ESLINT

```jsx
module.exports = {
  env: {
    browser: true,
  },
  extends: [
    'eslint:recommended',
    'plugin:react/recommended',
    'plugin:react/jsx-runtime',
    'plugin:react-hooks/recommended',
  ],
  parserOptions: {
    ecmaVersion: 'latest',
    sourceType: 'module',
    ecmaFeatures: {
      jsx: true,
    },
  },
  settings: {
    react: {
      version: 'detect',
    },
  },
  plugins: ['react-refresh'],
  rules: {
    'react-refresh/only-export-components': 'off',
    'react/react-in-jsx-scope': 'off',
    'react/prop-types': 'off',
    'no-unsafe-finally': 'off',
    'no-unused-vars': 'off',
    'react/jsx-key': 'off',
  },
};
```

Linguagem: [[Javascript]]