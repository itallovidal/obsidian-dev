### O que é?

ZOD é uma biblioteca focada em resolver validações. Há muitas outras bibliotecas focadas em validar dados, porém o ZOD se destaca por ter um sistema robusto de suporte ao typescript.

### Instalação

Primeiro devemos instalar de fato o ZOD.

```jsx
npm install zod
```

Pronto, de forma simples e leve o ZOD será instalado em nosso projeto. Ele pode ser usado sozinho ou em conjunto com o `*React-hook-form`* , que é o que faremos aqui. Usaremos o `*useForm*` para manipular os estados do formulário e o ZOD para fazer as validações necessárias, integrando as duas bibliotecas e deixando o form o mais simples e direto possível.

Para que possamos realizar essa integração, devemos baixar os resolvers: eles possibilitam que uma biblioteca externa se conecte com o hookform.

```jsx
npm install @hookform/resolvers
```

### Schemas

`*Schemas*` são configurações onde se possui um mapeamento do nome e sua validação equivalente. Podem ser de um elemento único caso seja um `*form*` com um único input ou pode ser um objeto com um mapeamento mais complexo. Por exemplo:

```jsx
// importando o objeto z da biblioteca do zod
import {z} from 'zod'

// criando um objeto de validação 
const schema = z.object({
    name: z.string(),
    password: z.string()
})
```

Como podemos ver, o tipo da validação está dentro do objeto `*z*` que nós importamos. Temos uma lista bem extensa de possibilidades de validações, só precisamos especificar o que o ZOD deve validar que todo o resto será feito sozinho.

Exemplos de validações de string:

```jsx
// validations
z.string().max(5);
z.string().min(5);
z.string().length(5);
z.string().email();
z.string().url();
z.string().emoji();
z.string().uuid();
z.string().cuid();
z.string().cuid2();
z.string().ulid();
z.string().regex(regex);
z.string().includes(string);
z.string().startsWith(string);
z.string().endsWith(string);
z.string().datetime();          // UTC
z.string().ip();                //  IPv4 and IPv6

// transformations
z.string().trim();              // retira espacos em branco
z.string().toLowerCase();       // toLowerCase
z.string().toUpperCase();       // toUpperCase
```

Exemplos de validações de Números:

```jsx
z.number().gt(5);
z.number().gte(5);               // alias .min(5)
z.number().lt(5);
z.number().lte(5);               // alias .max(5)

z.number().int();                // valor precisa ser inteiro

z.number().positive();           // > 0
z.number().nonnegative();        // >= 0
z.number().negative();           // < 0
z.number().nonpositive();        // <= 0

z.number().multipleOf(5);        // Múltiplo de 5, ou divisível por 5.
z.number().step(5)               // Múltiplo de 5, ou divisível por 5.
```

E nós podemos fazer uma cadeia de validações caso precisemos de algo mais robusto:

```jsx
const schema = z.object({

    // deve ser uma string com o mínimo de 3 e máximo de 10 caracteres
    name: z.string().min(3).max(10), 

    // deve ser uma string com mínimo de 3 caracteres
    password: z.string().min(3)
})
```

### Integrando com useForm

Como dito anteriormente, temos que utilizar do resolver para poder fazer essa integração. Com ele instalado, vamos importá-lo e passar como `*props*` do `*useForm*` .

```jsx
import {z} from 'zod'

// importando o resolver
import { zodResolver } from '@hookform/resolvers/zod';

const schema = z.object({
    name: z.string().min(3).max(10),
    password: z.string().min(3)
})
```

```jsx
function App() {
    const {
        formState: {errors},
        register,
        handleSubmit } = useForm({
				
        // passando o resolver do zod, e dentro dele o nosso schema
        resolver: zodResolver(schema)
    })

		.
		.
		.
		... resto do app
}
```

### Z.infer

Uma das coisas muito interessantes do ZOD é a incorporação do typescript. Até aqui nós fizemos um `*schema de validação*`, e a `*integração com o useForm*`. Só que caso usemos nossa e formos usar o objeto com os dados do nosso form, ele estará sem tipagem. O documento deve estar até agora mais ou menos assim:

```jsx
import {z} from 'zod'
import { zodResolver } from '@hookform/resolvers/zod';

const schema = z.object({
    name: z.string().min(3).max(10),
    password: z.string().min(3)
})
```

```jsx
function App() {
    const {
        register,
        handleSubmit } = useForm({
        resolver: zodResolver(schema)
    })

		// aqui estará dando erro: 'data é do tipo any implicitamente'
    function showUser(data){
        console.log('Passou! Tudo correto!')
        console.log(data.name)
        console.log(data.password)
    }

    return (
        <form onSubmit={handleSubmit(showUser)}>
            <h1>Nome</h1>
            <input type="text" {...register('name')} /> <br/> <br/>

            <br/>
            <input type="number" {...register('password')} /> <br/> <br/>

            <Button/>
        </form>
    )
}
export default App
```

Como vimos anteriormente no documento do `*useForm*`, podemos resolver isso criando uma interface com a configuração do nosso usuário:

```tsx
import {z} from 'zod'
import { zodResolver } from '@hookform/resolvers/zod';

// criando a interface usuário para que ele seja tipado
interface User {
    name: string,
    password: string
}

const schema = z.object({
    name: z.string().min(3).max(10),
    password: z.string().min(3)
})
```

```tsx
function App() {
    const {
        formState: { errors},
        register,       // passando o tipo como generics
        handleSubmit} = useForm<User>({
        resolver: zodResolver(schema)
    })

		// e passamos aqui o tipo do usuário 
    function showUser(data: User){
        console.log('Passou! Tudo correto!')
        console.log(data.name)
        console.log(data.password)
    }

    return (
			//... resto do código
    )
}
```

Esse é uma das formas de resolver esse problema. Com o ZOD podemos inferir o tipo do objeto data pelo nosso schema. Porque analisando esse código podemos reparar que nosso objeto com os dados é descrito na interface e também no schema. No objeto de validação também dizemos seu nome e suas características - até de uma forma mais específica.

Para corrigir essa duplicação de código, podemos criar um tipo com base no schema utilizando o método `*z.infer*` disponível no ZOD. Com ele, o ZOD irá identificar o shape - o molde - do objeto e irá retornar para nós essa interface.

```tsx
interface User extends z.infer<typeof schema>{}

// ou podemos criar um type

type User = z.infer<typeof schema>

// ambos funcionam perfeitamente, são duas abordagens
```

### Error Handling

Assim como `*useForm*` puro, podemos criar mensagens personalizadas de erro. A única diferença é que ao invés de passar essas mensagens como objeto opcional no `*register*`, elas são implementadas no schema do ZOD.

```tsx
const schema = z.object({
		// podemos quebrar em mais linhas para ler com mais facilidade
    name: z.string()
        .min(3, {message:"Mínimo de 3 caracteres."})
        .max(9, {message: "Máximo de 9 caracteres."}),

    password: z.string().min(3, {message:"Mínimo de 3 caracteres."}),
})
```

E podemos acessar essa mensagem de erro normalmente pelo objeto `*errors*` do `*useForm*` .

node: [[Bibliotecas]]