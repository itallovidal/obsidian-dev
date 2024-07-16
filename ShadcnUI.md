É uma coleção de componentes pré-prontos para web que nos possibilita criar interfaces de forma extremamente rápida, padronizada e personalizável. Um dos pontos positivos dela é que não é uma biblioteca, e sim uma coleção. Isso implica que não precisamos instalar os componentes, apenas copiar e colar no nosso projeto.

Apesar disso, o Shadcn/UI possui um CLI que facilita esse processo, caso queiramos adicionar um ou vários componentes de forma ainda mais simples e automatizada.
# Instalação

Precisamos instalar o *tailwind*, já que toda a estilização dos componentes é feita em cima dele, e instalar os types do node para que as importações dos componentes ocorram de maneira correta.

```bash
npm install -D tailwindcss postcss autoprefixer

npx tailwindcss init -p
```

```bash
# (so you can import "path" without error)
npm i -D @types/node

```
# Setup

Depois de instalado, serão criados dois arquivos: 
- tailwind.config.js
- postcss.config.js

No primeiro arquivo são configurações especiais do *tailwind*, como acabamos de instalar ele vai estar basicamente vazio e no segundo arquivo são configurações do pós processador ***postCSS***, uma biblioteca que permite que escrevamos CSS com JS.

## Configuração do TSConfig

Nas novas versões do vite são criados 3 arquivos: ***tsconfig.node.json***, ***tsconfig.app.json*** e o ***tsconfig.json***. Por conta disso, o shadcn/ui fica um pouco confuso para lidar com os aliases de importação de arquivos, e estrutura de pastas. Para isso, vamos fazer da seguinte forma: **vamos apagar o documento tsconfig.app.json**, e configurar os outros dois:

Agora temos que adicionar o código abaixo no **tsconfig.ts** dentro da parte de *compileOptions* para que o ts crie ***aliases*** de importação:

```json
...

/* aliases */  
"baseUrl": ".",  
"paths": {  
  "@/*": [  
    "./src/*"  
  ]},
  ...
 "references": [{ "path": "./tsconfig.node.json" }]  
```

O código completo ficará assim:

```json
{
  "compilerOptions": {
    "target": "es2022",
    "useDefineForClassFields": true,
    "lib": ["es2022", "DOM", "DOM.Iterable"],
    "module": "ESNext",
    "skipLibCheck": true,

    /* Bundler mode */
    "moduleResolution": "bundler",
    "allowImportingTsExtensions": true,
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx",

    /* Linting */
    "strict": true,
    "noFallthroughCasesInSwitch": true,

    // Shadcn ui
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  },
  "include": ["src"],
  "references": [{ "path": "./tsconfig.node.json" }]
}
```

E no arquivo ***tsconfig.node.ts***:

```json
{
  "compilerOptions": {
    "composite": true,
    "skipLibCheck": true,
    "module": "ESNext",
    "moduleResolution": "bundler",
    "allowSyntheticDefaultImports": true,
    "strict": true
  },
  "include": [
    "vite.config.ts",
    "tailwind.config.ts",
    "postcss.config.js",
    "eslint.config.js"
  ]
}
```

E agora iremos avisar ao vite que essas importações ocorrerão:

```js
// vite.config.ts

import { defineConfig } from 'vite'  
import react from '@vitejs/plugin-react'  
import path from "node:path"  
  
export default defineConfig({  
	plugins: [react()],  
	resolve: {  
	    alias: {  
	      "@": path.resolve(__dirname, "./src"),  
	    },
	},
})
```

Não se esqueça de **importar o css global no app!**
# Inicializando 

Abaixo podemos inicializar o CLI do shadcn/ui:

```node
npx shadcn-ui@latest init
```

E utilizar o CLI para copiar da base de dados do shadcn/ui para dentro da nossa aplicação.

**Exemplo:**
```node
npx shadcn-ui@latest add button
```