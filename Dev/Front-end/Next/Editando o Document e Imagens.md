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
        <link rel="preconnect" href="<https://fonts.gstatic.com>" crossOrigin={"anonymous"}/>
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

<aside> 💡 Lembrando sempre que ao modificar informações do `*_document*` é necessário reiniciar o servidor.

</aside>

<aside> 💡 Caso as alterações não sejam aplicadas, exclua a pasta `*cache*` de dentro da pasta `.next`

</aside>

# Carregando estilos no Servidor

É muito comum em aplicações que não possuem SSR como vite, CRA e etc. que os estilos e outros elementos js sejam carregados para execução na parte do cliente.

Então caso tenhamos um styled componentes, stitches ou qualquer outra biblioteca dependente desse processo e desabilitarmos o JS no browser, nossa aplicação nem carregue.

O Next.js como ele monta tudo na parte do back-end, nossa aplicação ainda é mostrada mas a estilização não é carregada pois por padrão, o lado do cliente que é responsável por lidar com essa parte do processo de pegar a estilização feita pela biblioteca e injetar na nossa página.

Com `*stitches*` podemos resolver isso indicando ao next que ele deve ser carregado no servidor antes do envio da página. Isso faz com que nossa aplicação ganhe performance na parte do cliente e que o cliente sempre consiga visualizar o conteúdo da forma correta.

# _App

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

[Components: <Image>](https://nextjs.org/docs/app/api-reference/components/image)

Subtópico de: [[Next]]