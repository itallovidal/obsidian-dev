Com essa biblioteca, poderemos utilizar SVGS de forma mais simples como se eles fossem componentes.

```jsx
npm i react-native-svg-transformer --save-dev
```

E agora devemos adicionar um arquivo chamado `*metro.config.js*`, e nele um objeto de configuração. O código abaixo será responsável por possibilitar que a biblioteca se comporte como o esperado.

```jsx
//metro.config.js 
const { getDefaultConfig } = require("expo/metro-config");

module.exports = (() => {
  const config = getDefaultConfig(__dirname);

  const { transformer, resolver } = config;

  config.transformer = {
    ...transformer,
    babelTransformerPath: require.resolve("react-native-svg-transformer")
  };
  config.resolver = {
    ...resolver,
    assetExts: resolver.assetExts.filter((ext) => ext !== "svg"),
    sourceExts: [...resolver.sourceExts, "svg"]
  };

  return config;
})();
```

E abaixo o arquivo de tipos do TS:

```tsx
declare module "*.svg" {
  import React from "react";
  import { SvgProps } from "react-native-svg";
  const content: React.FC<SvgProps>;
  export default content;
}
```


Subtópico: [[Bibliotecas RN]]