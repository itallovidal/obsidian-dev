
Palavra Chave: [[Front-end/React/React]]
# Introdução
Next é um framework que utiliza do react para criações de aplicações WEB. Com ele, podemos ter uma série de ferramentas como bundling, compiling, sistema de rotas, SSR, cache de requisições, otimizações de imagens, de fontes, e muito mais. 

# Aplicações SPA

Em uma aplicação tradicional SPA - Single Page Application - nós basicamente temos um front end responsável por renderizar informações de maneira dinâmica de acordo com as ações do usuário. Nossa página está sempre atualizando seus componentes com novas informações advindas, geralmente, de uma API Rest.

Temos um cenário onde o front solicita uma determinada informação, como uma lista de usuários, e a API recebe essa solicitação, fica responsável por todo o processo da captura e devolução desses usuários, e retorna um JSON com eles para o front, que por sua vez renderiza essa informação na tela.

## Acessibilidade de Crawlers e bots

#### Primeiramente, o que são crawlers?

Crawlers são basicamente rastreadores da WEB. Eles servem para rastrear e indexar informações que estão na internet. Eles percorrem todos os links e páginas da web para categorizar e identificar os conteúdos. Eles rastreiam títulos, SEOs, imagens, videos, textos, links, metadados categorizando essas informações e verificando a velocidade e a frequência que essas informações são acessadas.

Essas informações são classificadas com palavras chaves junto com a relevância. O crawler mais famoso e importante que temos é o do google. Ele nos ajuda a encontrar o que desejamos ao pesquisar uma determinada informação na internet, fazendo a catalogação e o match do conteúdo pesquisado.

## SPAs são CSRs

O problema de SPAs tradicionais são que elas são Client Server Rendering - ou seja, renderizam do lado do cliente. Assim que a página é carregada, ela depende do JS enviado do servidor para que suas informações sejam mostradas dinamicamente, já que é o JS que faz o processo de interação. 

Caso acessemos uma páginas em React, por exemplo, desabilitando o JS, ela vai ficar estática, e não vai carregar todas as informações. A maioria dos Crawlers acessam nossa aplicação com o JS desativado para melhorar a performance, além de ter um timeout muito pequeno.   

# Next é SSR

Com o next esse processo muda um pouco. Se pensarmos, código React é basicamente Código JS. A grande sacada do Next é trazer esse código JS para ser renderizado do lado do servidor, em node. Ou seja, aplicações Next possuem uma camada intermediadora entre o front e o backend, tendo um servidor node capaz de gerar todo o código React para ser enviado pro front end.

Então com SPAs tradicionais teríamos nosso site carregando a medida que os arquivos chegassem na máquina do cliente, e caso o JS necessário para fazer a requisição de uma determinada informação demorasse, ou acessássemos a página com o JS desabilitado, aquela informação não iria aparecer. 

Com Next, todo o conteúdo é renderizado no servidor, o que é muito mais rápido do que renderizar do lado do cliente. Então quando o cliente recebe a página, ele já recebe ela toda pronta. Além disso, mesmo com o JS desabilitado, a página ainda é mostrada da maneira correta, já com as informações, pois o conteúdo já foi previamente carregado pelo servidor.


![[Pasted image 20240731222024.png]]

# SSG - Static Site Generation

Hoje o desenvolvimento com next nos fornece uma série de funcionalidades e ferramentas que otimizam nossa aplicação, as quais estarão espalhadas nos outros documentos relacionados.

Um dos conceitos muito interessantes é o SSG. Com ele, podemos gerar uma determinada página ou um conjunto de páginas em Build Time. Para páginas que não possuem um conteúdo dinâmico muito latente, o uso de SSGs otimiza a performance e a usabilidade pelo usuário, já que as páginas são carregadas muito mais rápidas e são cacheadas para serem devolvidas em cada requisição.

Por exemplo, em um cenário onde o front end precisa mostrar um determinado conteúdo na tela advindo de um banco de dados, em uma aplicação sem SSG, cada vez que a tela for carregada terá uma chamada ao banco de dados. Mesmo que as informações sejam as mesmas. Mesmo se eu acabei de carregar essas informações, se eu fizer uma nova requisição para carregar a página esse processo de busca no banco de dados ocorre.

Com SSG ativo,  podemos fazer com que o Next faça uma única requisição pro banco/api de X em X tempos, e nesse intervalo, ter um cache dessas informações devolvendo para quem quer que se conecte com nossa aplicação acessar a página com as informações cacheadas.

# Instalação e Config

```jsx
npx create-next-app@latest
```

```jsx
//tsconfig
"moduleResolution": "node",
```
![[Pasted image 20240722210504.png]]
# File System Routing

O Next nos provê um sistema de roteamento baseado em arquivos físicos. Isso quer dizer que, para que possamos carregar um componente baseado na rota da nossa aplicação, podemos colocar o nome da rota dentro da pasta `pages` de nossa aplicação.

Ou seja, vamos supor que temos uma rota `*products*` que vai carregar um componente que lista todos os produtos. Nossa estrutura será:

```
/src
	/pages
		_app.tsx
		index.tsx
		products.tsx
		
```

O que é muito comum é termos pastas que representam uma rota. Neste caso a rota terá o nome da página e o arquivo de dentro será ou a subrota ou o seu índice.

Por exemplo, ao invés de termos diretamente um arquivo `*products` ,* teremos uma pasta e dentro dela teremos um `*index.`*

```
/src
	/pages
		_app.tsx
		index.tsx
		/products
			index.tsx
		
```

Nesse caso, assim como o `*index.tsx`* do root é a página principal - no caso a `*home*` - o `*index*` de dentro da pasta `*products*` representa a página principal desta rota.

# Rotas Parametrizadas

Para conseguirmos estabelecer rotas parametrizadas é muito simples. Para isso, basta utilizarmos `*colchetes + o parâmetro da rota` .* Vamos supor que ao invés de listar todos os produtos nessa rota nós queremos mostrar um produto em específico.

Naturalmente essa rota receberia um parâmetro como o `*id*` para que pudéssemos carregar suas informações. Para fazermos isso, nosso sistema de arquivos ficaria da seguinte forma:

```
/src
	/pages
		_app.tsx
		index.tsx
		/products
			[id].tsx
		
```

## Capturando os parâmetros

Para capturar os parâmetros é muito simples. Basta usarmos um `*hook*` que nos devolve essa informação chamado `useRouter`

```tsx
import { useRouter } from 'next/router'

function Product({product} : ProductProps) {
  const { query } = useRouter()
	console.log(query)  

	return(
			...
    )
}
```

# Editando o Document

No next o sistema de componentização é levado ainda mais a sério. Tudo é componente, inclusive nosso arquivo `*Document*`. Para que possamos editá-lo, adicionando fontes personalizadas, editando o cabeçalho ou qualquer outra coisa do tipo, devemos criar em nosso `*src*` um arquivo chamado `*_document.tsx*` .

Ele será responsável por dizer ao Next que as configurações daquele componente deverão ser aplicadas ao cabeçalho da página. Para isso, iremos criar um componente que irá utilizar de uma série de tags especiais do next para que possamos aplicar nossas configuração.

Vejamos como podemos aplicar fontes personalizadas.

```tsx
import { Html, Head} from 'next/document'

export default function Document() {
  return (
		// atenção às tags vindas do next/document
    <Html lang="en">
      <Head>
        <link rel="preconnect" href="<https://fonts.googleapis.com>"/>
        <link rel="preconnect" href="<https://fonts.gstatic.com>"      crossOrigin={"anonymous"}/>
        <link href="<https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,400;0,700;1,400;1,700&display=swap>" rel="stylesheet"/>
      </Head>
      <body>
      </body>
    </Html>
  )
}

```

Como podemos ver, utilizamos tags do next como `*Html*` e `*Head*` , colocando o link das fontes dentro do `*Head`* como faríamos em um arquivo comum.

Uma segunda etapa que precisamos concluir é adicionar uma tag especial chamada `*Main*` . Nela podemos informar ao Next onde nossa aplicação será renderizada. Ela atua de maneira muito semelhante à tag `*<div id='root' >`* do vite.

Além disso para carregarmos os scripts da nossa aplicação devemos utilizar uma tag especial chamada `*NextScript*` . Nosso arquivo ficará assim:

```tsx
import { Html, Head, Main, NextScript } from 'next/document'

export default function Document() {
  return (
    <Html lang="en">
      <Head>
        <link rel="preconnect" href="<https://fonts.googleapis.com>"/>
        <link rel="preconnect" href="<https://fonts.gstatic.com>" crossOrigin={"anonymous"}/>
        <link href="<https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,400;0,700;1,400;1,700&display=swap>" rel="stylesheet"/>
      <body>

        <Main />
        <NextScript />

      </body>
    </Html>
  )
}

```


> [!NOTE] 💡Obs.:
>  Lembrando sempre que ao modificar informações do `*_document*` é necessário reiniciar o servidor.

> [!NOTE] 💡OBS.:
> Caso as alterações não sejam aplicadas, exclua a pasta `*cache*` de dentro da pasta `.next`

# Carregando estilos no Servidor

É muito comum em aplicações que não possuem SSR como vite, CRA e etc. que os estilos e outros elementos js sejam carregados para execução na parte do cliente.

Então caso tenhamos um styled componentes, stitches ou qualquer outra biblioteca dependente desse processo e desabilitarmos o JS no browser, nossa aplicação nem carregue.

O Next.js como ele monta tudo na parte do back-end, nossa aplicação ainda é mostrada mas a estilização não é carregada pois por padrão, o lado do cliente que é responsável por lidar com essa parte do processo de pegar a estilização feita pela biblioteca e injetar na nossa página.

Com `*stitches*` podemos resolver isso indicando ao next que ele deve ser carregado no servidor antes do envio da página. Isso faz com que nossa aplicação ganhe performance na parte do cliente e que o cliente sempre consiga visualizar o conteúdo da forma correta.

#  _ _App
Este arquivo serve como Wrapper da nossa aplicação. Ele será carregado em qualquer página, já que ele engloba nosso componente.

Nosso componente é representado pelo `*Component*` ali, embaixo

```tsx
export default function App({ Component, pageProps }: AppProps) {
  
return (
    		<Component {...pageProps} />
    )
}
```

# Lidando com Imagens

O carregamento de imagens sempre é um problema, seja pela demora ocasionada pelo formato do arquivo ou pela imagem estar desnecessariamente grande.

O next nos fornece uma série de ferramentas interessantes para lidar com esse problema. Ele consegue fazer o redimensionamento das imagens, e mudar seu formato para otimizar a performance do carregamento, por exemplo.

Para isso, devemos utilizar um componente próprio do Next chamado `*Image` .* Existem muitas configurações interessantes como qualidade da imagem, media query para melhor otimização do tamanho, troca de formato e etc.. A lista de configurações pode ser encontra aqui:
https://nextjs.org/docs/app/building-your-application/optimizing/images

# Next Link

Muito importante que utilizemos o componente de Link do próprio Next para que sejamos enviados de uma página à outra. Isso porque ao utilizar deste componente, todo o conteúdo previamente carregado permanecesse em cache, não sendo preciso que o next busque novamente essas informações, coisa que não acontece quando utilizamos uma tag `*a`* por exemplo.

Uma das coisas que tem que tomar cuidado é quanto ao `*prefetch*` de dados. O next entende que aquele é um link e que ele vai carregar uma possível nova rota com novas informações e isso faz com que ele faça um fetch para carregar essa possível página de forma mais rápida.

O problema é que se tivermos muitos links disponíveis na página, o Next vai fazer esse `*prefetch`* e isso pode ser muito custoso. Para desabilitar, basta utilizar a propriedade `*prefetch={false}*` .

# API Routes

Muitas vezes no desenvolvimento da nossa aplicação, para juntar, manipular e preparar dados para nossa aplicação frontend, nos vemos na necessidade de criar uma API para lidar com esses processos, tendo duas aplicações trabalhando em conjunto.

Para contextos mais simples, o next possui uma feature chamada API Routes, que nos fornece a possibilidade da criação de uma API RESTful, eliminando a necessidade da criação de uma segunda base de códigos para esses tipos de processos.

O processo é muito parecido com o desenvolvimento de API com `*fastify*` ou `*express*`. Para todo conteúdo dentro da pasta `*/pages/**api` ,*** o next cria um endpoint para que possamos utilizá-lo.

```tsx
import {NextApiRequest, NextApiResponse} from "next";

export default async function handler(req: NextApiRequest, res: NextApiResponse){

		// fazer alguma coisa

    return res.status(201).json({
        message: 'Olá mundo!'
    })
}
```

<aside> 💡 Atenção: O next não faz diferenciação de método HTTP. Independente do método chamado, se a rota for passada corretamente a função será disparada.

</aside>

<aside> 💡 Atenção: essa função deve ser exportada com `*export default*`

</aside>

# Page Extensions

Podemos modificar quais extensões o next irá entender que são rotas através das pages extensions. É um vetor que configuramos no next.config.mjs
```tsx
/** @type {import('next').NextConfig} */
const nextConfig = {
  reactStrictMode: true,
  pageExtensions :[
      "page.tsx", "api.ts", "api.tsx"
  ]
};

export default nextConfig;
```