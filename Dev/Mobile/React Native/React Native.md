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

Subtópico: [[Mobile]]