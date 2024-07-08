Para renderizar conteúdos onde se há uma barra de rolagem, temos duas opções de componentes para ser usado: `*FlatList*` e `*ScrollView*` . Apesar de servirem para o mesmo propósito, possuem uma execução um pouco diferente.

A `*ScrollView*` é basicamente um container com um overflow: scroll. Ou seja, ele renderiza todos os conteúdos e disponibiliza uma barra lateral para que possamos ver todos eles. O problema disso é que em uma lista de 30 itens, ao utilizarmos a `*ScrollView*`, serão carregados e renderizados os 30 itens, mesmo que em tela só apareçam no máximo 5 itens.

Já no caso da `*FlatList*` , o `*React*` renderizará a medida que precisarmos mostrar os elementos, ocorrendo um carregamento dinâmico.

Ou seja, a `*ScrollView*` é indicada para listas onde temos pouca quantidade e esses elementos são bem definidos. Já a `*FlatList*` é indicada para uso onde não sabemos quantos elementos iremos mostrar em tela. Isso fará com que nossa aplicação fique mais performática.

**Estrutura da `*ScrollView*`:**

Como podemos ver abaixo, usamos um map para devolver os elementos e o ScrollView envolverá eles mostrando uma barra de rolagem caso necessário.

```jsx
const vetor = ['texto 01', 'texto  02', 'texto 03']

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

```jsx
const vetor = [{
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
},

<FlatList data={vetor}
					keyExtractor={item.id}
					renderItem={({item})=> <Text>{item.content}</Text> }/>
```

**Propriedades interessantes:**

- **`*ListEmptyComponent*` :** renderiza um componente específico caso a lista não tenha nenhum item.
- **`*ListFooterComponent` : renderiza um componente específico no rodapé da lista.***
- **`*ListHeaderComponent` : renderiza um componente específico no cabeçalho da lista.***

# Section List

Componente voltado para fazer agrupamento de informações. Ele possui uma estrutura de informações predefinida, ou seja, o objeto enviado para este componente deve ser:

- Um vetor de objetos
- Cada objeto deve ter obrigatoriamente:
    - `*title*`: responsável por entitular a seção
    - `*data*`: um vetor de informações

Abaixo colocaremos essas informações em um estado:

```jsx
const [cardapio, setCardapio] = React.useState([{
        title: "comidas",
        data: ["feijão", "arroz", "macarrão"]
    }, {
        title: "bebidas",
        data: ["coca", "agua", "suco"]
    }])
```

```jsx
				     // propriedade que recebe infos
<SectionList sections={cardapio} 
             keyExtractor={(item)=> item}

             // componente renderizado para cada item
             renderItem={()=> <Card/>} 

						 // compoente renderizado para cada cabecalho
             renderSectionHeader={({section})=> <Heading color={"white"}>{section.title}</Heading>}
            />
```

Vale notar que o `*renderSectionHeader*` desestrutura uma propriedade chamada `*section*` , é nela onde fica guardado internamente as informações passadas, por isso nós escrevemos `*section.title*` dentro do `*Heading`* renderizado.


Subtópico: [[React Native]]