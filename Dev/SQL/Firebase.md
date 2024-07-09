## Como funciona o Cloud Firestore

O `*Cloud Firestore*` é um banco de dados `*NoSQL (não relacional)*` orientado a documentos. Em um banco orientado a objeto ao invés de tabelas, você possui as coleções que são containers que armazenam os documentos, e cada documento contem os dados em forma de chave e valor.

## Configurações iniciais do Cloud Firestore

Primeiro é necessário criar um projeto, e dentro desse projeto criar um banco de dados.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/43f9deb0-8ca9-4b73-a688-fdc22bc065b0/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/f790bdb5-f209-4f60-a928-c20158151301/Untitled.png)

Depois é preciso adicionar a um aplicativo:

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/008ec212-6b9f-4e27-8bed-f420e78621f2/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/19694e6e-6d45-440b-b3de-2c8adf98380d/Untitled.png)

Ao adicionar o firebase ao app, ele te fornece um objeto - no caso da WEB - com uma série de configurações que servem para usarmos para nos conectarmos com o banco que acabamos de criar. Além disso, ele indica como podemos instalar o SDK do firebase. Vejamos:

## Instalando Firebase

Para fazer a conexão entre o código e o banco de dados, precisamos primeiro instalar o Firebase no projeto. Muito simples:

```jsx
npm install firebase
```

Depois disso, podemos criar um arquivo `*firebaseConfig.ts*` para guardar e manipular configurações básicas do nosso banco. Com o código que o próprio firebase disponibiliza, já conseguimos estabelecer nossa conexão.

## InitializeApp, getFirestore e firebaseConfig

O firestore trabalha atualmente com módulos, isso significa que cada função pode ser utilizada separadamente, deixando o código mais limpo e possibilitando que nós usemos apenas as funções necessárias para aquele contexto.

```tsx
import { initializeApp } from "firebase/app";
import { getFirestore } from "firebase/firestore";

// Criando uma variável que guarda as configuração do firebase com as credenciais de 
// acesso, recebidas ao criar o app no firebase
const firebaseConfig = {
  apiKey: "AIzaSyC522n8YPDfKkmBGgd_bwIewMmK2vdgE8Y",
  authDomain: "crud-firebase-1d155.firebaseapp.com",
  projectId: "crud-firebase-1d155",
  storageBucket: "crud-firebase-1d155.appspot.com",
  messagingSenderId: "120728452491",
  appId: "1:120728452491:web:d037c86185ec5ff3dac38e"
};

// Inicializando o app com  as configurações firebase
const app = initializeApp(firebaseConfig); 

// Criando uma conexão com o banco de dados
export const db = getFirestore(app)
```

Feito isso, a variável `db` agora é responsável armazenar a conexão com o banco de dados. Ela possui todas as ferramentas capazes de realizar esse processo de autenticação pois como podemos ver acima, possui a chave, o domínio, o id, e etc..

Agora com o projeto criado, e com a conexão do banco configurada, podemos começar os procedimentos rotineiros de banco de dados.

# Sumário

## Configuração

- `*initializeApp*`
- `*getFirestore*`

## Referências

- `*collection*`
- `*doc*`

## Métodos

- `*getDocs*`
- `*addDoc*`
- `*deleteDoc*`
- `*updateDoc*`

## Cláusulas e consultas

- `*query*`
- `*Where*`

## SELECT - getDocs

Como dito anteriormente, o firebase trabalha com um banco orientado à documentos. As informações estão dentro de documentos que estão dentro de coleções. Para que possamos pegar então os documentos com as informações que desejamos precisamos primeiro fazer a captura da sua respectiva coleção.

O firebase nos proporciona um método chamado `*collection*` que aceita a conexão do banco a ser conectado e o nome da coleção.

```jsx
import {collection, getDocs} from 'firebase/firestore'

const usersCollection = collection(db, "users");
const request = await getDocs(usersCollection)
```

- Agora, a variável `usersCollection` guarda o caminho da coleção `users`
- Com ela será possível selecionar os documentos.
- A função `*getDocs*` retorna todos os documentos relacionados à coleção previamente selecionada.

Porém ela retorna informações que não nos interessam. Para que possamos capturar as informações contidas nesses documentos, devemos utilizar a função `*.data()*` disponibilizadas para nós.

```tsx
const docs = request.docs.map(doc => doc.data());
```

Isso retornará um vetor com os documentos do tipo `DocumentData[]`. Por questão de typescript, é interessante remontar os valores que serão retornados para que o código entenda que o tipo retornado não é do tipo `DocumentData[]` mas sim do tipo da interface que você criou.

Por exemplo, se a minha interface for

```tsx
export interface IUser{
    hobbie: string,
    id: string,
    name: string
    password: string,
}
```

Meu `map` **vai ficar assim:

OBS.: Note que colocamos o nome da propriedade após a função para capturarmos seu valor.

```tsx
const docs = request.docs.map(doc =>{
        return {
            id: doc.data().id, 
            name: doc.data().name, 
            password: doc.data().password, 
            hobbie: doc.data().hobbie
        }
    });
```

Dessa maneira, posso dizer que a função retorna `Promise<IUser[]>`

## Query com Where

Podemos realizar `*SELECTS*` com cláusulas de condições também. Para isso devemos importar `*Query*` e `*Where`* e montar nossas consultas da seguinte forma:

```tsx
import {collection, getDocs, query, Where} from 'firebase/firestore'

const usersCollection = collection(db, "users");
const q = query(usersCollection, Where('id', '==', '1'))
const request = await getDocs(q)
```

Como podemos ver, o método query monta a consulta, recebendo como parâmetros a coleção e mais uma função `*Where*`, onde recebe o nome do campo, a operação - `*==*`, `*≠*`, `*≥*` etc. - e o nome do valor.

O Cloud Firestore oferece suporte aos seguintes operadores de comparação:

- `<` → Menor que
    
- `<=` → Menor que ou igual a
    
- `==` → Igual a
    
- `>` → Maior que
    
- `>=` → Maior que ou igual a
    
- `!=` → Diferente de
    
- `array-contains` → Verifica se existe esse valor no vetor
    
- `array-contains-any` →
    
- `in` → várias cláusulas de igualdade (`==`) no mesmo campo com um `OR` lógico
    
    ```jsx
    const q = query(citiesRef, where('country', 'not-in', ['USA', 'Japan']));
    ```
    
    - Retorna aonde country é igual a USA ou Japan
- `not-in` → Use o operador `not-in` para combinar até 10 cláusulas "diferente de" (`!=`) no mesmo campo utilizando um `AND` lógico
    
    ```jsx
    const q = query(citiesRef, where('country', 'not-in', ['USA', 'Japan']));
    ```
    
    - Retorna aonde country não é igual a USA nem Japan

## POST - addDoc

Para adicionar um documento em uma coleção é preciso utilizar o método `addDoc()`

```jsx
import { addDoc } from "firebase/firestore";
```

Esse método recebe como parâmetro a coleção e o objeto que será adicionado na coleção

```jsx
const usersCollection = collection(db, "users");

addDoc(usersCollection, {
    id: crypto.randomUUID(),
    name: user.name,
    password: user.password,
})
```

Com esse código um documento com os atributos `id`, `name`, `password` será criado na coleção `users`

Para deletar ou atualizar um documento, precisamos primeiramente de uma referência a ele. Para isso usaremos a função `*doc*` .

## DELETE - deleteDoc

Para deletar um documento precisamos primeiramente importar as funções `deleteDoc` e `doc`.

```jsx
import { deleteDoc, doc } from "firebase/firestore";
```

A função `doc` pega a referencia do documento, assim como a `collection` pega de uma coleção. Essa função recebe 3 parâmetros: o banco, a coleção e o id do documento.

```tsx
export interface DeleteUserProps {
    id: string
}

export async function deleteUser({id}: DeleteUserProps){
    console.log(id)
    //pega o documento com o id userID na coleção users
    const userRef = doc(db, "users", id);

    // agora só deletar o documento
    deleteDoc(userRef);
}
```

## UPDATE - updateDoc

Para dar update um documento precisamos primeiramente importar as funções `updateDoc` e `doc`.

```jsx
import { updateDoc, doc } from "firebase/firestore";
```

Depois basta criar a referencia para o usuário e utilizar o `updateDoc` para atualizar as informações, para isso basta passar a referencia do usuário e um objeto com os campos que devem ser alterados.

```tsx

const userRef= doc(db, "users", id);
updateDoc(userRef, {
	name: "manu",
});
```

## ORDER BY

Para ordenar os documentos em ordem crescente ou decrescente é preciso utilizar a função `orderBy()`

```jsx
import { query, orderBy } from "firebase/firestore";
```

A função `query` recebe como parâmetro a coleção e o `orderBy`. Já o `orderBy` recebe a propriedade que será ordenada e a propriedade `asc` ou `desc`

```jsx
const usersCollection = collection(db, "users");
const q = query(usersCollection, orderBy("name", "desc"))
const request = await getDocs(q);
```

Dessa maneira, nesse exemplo os documentos da coleção `users` serão organizados em ordem decrescente de acordo com a propriedade `name`

## Limitando a consulta

Basta adicionar a função `limit()` na `query()`, e passar como parâmetro a quantidade de elementos.

```tsx
const collectionRef = collection(db, "users");
const queryDocs = query(collectionRef, limit(3)); // irá retornar apenas 3 elementos
const docsRef = await getDocs(queryDocs);
const docs = docsRef.docs.map(docs => docs.data());

return docs;
```

## **Paginar dados - TERMINAR**

Com os cursores de consulta é possível dividir os dados retornados por uma consulta em lotes de acordo com os parâmetros definidos. Os cursores de consulta do firebase são:

- **`startAt()` →** Começa desse ponto, incluindo o ponto inicial
- **`startAfter()` →** Começa desse ponto, excluindo o ponto inicial
- **`endAt()` →** Termina nesse ponto, incluindo o ponto inicial
- **`endBefore()` →** Termina nesse ponto, excluindo o ponto inicial

Para fazer a paginação, primeiro criei duas variáveis globais, a referencia da coleção e o ultimo elemento retornado

```tsx
let lastDoc: DocumentData; // não inicializou porque nenhum elemento foi retornado ainda
const usersCollection = collection(db, "users");
```

Depois disso, é preciso pegar os primeiros elementos que serão mostrados na tela. Para isso, fiz uma `query` que retorna os 3 primeiros usuários ordenando eles pelo nome de forma crescente.

E logo após, salvo o ultimo elemento desse vetor na variável `lastDoc`, que será utilizado para saber de onde o próximo elemento deve começar.

Então se `docs` retorna `[{name: luiza},{name: maria}, {name: thalita}]`, a variável `lastDoc` guarda `{name: thalita}`

```tsx
// Pego só os 3 primeiros usuários
export async function getFirstsUsers(){
    const queryDocs = query(usersCollection, limit(3), orderBy("name")); // pegando 3 elementos
    const docsRef = getDocs(queryDocs); // referencia para os docs filtrados
    const docs = (await docsRef).docs.map(doc => doc.data()); // pegando os dados
    lastDoc = docs[docs.length - 1]; // pegando o ultimo documento

    return docs; // retorna um vetor de 3 elementos
}
```

Agora para pegar os elementos que vem depois desses, será usado o método `startAfter()`, que dirá “pega os elementos que vierem depois deste”

```jsx
import { startAfter } from "firebase/firestore";
```

Agora criei uma função que será chamada quando precisar dos próximos usuários. Primeiro fiz igual a outra função e fiz uma `query` que retorna os 3 primeiros usuários ordenando eles pelo nome de forma crescente.

Depois, chamei o `startAfter()` e passei como parâmetro a propriedade `name` do ultimo elemento que foi retornado. Passei essa propriedade pois estou ordenando o vetor pela propriedade `name`. Eles precisam de uma organização para saber qual vem antes e qual vem depois.

```tsx
export async function getNextUsers(){
    const queryDocs = query(usersCollection, limit(3), orderBy("name"), startAfter(lastDoc.name));
    const docsRef = getDocs(queryDocs);
    const docs = (await docsRef).docs.map(doc => doc.data());
    lastDoc = docs[docs.length - 1];

    return docs;
}
```

então `queryDocs` pega os 3 elementos que vem depois do elemento `{name: thalita}`, e guarda no `lastDoc` o ultimo elemento dessa nova requisição. Se não houver mais elementos, retorna um vetor vazio

node: [[SQL]]