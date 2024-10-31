Reanimated é uma biblioteca ReactNative capaz de proporcionar animações fluidas de uma maneira muito simples. Com ela podemos usar presets ou criarmos nossas próprias animações para entrada, saída e mudança de estado de algum componente.

# Instalação

Instalando com Expo:

```jsx
npx expo install react-native-reanimated
```

Depois iremos configurar o plugin do babel:

```jsx
module.exports = function (api) {
  api.cache(true);
  return {
    presets: ['babel-preset-expo'],
    plugins: ['react-native-reanimated/plugin'],
  };
};
```

> OBS.: O plugin do RReanimated deve ser o último na lista de plugins.

# Wrapper Animated

Para que possamos utilizar as propriedades desta biblioteca nos componentes, devemos “envolve-los” com um componente chamado **`*Animated*` .** Ele serve como `*wrapper*` e possui suporte nativo aos seguintes componentes:

itemLayoutAnimation

- `*FlatList*`
- `*Image*`
- `*View*`
- `*ScrollView*`
- `*Text*`

Com ele podemos definir animações de entrada, de saída, de mudança de layout e animações personalizadas. Vejamos sua estrutura:

```jsx
// sintaxe
import Animated from 'react-native-reanimated'

<Animated.View>
	// resto dos componentes
</Animated.View>
```

Para componentes como `*TextInput*`, `*Touchables*`, e além, assim como vezes que estamos utilizando bibliotecas de interfaces como `*Styled Components*`, `*Native Base*` e etc., devemos criar um componente animado manualmente a partir da função de criação da biblioteca.

Podemos utilizar a função `*Animated.createAnimatedComponent`* passando o componente em questão para que seja criado um novo componente animado que aceitará tudo o que os componentes nativos aceitam.

```jsx
export const AnimatedAlgo = *Animated.createAnimatedComponent()*
```

# Entering e Exiting

Para Animar a entrada e a saída de componentes na tela podemos utilizar as propriedades `*entering*` e `*exiting*`, respectivavemente. Elas aceitam os seguintes valores:

```jsx
// sintaxe
import Animated, {FadeIn, FadeOut } from 'react-native-reanimated'

<Animated.View entering={FadeIn} exiting={FadeOut}>
	// resto dos componentes
</Animated.View>
```

### Tipos de Animações suportadas

- _Fade_
    
- _Bounce_
    
- _Flip_
    
- _LighSpeed_
    
- _PinWheel_
    
- _Roll_
    
- _Rotate_
    
- _Slide_
    
- _Stretch_
    
- _Zoom_
    

# Layout Transition

Transições de Layout servem para que ocorra uma transição quando a disposição dos elementos mude. Por exemplo, em uma lista, quando um dos elementos for excluído, ela se reorganizar de maneira fluida. Abaixo alguns valores aceitos.

```jsx
// sintaxe
import Animated, {FadeIn, FadeOut, Layout } from 'react-native-reanimated'

<Animated.View entering={FadeIn} exiting={FadeOut} layout={Layout}>
	// resto dos componentes
</Animated.View>
```

### Tipos de Animações suportadas

- Layout
    - Anima eixo X e Y da mesma forma.
- Sequenced
    - Anima primeiro eixo X e largura, depois eixo Y, posição e altura.
- Fading
    - Anima com fade, diminui a opacidade com valor antigo, e depois mostra com o novo.

# Keyframes

O Reanimated suporta o uso de `*keyframes*` para animações personalizadas. Para isso é muito simples: basta instanciar um objeto `*keyframe*` e passar para ele as propriedades de inicio e fim, e dentro delas objetos de transformação com as configurações.

```jsx
import { Keyframe } from 'react-native-reanimated';

const keyframe = new Keyframe({
  0: {
    transform: [{ rotate: '0deg' }],
  },
  100: {
    transform: [{ rotate: '45deg' }],
  },
});
```

Subtópico: [[Bibliotecas RN]]


