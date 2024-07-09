Essa biblioteca nos disponibiliza uma série de `*hooks*` para manipulação de formulário dentro da nossa aplicação. O intuito é diminuir a quantidade de renderizações, aumentando a performance mantendo o manuseio das informações descomplicada.
### Instalação

```jsx
npm i react-hook-form
```

### useForm: Register e watch

```jsx
function App() {

		// método watch
    const {register, watch} = useForm()

		// acessando fornecendo o nome do input dado no register
    console.log(watch('name'))

    return (
    <form>
        <h1>Nome</h1>
        <input type="text" {...register('name')} />
        <button type={'submit'}>Enviar</button>
    </form>
  )
}
```

O método `*watch`* nos possibilita ‘vigiar’ um campo e ter suas informações à medida que se é atualizado. Ou seja, a cada vez que mudarmos uma letra no input, saberemos seus valores em tempo real. É basicamente a mesma coisa de criar um useState baseado no valor de um input, porém de forma mais simples.

O useForm nos provê diversos métodos que iremos ver ao longo desta documentação. O `*register*` é um dos mais usados pois ele é responsável por registrar/vincular nosso input à biblioteca que estamos utilizando. Uma vez feita essa operação, poderemos manipulá-lo através de métodos disponíveis no useForm.

Sua sintaxe é muito simples:

```jsx
function App() {
		// desestruturandoo register
    const {register, watch} = useForm()

  return (
    <form>
        <h1>Nome</h1>
				
				// note a utilizacão do spread
        <input type="text" {...register('name')} />
        <button type={'submit'}>Enviar</button>
    </form>
  )
}
```

O register retorna 4 elementos: `*name*`, `*onBlur*`, `*onChange*` e `*ref*`.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/349727ab-69d9-450f-8e02-ccb791fa4214/Untitled.png)

São métodos/propriedades que serão usadas pelo useForm para monitorar o campo, por isso devemos “espalhá-los” no input. Muito importante dar um nome para que possamos futuramente acessar esse input pelo useForm.

### Register Options

Ele possui um objeto opcional - cuja interface é `*RegisterOptions*` - capaz de receber argumentos de verificação e modificação de valor. E é neste ponto a maior vantagem do `*useForm*`: lidar com verificações e erros.

Nesse objeto podemos transformar o valor capturado em número ou em data por exemplo. Ou torná-lo obrigatório, dizer que precisa ter x caracteres ou no máximo y.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c20a0fb7-a92c-4dc8-b755-3f9771634594/Untitled.png)

Esses são os valores aceitos por padrão, mas depois podemos expandir as possibilidades com um validador mais complexo em conjunto com o `*useForm*`. Vamos usar por exemplo o `*required*`:

Note a estrutura: Um objeto com o nome da verificação e dentro dele recebendo um valor e uma mensagem caso a verificação tenha alguma falha.

```jsx
function App() {
    const {register} = useForm()

    return (
    <form>
        <h1>Nome</h1>
        <input type="text" {...register('name', {
            required: {
                value: true,
                message: 'Informe o campo!'
            }
        })} />

        <Button/>
    </form>
  )
}
```

Assim, é com outros tipos de validações:

```jsx
function App() {
    const {register} = useForm()

    return (
    <form>
        <h1>Nome</h1>
        <input type="text" {...register('name', {
            required: {
                value: true,
                message: 'Informe o campo!'
            }
        })} />

        <input type="text" {...register('password', {
            minLength: {
                value: 6,
                message: 'Campo de senha deve haver mais de 6 caracteres.'
            }
        })} />

        <Button/>
    </form>
  )
}
```

### useForm: HandleSubmit e FormState

O `*handleSubmit*` provido pelo `*useForm*` é responsável por fazer as verificações necessárias internas - aquelas que passamos - e caso tudo esteja dentro dos conformes, ele dispara uma função que nós passamos como parâmetro.

```jsx
// note a criacão da interface
interface User {
    name: string,
    password: string
}

function App() {
		//                               e a tipagem do form
    const {register, handleSubmit} = useForm<User>()
    
		function showUser(data: User ){
        console.log('Passou! Tudo correto!')

        console.log(data.name)
        console.log(data.password)
    }

    return (
    <form onSubmit={handleSubmit(showUser)}>
        <h1>Nome</h1>
        <input type="text" {...register('name', {
            required: {
                value: true,
                message: 'Informe o campo!'
            }
        })} />

        <input type="text" {...register('password', {
            minLength: {
                value: 6,
                message: 'Campo de senha deve haver mais de 6 caracteres.'
            }
        })} />

        <Button/>
    </form>
  )
}
```

Ou seja, a funcão `*showUser*` só será disparada caso o nome esteja preenchido e a senha tenha uma quantidade de caracteres maior que 6. Repare que para termos uma tipagem adequada foi criado uma interface de usuário. Essa interface foi utilizada como generics do `*useForm*` e também no `*showUser*`, já que essa função receberá um objeto com os dados do formulário.

Podemos também passar uma segunda funcão de erro para caso essa validação não dê certo:

```jsx
function App() {
    const {register, handleSubmit} = useForm<User>()
    
		function showUser(data: User ){
        console.log('Passou! Tudo correto!')

        console.log(data.name)
        console.log(data.password)
    }

    function showError(){
        console.log('Algo deu errado!')
    }

    return (
    <form onSubmit={handleSubmit(showUser, showError)}>
        <h1>Nome</h1>
        <input type="text" {...register('name', {
            required: {
                value: true,
                message: 'Informe o campo!'
            }
        })} />

        <input type="text" {...register('password', {
            minLength: {
                value: 6,
                message: 'Campo de senha deve haver mais de 6 caracteres.'
            }
        })} />

        <Button/>
    </form>
  )
}
```

### Lidando com Erros

Para que possamos mostrar a mensagem específica de erro do input, devemos desestruturar um objeto responsável por armazenar os estados do formulário. O objeto formState possui diversas propriedades e métodos que capazes de nos informar se o form foi validado, se foi tudo certo, se houve erros, está carregando e etc.

Para nós por enquanto serão interessantes os objetos `*errors*` , `*isSubmitSuccessful*` - que iremos ver em breve.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/101646f6-4810-4c31-bba8-6858077165ac/Untitled.png)

```jsx
const {
			formState: {errors}, // desestruturando e desestruturando
			register,
			handleSubmit
			} = useForm<User>()
```

`*errors`* é um objeto vazio que é preenchido com todos os dados que não passaram pela verificação. Por exemplo, caso o input de idade esteja preenchido errado, o objeto ficará desta forma:

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0a8df43e-7e6c-4e54-b533-923d36b57cf4/Untitled.png)

Note que dentro do objeto de erro temos um outro objeto com o mesmo nome que definimos no `*register*` que guarda o input referente, a mensagem de erro e o tipo do erro para caso tenhamos mais de uma validação.

Agora fica extremamente fácil de mostrar uma mensagem para o usuário de acordo com o erro de validação do formulário.

```jsx
function App() {
    const {
            formState: {errors},
            register,
            handleSubmit} = useForm<User>()

    function showUser(data: User ){
        console.log('Passou! Tudo correto!')

        console.log(data.name)
        console.log(data.password)
    }

    return (
    <form onSubmit={handleSubmit(showUser)}>
        <h1>Nome</h1>
        <input type="text" {...register('name', {
            required: {
                value: true,
                message: 'Informe o campo!'
            }
        })} />

				// caso o objeto de erro tenha um objeto de name, mostre a mensagem
        {errors.name && <p>{errors.name?.message}</p>}

        <input type="text" {...register('password', {
            minLength: {
                value: 6,
                message: 'Campo de senha deve haver mais de 6 caracteres.'
            },
            required: {
                value: true,
                message: 'Informe o campo!'
            }
        })} />

				// caso o objeto de erro tenha um objeto de password, mostre a mensagem
        {errors.password && <p>{errors.password?.message}</p>}
        <Button/>
    </form>
  )
}
```

### Reset, isSubmitSuccessfull

Após o submit do form, mesmo as validaçoes ocorrendo com sucesso, nosso formulário mantém os dados digitados no input. Podemos resolver isso de várias maneiras, e uma delas é resetando com o método nativo `*reset`* da biblioteca.

Apesar de muito comum, a documentação oficial recomenda que o reset não ocorra dentro do callback do método handleSubmit. Dentro do FormState temos um booleano que nos informa se o form teve sucesso ou não.

Utilizando essa informação em conjunto do useEffect, podemos limpar o form assim que ela for enviado.

```jsx
function App() {
    const {
        formState: {errors, isSubmitSuccessful },
        register,
        reset,
        handleSubmit} = useForm<User>()

    React.useEffect(()=>{
        if(isSubmitSuccessful)
            reset()

    }, [isSubmitSuccessful])

    function showUser(data: User ){
        console.log('Passou! Tudo correto!')

        console.log(data.name)
        console.log(data.password)
    }

    return (
        <form onSubmit={handleSubmit(showUser)}>
            <h1>Nome</h1>
            <input type="text" {...register('name', {
                required: {
                    value: true,
                    message: 'Informe o campo!'
                }
            })} />

            {errors.name && <p>{errors.name?.message}</p>}

            <input type="text" {...register('password', {
                minLength: {
                    value: 6,
                    message: 'Campo de senha deve haver mais de 6 caracteres.'
                },
                required: {
                    value: true,
                    message: 'Informe o campo!'
                }
            })} />

            {errors.password && <p>{errors.password?.message}</p>}
            <Button/>
        </form>
    )
}
```


# React native 

Para que possamos utilizar o useForm com o react native teremos que utilizar um `*Controller*`. Ele é um componente responsável por controlar nosso input e manipular as suas mudanças. Possui como atributos `*name*` , `*control`* e `*render*` . O atributo `*render*` recebe uma função que vai renderizar nosso input, e ele desestrutura os métodos do campo `*onChange*` , `onBlur` **e _`value` ._

Vejamos a estrutura básica:

```jsx
<Controller control={control}
            name={"produto"}
            render={({field: {onChange, onBlur, value}})=> (
                <Input onChangeText={onChange}
											 onBlur={onBlur}
											 value={value}/>)} /> 
```


Subtópico: [[Bibliotecas RN]]

Subtópicos: [[Bibliotecas]]