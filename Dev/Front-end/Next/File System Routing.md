O Next nos provê um sistema de roteamento baseado em arquivos físicos. Isso quer dizer que, para que possamos carregar um componente baseado na rota da nossa aplicação, podemos colocar o nome da rota dentro da pasta `*pages`* de nossa aplicação.

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

# Next Link

Muito importante que utilizemos o componente de Link do próprio Next para que sejamos enviados de uma página à outra. Isso porque ao utilizar deste componente, todo o conteúdo previamente carregado permanecesse em cache, não sendo preciso que o next busque novamente essas informações, coisa que não acontece quando utilizamos uma tag `*a`* por exemplo.

Uma das coisas que tem que tomar cuidado é quanto ao `*prefetch*` de dados. O next entende que aquele é um link e que ele vai carregar uma possível nova rota com novas informações e isso faz com que ele faça um fetch para carregar essa possível página de forma mais rápida.

O problema é que se tivermos muitos links disponíveis na página, o Next vai fazer esse `*prefetch`* e isso pode ser muito custoso. Para desabilitar, basta utilizar a propriedade `*prefetch={false}*` .

Subtópico de: [[Next]]