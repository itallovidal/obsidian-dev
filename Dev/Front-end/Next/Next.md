
Subtópico de: [[Front-end/React/React]]
# Introdução

// todo

# Instalação

```jsx
npx create-next-app@latest
```

```jsx
//tsconfig
"moduleResolution": "node",
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/251b1041-63a4-43f8-b863-cb4b653294fa/Untitled.png)

# Page Extensions

Podemos modificar quais extensões o next irá entender que são rotas através das pages extensions. É um vetor que configuramos no next.config.mjs

```tsx
/** @type {import('next').NextConfig} */
const nextConfig = {
  reactStrictMode: true,
  pageExtensions :[
      "page.tsx", "api.ts", "api.tsx"
  ]
};

export default nextConfig;
```

