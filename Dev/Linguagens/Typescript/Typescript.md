O `*typescript*` é uma linguagem que busca resolver problemas comuns do `*javascript`* e oferecer diversas ferramentas para que o DX - Developer Experience - seja o mais agradável e eficiente possível. Com ele temos acesso à um `*javascript*` fortemente tipado, podendo definir variáveis, retorno e parâmetros de funções, Além disso, podemos antecipar erros antes do tempo de execucão da aplicação.

E não só isso, ele também nos provê um melhor ambiente de desenvolvimento com `*POO*`, já que podemos trabalhar de maneira mais eficaz na utilização de Herança, Encapsulamento e Classes em geral com Interfaces, e Classes Abstratas.

# Instalação e Configuração

Configurando typescript como uma dependência de desenvolvimento:

```jsx
npm install -D typescript
```

Caso estejamos desenvolvendo com node, precisamos baixar o pacote de tipos, pois o TS não reconhece por padrão seus métodos e propriedades específicos.

```jsx
npm install -D @types/node 
```

Criamos um arquivo de configuração do typescript

```jsx
npx tsc --init
```

# Compilação e desenvolvimento

Com o typescript instalado podemos executar o código TS de duas formas:

- Compilando um ou vários arquivos .ts para .js para que possamos executar

```jsx
npx tsc arquivo.ts
```

- Ou podemos instalar uma biblioteca chamada tsx. Com ela podemos executar arquivos ts diretamente, sem precisar compilar e executar os .js

```jsx
npm install -D tsx
```

Agora podemos executar diretamente os arquivos.

```jsx
npx tsx arquivo.ts
```

### Utilizando vite

A segunda forma é usando `*Vite*`: automaticamente criar o ambiente de desenvolvimento e nos dar a opção de inicializar um servidor, fazendo todas as configurações e atualizações necessárias para que possamos escrever nosso arquivo `*ts` .*

É só criar um ambiente `*vite*` e seguir os _prompts_ no console.

```jsx
npm create vite@latest .
```

### Compile-time e Run-time: Revisando

//

Subtópico: [[Javascript]]