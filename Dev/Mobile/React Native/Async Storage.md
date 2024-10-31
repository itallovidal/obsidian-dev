Temos diversas maneiras de armazenar conteúdo em nosso dispositivo. Seja online, offline ou híbrido, a abordagem dependerá do que precisamos em nosso aplicativo. Neste documento veremos a abordagem offline com o **`*Async Storage.*`**

Como o próprio nome já diz, é uma forma assíncrona de guardar dados no dispositivo de maneira desconectada. Funciona muito semelhante ao **`*local Storage*`** do navegador, então é muito simples e intuitivo. Para que possamos utilizar deste modelo devemos fazer a seguinte instalação:

```jsx
npx expo install @react-native-async-storage/async-storage
```

Pronto, agora só precisamos importar o objeto e utilizá-lo.

### Guardando Dados

Assim como o localStorage do navegador, o asyncStorage só guarda strings. Ou seja, caso desejarmos guardar vetores ou objetos sempre precisaremos dar um `*JSON.strigify()*`. Abaixo podemos ver um exemplo guardando um vetor:

```jsx
async function storeData(data: User[]) {
	// transformando o vetor de usuários em uma string
    const list = JSON.stringify(data)
	// processo é assíncrono
    await AsyncStorage.setItem('lastList', list)
}
```

### Pegando Dados

```jsx

async function getStoredList(): Promise<CartItem[] | false> {
    const response = await AsyncStorage.getItem('lastList')
    if(response){
	// lembrar de transformar de volta de string para objeto/vetor
        return JSON.parse(response)
    }
    return false
}
```

### Métodos úteis

Podemos limpar todos os dados utilizando:

```jsx
AsyncStorage.clear()
```

### Lista de todos os Métodos

![[Pasted image 20240708211420.png]]

Subtópico: [[React Native]]