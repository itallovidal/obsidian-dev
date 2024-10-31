
Rotas são os caminhos dentro da nossa aplicação que irá nos levar para determinada página para mostrar um certo conteúdo. Um dos principais motivos pela utilização do React, como já comentado, é para realizar aplicações de página única (SPA). Com a extensão _react-router-DOM_, esse objetivo fica mais simples de ser atingido.

Para que possamos instalar, usamos o seguinte comando:

```jsx
npm install react-router-dom
```

Página de documentação: [Home v6.13.0 | React Router](https://reactrouter.com/en/main)

### Primeiros Passos

Este _plugin_ nos dá acesso à um objeto com diversas funções e componentes. Por ora, temos que entender os seguintes componentes:

- `*BrowserRouter*`
- `*Routes*`
- `*Route*`

O componente `*BrowserRouter*` é responsável por envolver todas as rotas de nosso aplicativo junto com outros componentes. Geralmente usado na camada mais externa do nosso aplicativo.

O componente `*Routes`* é responsável por envolver um conjunto de rotas do nosso aplicativo. Ele que indica o local específico no código que vai receber as rotas.

O componente `*Route*` é responsável por indicar qual rota carrega/direciona para qual elemento (componente).

Vamos ver um exemplo para que o uso dos componentes importados faça mais sentido.

```jsx
// primeiro importamos os componentes do plugin
import {BrowserRouter, Routes, Route} from "react-router-dom";

// aqui importamos nossas páginas e nossa navbar
import Home from "./home.jsx";
import Sobre from "./sobre.jsx";
import Nav from "./nav.jsx";

function App() {

    return (
				// envolvemos nosso aplicativo com o BrowserRouter
        <BrowserRouter>
						// nossa nav se manté imutável
            <Nav/>
						// espaco para nossas rotas
            <Routes>
                <Route path='/' element={<Home/>}/>
                <Route path='sobre' element={<Sobre/>}/>
            </Routes>
        </BrowserRouter>
    )
}

export default App
```

O código acima mostra um um _webapp_ com duas páginas: `*Home*`e `*Sobre*`. São dois componentes simples com um `*h1`* que mostra o nome da página.

```jsx
const Home = () => {
    return (
        <main>
            <h1>Essa é a página home!</h1>
        </main>
    );
};

export default Home;
```

Repare que o `*Route*`possui dois atributos: um path e um `*element*`. O primeiro deles indica qual caminho deve ser indicado na _URL_ do site e o segundo atributo é qual elemento/componente deve ser renderizado.

Note que o `*path*` da `*Home*`está com uma barra: isso acontece pois o home é a página inicial da nossa aplicação. Sendo assim, podemos substituir esse atributo pelo atributo index para que fique ainda mais intuitivo.

```jsx
function App() {

    return (
        <BrowserRouter>
						<Nav/>
            <Routes>
                <Route index element={<Home/>}/>
                <Route path='sobre' element={<Sobre/>}/>
            </Routes>
        </BrowserRouter>
    )
}
```

### Mudando a Página: Link e NavLink

Agora que nossas rotas foram estabelecidas, precisamos de uma forma para efetivamente mudar a página. Para isso, temos dois componentes à nossa disposição: `*Link*`, `*NavLink*`.

```jsx
// nav.jsx

// importando os componentes
import {Link, NavLink} from "react-router-dom";

function Nav() {
    return (
        <div>
            <Link to='/'>Home</Link>
            <NavLink to='sobre'>Sobre</NavLink>
        </div>
    );
}

export default Nav;
```

Ambos componentes servem para enviar o usuário para uma determinada _URL_. Devemos utilizar o atributo `*to*` para indicar o caminho desejado, e assim, carregar o componente referente à ele. Adicionando um css básico a nossa navegação ficará assim:

![uou.gif](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/494503cf-71b5-4fe3-86de-e241e93713c1/uou.gif)

A diferença entre o `*navlink*` e o `*nav*` é que o `*navlink*` indica qual link está ativo quando é clicado, adicionando uma classe `*.active*` no elemento, muito útil para que possamos estilizar caso necessário.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b82bb9ae-578e-422f-96c6-408b5d1566ac/Untitled.png)

### Redirecionamento com useNavigate

Vamos supor que ao invés de mudarmos de página assim que clicarmos no botão - que neste caso acima é um link (a) - nós queiramos realizar alguma tarefa como de login e depois redirecionar o usuário para uma página.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/632f707c-0b63-453e-9714-45b3fa429532/Untitled.png)

```jsx
function App() {

    return (
        <BrowserRouter>
            <Routes>
                <Route index element={<Home/>}/>
                <Route path='perfil' element={<Perfil/>}/>
            </Routes>
        </BrowserRouter>
    )
}
```

```jsx
// home.jsx

// importando o useNavegate do react router
import {useNavigate} from "react-router-dom";

const Home = () => {
		// usando o hook importado
    const navigate = useNavigate()

    function login(){
        console.log('Fazendo login..')
        console.log('Logado.')
				// passando o caminho desejado
        navigate('/perfil')
    }

    return (
        <main>
            <button onClick={login}>Fazer login</button>
        </main>
    );
};
```

### Rotas Dinâmicas: Utilizando useParams

Muitas vezes precisaremos que nossas rotas seja dinâmicas pois elas irão mudam dependendo da necessidade da aplicação. Por exemplo, vamos supor que temos um site que possui diversas categorias de produtos.

Neste caso, podemos usar dois pontos `*:*` + o indicador do nome para montar uma rota dinâmica. Por exemplo, em um site que temos a categoria de roupas, eletrônicos e acessórios.

```jsx
// home.jsx
function Home(props) {
    return (
        <div>
            <h1>Você está na home</h1>
            <Link to={'/produtos/acessorios'}>Acessórios</Link>
            <br/>
            <Link to={'/produtos/eletronicos'}>Eletrônicos</Link>
            <br/>
            <Link to={'/produtos/roupas'}>Roupas</Link>
        </div>
    );
}
```

```jsx
function App() {
    return (
        <BrowserRouter>
            <Routes>
                <Route index element={<Home/>}/>
								// utilizando o id de 'categoria'
                <Route path='/produtos/:categoria' element={<Produtos/>}/>
            </Routes>
        </BrowserRouter>
    )
}
```

Neste caso, o “:categoria” irá ser substituído por _acessórios_, _eletrônicos_ ou roupas, como o nosso link do componente home indica. O bom de darmos um id neste caso, é que podemos capturar informações da rota de maneira mais fácil e intuitiva com o `*useParams*`, hook que o react router também disponibiliza.

```jsx
import React from 'react';
import {useParams} from "react-router-dom";

function Produtos() {
    const rota = useParams()
		// vamos mostrar no console o que este hook devolve
    console.log(rota)

    return (
        <div>Esta é a página de produtos</div>
    );
}

export default Produtos;
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dcbb802c-8305-4162-897f-7d87f3796fc6/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/08153285-4141-401f-bab8-3900d22c71a8/Untitled.png)

Com essa informação, poderíamos fazer um fetch ou levar o usuário até uma parte específica da página.

### Mais Informações com useLocation

```jsx
const location = useLocation()
```

Um outro hook bem interessante que nos proporciona informações mais variadas da rota é o `*useLocation*`. Com ele podemos acessar:

- Pathname
- hash
- state
- key
- search *

Para nós, por enquanto, é interessante ver o `*pathname*`, que seria o caminho da rota e o `*search*`. Geralmente quando vamos consultar no banco de dados através de um `*POST*` nossa URL possui um sinal `*?nome=valor&nome=valor*` . Por exemplo: Vamos supor que queremos pesquisar todos os celulares que tiverem a cor azul.

A url se pareceria mais ou menos assim:

> /produtos/eletronicos?subcategoria=celulares&cor=azul

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7529b82d-9e3e-43bf-b63f-0b83b4c11c11/Untitled.png)

Para pegarmos os valores de forma ‘limpa’ podemos utilizar uma função em JS que formata URL para nós, exigindo que passemos apenas a chave do valor.

```jsx
const location = useLocation()

const params = new URLSearchParams(location.search)
console.log(params.get('cor')) // azul
console.log(params.get('subcategoria')) // celulares
```

### Rotas Aninhadas

Vamos supor que ao carregar a página de produtos, você queira mostrar uma parte que mostra os comentários e, ao mudar na barra de navegação, mostre a descrição do produto. Essa visualização só ocorrerá na página de produtos, sendo uma roda aninhada de produtos. Ou seja, ficará:

**/produtos/acessorios/** (não mostrando nada)

**/produtos/acessorios/comentarios**(mostrando os comentários)

**/produtos/acessorios/descricao** (mostrando a descrição)

Para isso, chamaremos nosso componente responsável por separar a parte da aplicação específica para rotas - o `*Router`* - e indicaremos as rotas e seus caminhos dentro dele.

```jsx
function Produtos() {
    const params = useParams()

    return (
        <>
            <h1>Esta é a página de produtos</h1>
            <p>Produto Selecionado: {params.categoria}</p>

            <nav>
								<Link to={'comentarios'}>Comentários</Link>
                <Link to={'descricao'}>Descrição</Link>
            </nav>

            <Routes>
                <Route path='comentarios' element={<Comentarios/>}/>
                <Route path='descricao' element={<Descricao/>}/>
            </Routes>

        </>
    );
}
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/42f15dfd-6753-4689-acfa-a7b12179ef68/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cdbc21e6-64d5-40f1-b2dc-88541cb54c9a/Untitled.png)

![uouo12.gif](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/17292a3d-6117-4037-8948-00ddee0447d4/uouo12.gif)

Acabamos de criar uma rota dentro de uma outra rota. Um ponto importante a enfatizar é que para que o código acima dê certo, devemos alterar a rota que nos leva a ele/

```jsx
// app.jsx antes

function App() 
    return (
        <BrowserRouter>
            <Routes>
                <Route index element={<Home/>}/>
                <Route path='/produtos/:categoria' element={<Produtos/>}/>
            </Routes>
        </BrowserRouter>
    )
}
```

```jsx
// app.jsx depois

function App() 
    return (
        <BrowserRouter>
            <Routes>
                <Route index element={<Home/>}/>
																							    |
																									V alteração
                <Route path='/produtos/:categoria/*' element={<Produtos/>}/>
            </Routes>
        </BrowserRouter>
    )
}
```

### O asterisco

Vamos revisar: acima estamos criando um componente `*BrowserRouter`* que engloba todo nosso aplicativo já que ele terá rotas navegáveis. Dentro dele temos um componente dizendo que aquela parte é dedicada à veiculação de rotas, e dentro dele temos nossas rotas - uma para página inicial e uma para página de produtos.

A página de produtos está com um caminho que indica que é uma rota dinâmica já que ela possui um identificador nomeado ‘categoria’ que vem logo depois do sinal de :.

Dito isso, dentro da página de categorias temos um aninhamento de rotas fazendo com que dependendo do caminho mostre comentários ou descrições. Note que para que o elemento `*<Produtos/>*` seja renderizado o caminho deve ser **/produtos/roupas**- por exemplo.

Caso naveguemos dentro de celulares e cliquemos no campo de comentários, a rota passará a ser **/produtos/produtos/comentarios.** Deixando o código sem o asterisco **neste caso**, fará com que a página não seja mostrada.

_**Por que?**_

Simples, porque ela só será mostrada única e exclusivamente se o caminho der match com o passado na rota externa. Para resolver esse problema devemos adicionar o asterisco, pois com ele indica para o componente route que a rota será **/produtos/roupas/qualquer-outra-coisa.**

### 404: Usando o `***`

Uma das coisas que podemos fazer com o asterisco é mostrar uma página de erro caso a url não exista.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b2e2a807-cb93-4244-94f9-ff24a26125ea/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/90e92a28-2191-4a3d-b028-cf08b8a116a3/Untitled.png)

```jsx
function App() {
    return (
        <BrowserRouter>
            <Routes>
                <Route index element={<Home/>}/>
                <Route path='/produtos/:categoria/*' element={<Produtos/>}/>
									
									Ou seja, qualquer coisa que não seja 
									nenhum dos caminhos de cima
                <Route path='*' element={<Error/>}/>
            </Routes>
        </BrowserRouter>
    )
}
```

## Rotas: segundo approach

`*todo*`

Linguagem: [[Front-end/React/React]]