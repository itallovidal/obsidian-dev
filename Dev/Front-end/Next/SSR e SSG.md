# SSR - Get Server Side Props

No desenvolvimento de aplicações com react é muito comum que peguemos informações de APIs. através do `*useEffect` .* Ao montarmos nosso componente fazemos um fetch na API e populamos um estado interno de algum componente.

O problema disso é, novamente, ao desabilitarmos o JS da página, hooks como useEffect ou qualquer outro pedaço de código que roda no lado do cliente não é executado e nós ficamos sem o fetch dos dados.

Com next, temos a possibilidade de rodar esses fetchs no lado do servidor. _Isso tem pontos positivos e negativos._

Ou seja, ao invés de fazermos o fetch no front-end dentro do componente, iremos fazer no backend e passar para o componente pelas suas props. Para isso teremos que utilizar uma função chamada `*GetServerSideProps` .*

Antes complicarmos as coisas, vamos ver a sintaxe básica:

```tsx
// intellisense
import { GetServerSideProps } from 'next'

export default function Home({names}: {names: string[]}) {
    return names.map((nome)=> <p>{nome}</p>)
}

export function getServerSideProps(): GetServerSideProps{
  return {
      props: {
          names: ['eu', 'ele', 'ela']
      }
  }
}
```

Note que: o retorno da função `*getServerSideProps*` **deve** ter `*props*` e ele **deve ser** um objeto com algum outro valor. No caso, as props são um conjunto de nomes.

A nossa `*home*` pega as props e desestrutrura pegando diretamente os nomes. A partir daí é código react comum.

## Problemas

A grande questão é que se tivermos uma chamada para API que demore muito tempo para acontecer, nosso usuário enfrentará uma tela em branco. Isso porque o Next só manda para o fronte end quando o conteúdo está pronto, e se uma promessa não foi resolvida, ele não pode enviar os componentes para o front.

Então devemos ter muito cuidado ao utilizar `*ServerSideProps` .* Geralmente iremos utilizá-lo quando queremos que bots e crawlers tenham acesso à determinadas informações assim que a página esteja pronta, ou que determinada chamada à API esteja invisível aos olhos do usuário final.

<aside> 💡 Lembrando que: Cada vez que uma requisição é feita para a rota com `*ServerSideProps*`, a função é disparada. Por conta disso podemos manipular a requisição, a resposta, os parâmetros da rota e por aí vai.

</aside>

# Static Server Generation (SSG)

## GetStaticProps

Uma das features mais interessantes do Next é o SSG. Com esse conceito podemos pegar conteúdos que não mudam com frequência na nossa aplicação e gerar uma página estática fazendo com que o carregamento seja hiper rápido - já que esse conteúdo foi uma vez já carregado. Por exemplo:

Vamos supor que temos um conjunto de produtos. Os produtos possuem fotos, descrição e etc. Ou seja, muitos produtos, muitas fotos, carregamento lento. Ao invés de fazermos toda vez que carregado a página um fetch para listagem dos produtos, podemos fazer o fetch uma vez a cada X tempo e nesse espaço de tempo termos os produtos cacheados pelo nosso servidor.

Isso diminui a demanda no banco de dados e faz com que os produtos sejam mostrados mais rápido no front. Esse processo possui pontos positivos e negativos. Vejamos:

Quanto à sintaxe:

```tsx
// intellisense
import { GetStaticProps } from 'next'

export default function Home({names}: {names: string[]}) {
    return names.map((nome)=> <p>{nome}</p>)
}

export function getStaticProps(): GetStaticProps{
  return {
      props: {
          names: ['eu', 'ele', 'ela']
      },
			revalidate: 60 * 60
  }
}
```

Podemos ver que a sintaxe é muito parecida, tendo apenas um `*revalidate*` que indica o intervalo de tempo de quando essa função precisa ser disparada novamente.

Nesse exemplo não faz diferença em performance, já que ele só mostra a questão de sintaxe, mas pensando em algo maior - como o exemplo dos produtos citado acima - é muito mais interessante utilizar `*StaticProps*` do que `*ServerSideProps` .*

Isso porque já que os produtos deverão ser visualizados por todos os clientes de forma igual, e é uma coisa que não muda com tanta frequência, você não precisa ter essas informações puxadas de um banco de dados à todo instante.

<aside> 💡 Lembrando que: A função `*GetStaticProps`* é rodada no momento da build e depois do intervalo indicado pelo _`revalidate`._

</aside>

<aside> 💡 O método `*GetStaticProps*` recebe também dois `*generics*`, sendo o primeiro o que ele vai retornar nas props e o segundo o tipo de parâmetro que ele recebe.

</aside>

## Problemas

O problema é que se tivermos muitos produtos, a nossa build tende a demorar mais para acontecer já que uma mesma - ou várias - página tem que ser gerada diversas vezes com várias informações diferentes. Então essa ferramenta tem que ser utilizada com muito cuidado, apenas em seções que exigem muita demanda. Como uma página que tem muitos acessos, os 5 produtos mais comprados, ou contextos parecidos.

## GetStaticPaths

Ao gerar páginas estáticas que possuem parâmetros dinâmicos, por padrão o Next precisa de uma outra função configurada chamada `*GetStaticPaths` .* Isso porque para carregar essa página, é preciso de uma informação a mais que vem pela rota - no nosso exemplo dos produtos, o ID.

Isso faz com que o Next não saiba exatamente o que carregar, pois no momento da build esse parâmetro não existe. Por isso precisamos utilizar o `*GetStaticPaths`,* com ele podemos definir se a página precisa ser gerada em build time ou não, e caso precise, quais páginas com quais informações. Ela devolve duas propriedades: `*paths*` e `*fallback` .*

`*Path`* indica quais parâmetros/informações são precisos para que a página seja gerada. Então por exemplo, precisamos que o produto com ID de 01 gere uma página com suas informações. Note que seria uma rota como `*/produtos/[id]` ,* então nos paths deveríamos dizer que os parâmetros são um ID com o valor X.

Ex.:

```tsx
export const getStaticPaths: GetStaticPaths<{ slug: string }> = async () => {

    return {
        paths: [{
					params: {
						id: 01	
					}
				}], 
        fallback: false 
    }
}
```

Isso fará com que para o produto de ID 01 tenha uma página estática com as suas informações.

## Problemas

Como dito anteriormente, a questão é que se você tiver 2000, 5000, ou até mesmo 50000 produtos, ele teria que gerar uma página estática para cada um e isso demoraria uma eternidade. Em ocasiões como essa, que não queremos que necessariamente todos os produtos sejam carregados, e sim talvez os que mais saem para ter uma experiência de compra mais otimizada, é que entra a propriedade `*fallback*` .

A propriedade `*fallback*` define o que o next deve fazer para o restante das páginas que devem ter o conteúdo carregado. Ela possui três possíveis valores: `*true*`, `*false*` e `*‘blocking’` .*

- Com o valor `*false*` a página simplesmente não irá carregar, dando erro 404, já que o ID em questão não foi passado nos paths.
- Com o valor `*true*` o next irá tentar gerar uma versão estática assim que a requisição for disparada na página. Ele vai mostrar a página mas sem conteúdo. Neste momento a função `*getStaticProps`* será disparada e fará as requisições necessárias em um processo assíncrono. Ao receber as informações, o componente atualizará.
- Com o valor de `*blocking*` o next só vai mostrar a tela quando estiver com todas as informações. Enquanto isso a tela ficará em branco.

<aside> 💡 Podemos acompanhar o status do `*fallback`* através da propriedade `*isFallback*` advinda do `*useRouter`* do Next.

</aside>

Subtópico de: [[Next]]