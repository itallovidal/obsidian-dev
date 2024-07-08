O react Navigation é uma biblioteca responsável por lidar com navegação entre as telas. Temos três principais tipos de navegação:

- Stack Navigation
- Drawer Navigation
- Tab Navigation

Cada navegação será abordada com seus exemplos e seus cuidados.

### Instalação Base

Para usarmos seja o modelo que for, precisamos instalar o react Navigation. Sua instalação acompanha mais duas bibliotecas: `*react-native-screens*` e `*react-native-safe-area-context*`

```jsx
npm install @react-navigation/native
```

```jsx
npx expo install react-native-screens react-native-safe-area-context
```

### Stack Navigation

A Stack Navigation é a navegacão baseada em pilhas, ou seja, as páginas são empilhadas umas em cima das outras, e caso nós precisemos voltar a página elas serão descartadas para mostrar uma página anterior. Podemos animar esse empilhamento de várias formas de maneira default, mas abordaremos isso em breve.

Com a navegação base feita, podemos instalar a parte da lib específica para o modelo de navegacão que desejamos.

```jsx
npm install @react-navigation/native-stack
```

O `*React-Navigation*` se parece muito com o `*react router dom*` da web, tendo alguns componentes com nomes diferentes. Apesar disso, veremos que a ideia é muito parecida, e alguns componentes parecem fazer a mesma coisa.

Com tudo instalado teremos acesso a uma funcão chamada `*createNativeStackNavigator().*` Essa funcão nos devolve, principalmente, um componente chamado `*Navigator*` e outro chamado `*Screen*`.

A lógica é: _vou criar um componente de navegação e dentro dele vou adicionar todas as minhas telas._ Para ficar mais organizado podemos criar um componentes chamado `*AppRoutes*` que vai ser responsável por exportar todas essas rotas.

O componente `*screen*` recebe o nome da rota, seu elemento e seus parâmetro caso desejarmos passar alguma informação pelo contexto da rota.

```jsx
import React from 'react';
import {createNativeStackNavigator} from "@react-navigation/native-stack";
import Home from "../Screens/Home/Home";

const {Navigator, Screen} = createNativeStackNavigator()
function AppRoutes() {
    return (
        <Navigator>
            <Screen name={'home'} component={Home}/>
        </Navigator>
    );
}

export default AppRoutes;
```

Agora precisamos ir no app - ou em um componente à parte - e definir o `*NavigationContainer*` e chamar nossas rotas:

```jsx
import {NavigationContainer} from "@react-navigation/native";
import AppRoutes from "./src/routes/AppRoutes";

export default function App() {
    return (
        <NavigationContainer>
            <AppRoutes/>
        </NavigationContainer>
    )
}
```

Se formos reparar, tanto a navegação web quanto a mobile é muito parecida. Obviamente possui suas particularidades, porém em termos de estrutura base e lógica é muito parecido. Então se você pegou bem os conceitos da WEB, no `*React Native*` não terá muitas dificuldades de adaptação.

```jsx
// com react navigation
export default function App() {
    return (
        <NavigationContainer>
          <Navigator>
						// lembrando que no component devemos 
						// passar o componente como variavel
	          <Screen name={'pag1'} component={pag1}/>
						<Screen name={'pag2'} component={pag2}/>
						<Screen name={'pag3'} component={pag3}/>
	        </Navigator>
        </NavigationContainer>
    )
}

// com react router dom
export default function App() {
    return (
        <BrowserRouter>
          <Routes>
	          <Route path={'pag1'} element={<pag1/>}/>
						<Route path={'pag1'} element={<pag2/>}/>
						<Route path={'pag1'} element={<pag3/>}/>
	        </Routes>
        </BrowserRouter>
    )
}
```

### Options

As screens possuem um atributo chamado `*options*`, e nele podemos passar uma série de propriedades com algumas configurações de título, de animação e etc.. Uma delas é o `headerShown: *false`,* que retira o cabeçalho branco que mostra o nome da página.

### Tipando as Rotas: routes.d.ts

Para que possamos ter intelisense na hora de navegarmos pela nossa aplicação, é bom que tipemos nossas rotas. Não só para sabermos o nome dela mas também para saber caso ela precise de algum parâmetro. Para fazer isso podemos fazer de duas formas. A primeira forma é criando um arquivo de declaração do typescript chamado `*navigation.d.ts*` dentro de `*@types*` . Nele terá a seguinte estrutura:

Para rotas sem parâmetro, adicionamos undefined, para rotas com parâmetro adicionamos um objeto, o nome do parâmetro e seu tipo.

> Lembrando que é o nome da rota (`*name*`) e não o nome do componente. Isso pode vir a confundir e não carregar.

```tsx
export declare global {
    namespace ReactNavigation{
        interface RootParamList{
            nomeRota1: undefined,
            nomeRota2: undefined,
						nomeRota3: {
							parametro: string/number/obj
						}
        }
    }
}
```

### Tipando as Rotas: com types

Para tiparmos de uma forma mais simples e comum, podemos importar um um componente de propriedades daquela navegação. Utilizando o `*stack Navigator*`, por exemplo, podemos importar o `*NativeStackNavigationProp*` e criar um type com as rotas.

```tsx
import {NativeStackNavigationProp} from '@react-navigation/native-stack'

export type TRoutes = {
    nomeRota1: undefined,
    nomeRota2: undefined
}

export type TNavigatorProps = NativeStackNavigationProp<TRoutes>
```

Depois é só tiparmos a rota na hora da sua criação

```tsx

import { createNativeStackNavigator } from '@react-navigation/native-stack'

import {TNavigatorProps} from "../@types/auth.routes";

const { Navigator, Screen } = createNativeStackNavigator<TRoutes>()

function Routes() {
    return (
			...
    );
}

export default Routes;
```

### Navegando

Para navegar é muito simples. Basta importar o hook de navegacão e indicar para onde queremos ir no toque de um botão.

```tsx
function Component(){
	const navigation = useNavigation()
	
	function handleClick(){
	    navigation.navigate('nomeRota1')
	}

...
}
```

### Bottom Tab Navigator

O tab navigator é a navegação de tabs, onde se tem geralmente ícones e botões

```tsx
npm install @react-navigation/bottom-tabs
```

Para configurar as rotas é muito simples, mega similar:

```jsx
// app.routes.tsx

// importamos o tabnavgator
import {createBottomTabNavigator} from '@react-navigation/bottom-tabs'

// importamos as rotas desejadas
import Home from "@screens/home";
import Profile from "@screens/profile";

// pegamos o navigator e o screen
const {Navigator, Screen} = createBottomTabNavigator()

function AppRoutes(){
    return (
				// definimos do mesmo jeito
        <Navigator>
            <Screen name={'home'} component={Home}/>
            <Screen name={'profile'} component={Profile}/>
        </Navigator>
    )
}

export default AppRoutes;
```

# Configurando as Tabs

Podemos retirar tanto o cabecalho branco com o nome da página quanto configurar o estilo das tabs.

## Cabeçalho e Label

Para isso podemos utilizar a propriedade `*ScreenOptions*` no `*Navigator*` com um objeto de configuração. Dentre várias opções podemos retirar o cabeçalho e retirar o nome das tabs deixando apenas os ícones.

```jsx
<Navigator *screenOptions*={{
		headerShown: *false,
		tabBarShowLabel: false*
		}}> 
	// ... screens
</Navigator>
```

## Ícones e Cores

Mas como podemos ver, os ícones não estão configurados ainda. Para fazer isso é muito simples. Seja com um arquivo interno ou uma biblioteca de ícones externa, basta passar o ícone dentro na propriedade `*tabBarIcon*` .

A `*TabBarIcon*` é uma propriedade que está disponível em `*options*` dos componentes `*Screens*`. Ela recebe uma função que retorna o ícone.

Podemos mudar a cor de todos os ícones através das propriedades `*tabBarActiveTintColor` e `tabBarInactiveTintColor`* do `*Navigator*` .

```jsx
<Navigator *screenOptions*={{
		headerShown: *false,
		tabBarShowLabel: false

		tabBarActiveTintColor: colors.green["700"],
    tabBarInactiveTintColor: colors.red["500"]*
		}}> 
	
<Screen name={'home'}
        component={Home}

				// propriedade de config
        options={{
            tabBarIcon: ()=> <House size={32} />
        }}/>

<Screen name={'profile'}
        component={Profile}
        options={{
            tabBarIcon: ({color})=> <UserCircle color={color} size={32} />
        }}/>
</Navigator>
```

## Finalizando a Bottom Tab

Podemos também estilizar o fundo, que é o que envolve os nossos ícones. Para isso é muito simples, precisamos mexer no objeto de configuração `*tabBarStyle*` .

```jsx
<Navigator screenOptions={{
            headerShown: false,
            tabBarShowLabel: false,
            tabBarActiveTintColor: colors.green["700"],
            tabBarInactiveTintColor: colors.gray["200"],

            tabBarStyle: {
                backgroundColor: colors.gray["600"],
                borderTopWidth: 0,
                paddingBottom: 36,
                paddingTop: 36,
                height: "auto"
            }
            }}>
```

> Obs.: Nós também podemos ocultar um botão com

> `*options={{tabBarButton: ()=> null}}*` . Isso pode ser útil para quando temos mais uma tela mas não queremos aplicar um outro estilo de navegação.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/e099aa2c-11fa-4940-9155-aff2f0bad78e/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/3309ca37-caa1-4807-ae3e-fec783c46fce/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/a859045f-8c24-4eae-a486-c3060a45a153/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/441c5886-c40a-43f7-bd1c-a64d6110157a/Untitled.png)


Subtópico: [[React Native]]