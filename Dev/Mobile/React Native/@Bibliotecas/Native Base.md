# Instalação

_focus

_pressed

Native base é uma biblioteca muito interessante que nos disponibiliza uma série de componentes pré-configurados para adiantar no desenvolvimento de nossa aplicação. Para que ele funcione corretamente devemos adicionar a dependencia do próprio native base, do react native svg para que nossa aplicação lide com ícones e o safe area context.

```jsx
npm install native-base
```

```jsx
npx expo install react-native-svg
```

```jsx
npx expo install react-native-safe-area-context
```

Depois de instalado precisamos envolver nossa aplicação com o componente `*NativeBaseProvider`* para que os outros componentes funcionem com a possibilidade do nosso tema ser aplicado.

# Criando um Tema

O native Base oferece um conjunto enorme de cores, tamanhos, e componentes pré definidos, mas podemos sobrescrever suas características para fazer nosso tema próprio.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/bb126ece-aa70-44f4-8a75-de1fb1663768/Untitled.png)

> Exemplos de cores pré definidas

Para isso é muito simples, basta passar um objeto de configuração utilizando uma propriedade fornecida pelo native base chamada `*extendTheme`.*

```jsx
export const THEME = extendTheme({
    colors: {
        green: {
            700: '#00875F',
            500: '#00B37E',
        }
		}})
```

Agora para que esta variável esteja disponível em toda aplicação, devemos passá-la no componente de contexto do native base, o `*NativeBaseProvider` .*

# Utilização de ícones Externos

Muitas vezes queremos utilizar ícones que estão na nossa máquina ou de uma biblioteca externa como a do `*phospor-icons*`, por exemplo. O problema disso é que nesses casos, esses componentes não são do `*native base*` e assim não aceitam determinados valores do nosso tema, por exemplo.

Ou seja, caso queiramos utilizar um ícone do `*phospor-icons*` mas passando um valor de cor do nosso tema, não irá funcionar, porque a biblioteca não possui nenhum “blue.600” por exemplo. Mas isso é facilmente contornável com o componente `*Icon*` do `*native base*` .

Com ele passamos qual ícone iremos utilizar na propriedade `*as*` e depois estilizamos normalmente como se fosse um ícone do `*native base.*`

```jsx
import {Icon} from "native-base";
	
// ícone externo
import {SignOut} from "phosphor-react-native";

<Icon
	as={SignOut} // passando o ícone externo
	size={32}
	color={"blue.600"}
/>
```

# Skeleton

Esse é um componente muito útil para quando queremos dar um feedback visual para o usuário de que o conteúdo que ele deseja visualizar está carregando. Com ele utilizamos um componente chamado `*Skeleton*` com o mesmo tamanho que o conteúdo a ser mostrado quando carregado.

Ao carregar o conteúdo, podemos passar um booleano para a sua propriedade `*isLoaded*` e ele irá renderizar o `*children*` passado. Por exemplo:

Vamos supor que queremos carregar uma foto de perfil. Essa foto pode demorar a carregar, então daremos um feedback visual mostrando que nosso aplicativo está no processo.

![Animação.gif](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/23d4b9b9-7d01-45a5-945f-a6e8743d6cb4/Animao.gif)

![Animação2.gif](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/2b3e0f6c-282d-4998-83b7-fd88b0afa3f7/Animao2.gif)

Para isso é muito simples:

```jsx
<Skeleton w={32}
          h={32}
          rounded={"full"}
          isLoaded={isPhotoLoaded} // estado que informará quando renderizar o filho
          startColor={"gray.300"} // podemos mudar as cores de comeco e fim!
          endColor={"gray.500"}>

          <UserPhoto size={32}
                     alt={""}
                     source={{uri: "<https://github.com/itallovidal.png>"}}
          />

</Skeleton>
```

> Dica: Para renderizar um `*skeleton*` de texto, use `*Skeleton.Text*`

# useToast

Esse é um hook que nos possibilita utilizar mensagens formatadas no padrão do celular. Geralmente como mensagens de feedback ou alerta, muito fácil de utilizar.

```jsx
const toast = useToast()
toast.show({
            title: "Ops, imagem muito grande!",
            placement: "top",
            bgColor:"red.500",
        })
```

# Botões

## `*<Pressable>*`

Componente que de toque sem feedback visual.

isPressed, _pressed

# Componentes de Layout

Componentes de layout são componentes que servem para organizar um grupo de componentes. Eles trazem configurações pré definidas para que estruturem visualmente nossa aplicação sem que tenhamos muito trabalho.

## `*<VStack>*`

Componente, como o nome sugere, que possui o intuito de dispor outros componentes _**um abaixo do outro.**_

## `*<HStack>*`

Componente, como o nome sugere, que possui o intuito de dispor outros componentes _**um ao lado do outro.**_

## `*<Center>*`

Componente que centraliza todo o conteúdo que está dentro dele.

## `*<Box>*`

Similar a div no HTML, a box é um componente wrapper simples sem estilização.


Subtópico: [[Bibliotecas RN]]