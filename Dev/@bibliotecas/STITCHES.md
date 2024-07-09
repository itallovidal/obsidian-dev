Stitches é uma biblioteca CSS-in-JS muito semelhante ao `*Styled Components`* mas que trabalha de uma forma melhor com o Next.js justamente por ter suporte a SSR. Além disso possui uma forma de manipulação de multi-estilos mais organizada.

# Instalação

```tsx
npm install @stitches/react
```

# Configuração e Tema

Com a função `*createStitches`* podemos configurar e personalizar nosso tema livremente. Para que possamos acessar essas configurações, devemos exportar alguns objetos que essa função retorna.

São muitos objetos, então iremos ir vendo à medida que for necessário. No momento, precisamos nos atentar aquele `*styled`* retornado pela função.

```tsx
// styles/index.ts
import { createStitches } from "@stitches/react";

export const { styled } = createStitches({
    theme: {
        colors: {
            white: '#fff',
						minhaCor: '#121214'
        } as const
    }
})
```

Com ele poderemos criar os componentes necessários para nossa aplicação.

# Criando um componente

Para criar um botão, por exemplo, utilizamos o `*styled*` exportado no documento `*/styles/index.ts*` - o documento acima - e criamos o botão passando para a função `*styled*` o tipo de tag e suas configurações.

Por exemplo:

```tsx
import { styled } from 'styles/index'

const Button = styled('button', {
	backgroundColor: 'blue'
})
```

Note que a estilização, diferente do Styled Components, é feita com um objeto JS. A configuração desse componente não é feita como se estivéssemos utilizando CSS diretamente, mas por um objeto javascript.

As nossas cores personalizadas são utilizadas colocando um sinal de `*$`* na frente da variável:

```tsx
import { styled } from 'styles/index'

const Button = styled('button', {
	backgroundColor: '$minhaCor' // #121214
})
```

# Encadeamento de Tags

Assim como no SCSS, podemos fazer o encadeamento de estilizações de forma muito simples. Ou seja, se tivermos uma `*div*` que tem um `*span*` e um `*p*`, podemos estilizarmos diretamente dentro da `*div*`.

```tsx
import { styled } from 'styles/index'

const Div = styled('div', {
	backgroundColor: '$minhaCor' // #121214

	span: {
		color: 'blue'	
	}

	p:{
		color: 'yellow'
	}
})

<div>
	<span>span</span>
	<p>paragrafo</p>
</div>

```

# Carregando estilos no Servidor

É muito comum em aplicações que não possuem SSR como vite, CRA e etc. que os estilos e outros elementos js sejam carregados para execução na parte do cliente.

Então caso tenhamos um styled componentes, stitches ou qualquer outra biblioteca dependente desse processo e desabilitarmos o JS no browser, nossa aplicação nem carregue.

O Next.js como ele monta tudo na parte do back-end, nossa aplicação ainda é mostrada mas a estilização não é carregada pois por padrão, o lado do cliente que é responsável por lidar com essa parte do processo de pegar a estilização feita pela biblioteca e injetar na nossa página.

Com `*stitches*` podemos resolver isso indicando ao next que ele deve ser carregado no servidor antes do envio da página. Isso faz com que nossa aplicação ganhe performance na parte do cliente e que o cliente sempre consiga visualizar o conteúdo da forma correta.

Para isso devemos ir no `*_document.tsx*` e acrescentar a seguinte linha no `*Head*` do documento:

```tsx
<style id={'stitches'} 
			 dangerouslySetInnerHTML={{__html: getCssText()}}/>
```

```tsx
// styles/index.ts
import { createStitches } from "@stitches/react";

export const { 
	styled, 
	getCssText
} = createStitches({
    theme: {
        colors: {
            white: '#fff',
						minhaCor: '#121214'
        } as const
    }
})
```

# Estilos Globais

```tsx
// styles/index.ts

import { createStitches } from "@stitches/react";

export const { 
	styled, 
	getCssText,
	globalCss
} = createStitches({
    theme: {
        colors: {
            white: '#fff',
						minhaCor: '#121214'
        } as const
    }
})
```

Para criar estilos que serão globais para nossa aplicação é muito simples, basta exportarmos uma função chamada `*globalCss*` e criar um objeto que recebe o retorno dela.

```tsx
export const globalStyles = globalCss({
    '*': {
        margin: 0,
        padding: 0,
        boxSizing: 'border-box'
    },

    '*:link, *:active':{
        textDecoration: 'none',
    },

    main:{
        opacity: 0,
        transform: 'translateY(100px)',
        animation: `${show} 500ms forwards`
    },

    body: {
        '-webkit-font-smoothing': 'antialiased',
        backgroundColor: '$gray900',
        color: '$gray100'
    },

    'body, input, textarea, button': {
        fontFamily: 'Roboto',
        fontWeight: 400
    },

    picture: {
        display: 'grid',
        placeItems: 'center',
        width: '100%',
        height: '100%',
        position: 'relative',

        img: {
            maxWidth: '100%',
            maxHeight: '100%',
        }
    }
})
```

Depois é só chamar no Wrapper da nossa aplicação.

node: [[Bibliotecas]]