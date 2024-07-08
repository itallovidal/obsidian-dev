O NEST.js é um framework node para aplicações de maior porte. Ele trás uma opinião mais intensa, ou seja, ele possui uma estrutura predefinida a ser seguida, tendo como objetivo ser mais escalável e fácil de manter.

Para que possamos extrair o máximo potencial do NEST, é aconselhável instalar o seu CLI.

```jsx
npm i -g @nestjs/cli
```

Para que possamos criar um projeto podemos utilizar o seguinte comando:

```jsx
nest new "nome-projeto" 
```

```jsx
npm i --save @nestjs/config
```

Isso vai gerar um projeto com as configurações base. Podemos retirar caso queiramos os arquivos `*.eslintrc.js*`, `*.prettierrc*` e [`*readme.md`](http://readme.md) .*

O conteúdo de dentro da pasta `*test`* também _p_odemos retirar, pois ele não faz sentido no momento para nós e podemos apagar um documento dentro da pasta _`src`_ chamado _`app.controller.spec.ts`_

> No `*package.json*` é importante dizer que por padrão o nest.js usa o `*jest`* para fazer os seus testes. Então caso utilizemos outra biblioteca para fazer os nossos testes como o `*vitest`* devemos retirar os scripts de lá.

Nossas pastas vão ficar assim:

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/4a4346bf-389c-4c4c-af27-e442ef532866/Untitled.png)

# TSConfig

Uma das coisas importantes que é bom verificarmos é a configuração do TS Config. Por padrão algumas verificações vem desabilitadas o que pode inferir tipos errados ou pela metade.

```tsx
{
  "compilerOptions": {
    "module": "commonjs",
    "declaration": true,
    "removeComments": true,
    "emitDecoratorMetadata": true,
    "experimentalDecorators": true,
    "allowSyntheticDefaultImports": true,
    "target": "ES2021",
    "sourceMap": true,
    "outDir": "./dist",
    "baseUrl": "./",
    "incremental": true,
    "skipLibCheck": true,
    "strict": true, // false por padrão
    "strictNullChecks": true, // false por padrão
    "noImplicitAny": false,
    "strictBindCallApply": false,
    "forceConsistentCasingInFileNames": false,
    "noFallthroughCasesInSwitch": false
  }
}
```

# Estruturas

## Controllers

Os `*controllers*` são uma porta de entrada para nossa aplicação que são alcançadas através de requisições HTTP. Todo `*Controller*` é identificado por um `*Decorator*` _- muito parecido com as Annotations em Spring_. Elas adicionam comportamento em um determinado trecho de código.

```tsx
@Controller() // decorator
export class AppController {
  constructor(private readonly appService: AppService) {}

  @Get() // decorator
  getHello(): string {
    return this.appService.getHello();
  }
}
```

## Modules

Os modules são arquivos que reúnem tudo: _controllers_, configurações, conexões e reúne tudo em um único arquivo para que possa ser registrado no _nest_. Podemos ver que *decorator `@*Module` ele recebe um objeto com duas propriedades:

- _Controllers_
    - Recebe um vetor de _controllers_.
- _Providers_
    - Recebe um vetor de possíveis dependências para esses _controllers_.

```tsx
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';

@Module({
  controllers: [AppController],
  providers: [AppService],
})

// classe vazia
export class AppModule {}
```

O módulo será responsável por automaticamente administrar a injeção de dependências no controllers dado os providers fornecidos.

## Services (Ou providers)

Mas para que esse processo seja feito da forma correta, os _services_ devem ter um `*decorator`* chamado `@Injectable`. Isso fará com que o _Nest_ consiga entender que aquele serviço pode ser injetável em um _controller_.

```tsx
import { Injectable } from '@nestjs/common';

@Injectable()
export class AppService {
  getHello(): string {
    return 'Hello World!';
  }
}
```

Um Service - ou Provider - nada mais é do que um trecho de código - mais especificamente uma classe - responsável por realizar uma determinada ação que não está vinculada à uma requisição HTTP. Ou seja, um envio de email, Um repositório, casos de usos e etc..

# Pipes

# Decorators Summary

@Injectable

@Controller

@HttpCode

node: [[Node]]