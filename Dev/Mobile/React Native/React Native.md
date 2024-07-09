# Introdução ao React Native

### Configurando o Ambiente de Desenvolvimento

Para que possamos trabalhar e desenvolver aplicações com React Native primeiro devemos preparar nosso ambiente para que ele forneça todo o suporte necessário. Precisaremos de:

- Versão recente do Node:  
    [Node.js (nodejs.org)](https://nodejs.org/en)
- Versão recente do Android Studio para executarmos virtualmente:  
    [Desenvolvedores Android  |  Android Developers](https://developer.android.com/?hl=pt-br)

Para criar um projeto, podemos utilizar o comando:

```tsx
npx create-expo-app --template
```

Com ele aparecerá um prompt questionando qual template queremos utilizar, se é em branco com typescript ou se é com o template de navegação.

Assim que tudo estiver pronto, podemos dar abrir o servidor com o comando:

```tsx
npx expo start
```

Com ele nosso servidor será criado e poderemos abrir o app tanto no emulador quanto escaneando o QR Code, abrindo no nosso próprio celular utilizando o APP Expo GO. Incrível.

Para fazer uma verificação de todas as dependências podemos utilizar o comando:

```tsx
npx expo install --check
```

Pronto. Agora é só fazer as alterações e ver o app sendo modificado em tempo real.

# Componentes Importantes

A dinâmica de construção da aplicação muda um pouco em relação à WEB. Isso pois existem elementos específicos que precisamos utilizar para que depois seja traduzido para elementos nativos durante o processo de `*bundling*`.

Com isso em mente, veremos agora alguns componentes chave para utilizarmos em nosso desenvolvimento.

## `*<Text>*`

Responsável por receber e mostrar textos em tela. Deve envolver todo e qualquer texto, mesmo que ele apareça dentro de botões.

## `*<TextInput/>*`

Responsável por mostrar um input para que o usuário possa adicionar/alterar um valor.

**Propriedades importantes:**

- `*onchangeText*`: função disparada toda vez que o valor do input é alterado. Devolve um texto.

## `*<View>*`

Parecida com a `*<div>`* da web, envolve outros elementos para que seja mostrados em tela, ou seja, possui como papel ser um container/wrapper de outros componentes.

## `*<StatusBar/>*`

Componente responsável por representar a barra de notificações. Podemos alterar suas cores, seu fundo e seu comportamento.

Propriedades Importantes:

- `*BackgroundColor*` : Muda o fundo da barra.
- `*BarStyle*` : Altera a cor do texto/ícones da barra.
- `*Translucent*` : Define se a barra de notificações ficará em cima da aplicação ou se ela será empurrada para baixo. Valores booleanos.

# _Scroll View_ e _FlatList_: Diferenças

Para renderizar conteúdos onde se há uma barra de rolagem, temos duas opções de componentes para ser usado: `*FlatList*` e `*ScrollView*` . Apesar de servirem para o mesmo propósito, possuem uma execução um pouco diferente.

A `*ScrollView*` é basicamente um container com um overflow: scroll. Ou seja, ele renderiza todos os conteúdos e disponibiliza uma barra lateral para que possamos ver todos eles. O problema disso é que em uma lista de 30 itens, ao utilizarmos a `*ScrollView*`, serão carregados e renderizados os 30 itens, mesmo que em tela só apareçam no máximo 5 itens.

Já no caso da `*FlatList*` , o `*React*` renderizará a medida que precisarmos mostrar os elementos, ocorrendo um carregamento dinâmico.

Ou seja, a `*ScrollView*` é indicada para listas onde temos pouca quantidade e esses elementos são bem definidos. Já a `*FlatList*` é indicada para uso onde não sabemos quantos elementos iremos mostrar em tela. Isso fará com que nossa aplicação fique mais performática.

**Estrutura da `*ScrollView*`:**

Como podemos ver abaixo, usamos um map para devolver os elementos e o ScrollView envolverá eles mostrando uma barra de rolagem caso necessário.
```js
const vetor = ['texto 01', 'texto 02', 'texto 03'] 

<ScrollView> 
	  { 
		  vetor.map(item => <Text key={item}>{item}</Text>) 
	  } 
</ScrollView>
```

**Propriedades Interessantes:**

- `*showverticalscrollindicator*`: mostra ou oculta a barra.

**Estrutura da `*FlatList*`:**

Como podemos ver abaixo, sua estrutura se difere um pouco. Possui dois atributos obrigatórios: `*data*` ,`*renderItem*` , `*keyExtractor*` . O primeiro atributo é o vetor no qual a `*FlatList*` irá receber para manipular, o segundo atributo serve para definirmos o que será renderizado em cada item da lista fornecida, e o terceiro atributo é o valor que cada atributo irá receber.
```js
const vetor = [
	{ 
		id: 1, 
		content: 'texto 01' 
	}, 
	{ 
		id: 2, 
		content: 'texto 02' 
	}, 
	{ 
		id: 3, 
		content: 'texto 03' 
	}
]
	
	<FlatList data={vetor} 
			keyExtractor={item.id} 
			renderItem={({item})=> <Text>{item.content}</Text> }/>
```

**Propriedades interessantes:**

- **`*ListEmptyComponent*` :** renderiza um componente específico caso a lista não tenha nenhum item.
- **`*ListFooterComponent` : renderiza um componente específico no rodapé da lista.***
- **`*ListHeaderComponent` : renderiza um componente específico no cabeçalho da lista.***

Subtópico: [[Mobile]]