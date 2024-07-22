### Local Storage, Session Storage e Cookies

Conforme nós, como usuários, navegamos pela a internet, é muito comum entrarmos em um site e nos depararmos com a seguinte pergunta:

> “_Esse site usa cookies para melhorar a experiência do usuário e deseja guardar seus cookies, você permite?”_

Isso se dá pela necessidade das páginas de salvar determinadas informações que são mais simples sem a necessidade de se conectar com um banco de dados e fazer todo um processo mais complexo. Coisas como salvar se o modo escuro ou o claro foi selecionado, salvar onde em um video o usuário parou, qual player ele selecionou, auto-completar determinados dados que são utilizados com frequência, informações básicas de um login, e etc.

Essas informações são guardadas no navegador e podem ser limpas pelo usuário a qualquer momento. Podem ser temporárias ou não. E por último e não menos importante: elas não podem ser informações sensíveis já que o acesso é fácil.

Tabela de características de cada sistema:

—

Capacidade

Acessibilidade

Expiração

Cookies

4kb

Todas Janelas

set Manual

Local Storage

10mb

Todas Janelas

Nunca

Session Storage

5mb

Mesma Janela

Ao fechar Janela

### Local Storage e Session

Suas funcionalidades consistem em salvar, adicionar, recuperar ou excluir dados localmente no seu navegador. A informação é guardada na forma de pares de _**chave-valor**_ e os valores podem ser apenas em `*strings` .*

Seus métodos de manipulação são:

- **setItem(chave, valor) :**
    
    - Armazena um item com a chave e o valor.
- **getItem(chave):**
    
    - Recupera o valor do item com o nome da chave.
- **removeItem(chave):**
    
    - Remove o item usando sua chave.
    
    ```jsx
    const btn = document.querySelector('button')
    
    btn.addEventListener('click', ()=>{
        const valor = document.querySelector('input').value
    
    		// adicionando o valor no local storage
        localStorage.setItem('valorDigitado', valor)
    })
    ```
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/12319dd2-9c45-4837-9414-d711ad2998c7/Untitled.png)
    
    ```jsx
    // verificando quando a pagina carrega se existe algo no local Storage
    if(localStorage.getItem('valorDigitado') !== null){
        const p = document.querySelector('p')
        p.innerHTML = localStorage.getItem('valorDigitado')
    }
    ```
    
    Por padrão, esse item recebido é sempre uma string, ou seja, não podemos armazenar objetos e vetores diretamente, já que o local storage só pode receber dados do tipo `string`. Isso quer dizer que só iremos armazenar strings? Não!
    
    Podemos contornar esse problema facilmente com os métodos de JSON stringfy e parse. Com o Stringfy podemos transformar qualquer tipo de valores em uma string, e depois adicionar ao local storage.
    
    ```jsx
    const vetor = [1,2,3,4,5]
    
    localStorage.setItem('valores', JSON.stringify(vetor))
    ```
    
    E para transformar no tipo anterior podemos usar `*JSON.parse()*` e atribuir à variável que quisermos.
    
    ```jsx
    if(localStorage.getItem('valores') !== null){
        const valores = JSON.parse(localStorage.getItem('valores'))
    
        valores.forEach((valor)=>{
            console.log(valor)
        })
    }
    ```
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0bc1c46a-5c31-493f-8209-7ca1f1357ce1/Untitled.png)
    
    O mesmo exemplo feito com local Storage acima se aplica com session storage já que a forma de manuseio é muito parecida, mudando apenas algumas características específicas de usabilidade onde podemos verificar na tabela citada.
    
    ### Cookies
    
    Os cookies são uma forma mais antiga e mais limitada de armazenar informações. Eles são capazes de armazenar menos dados do que o session e o local storage, e são mais complicados de manipular. A maioria das vezes hoje em dia não o estaremos utilizando.
    
    O comportamento dos cookies são um pouco diferentes também já que ele é enviado ao servidor cada vez que o seu site faz uma requisição de algo, arquivos html, css, imagens, videos e etc.. Isso pode ser um problema pois se você tiver uma requisição mais alta, enviar toda hora esses dados pode fazer com que seu site fique mais lento.
    
    Por padrão o cookie é criado já expirado, então para fazermos ele ficar válido devemos indicar quando ele vai expirar. Para definir que ele nunca expire, podemos setar um valor muito alto, inalcançável.
    
    A data que eles recebem é no formato UTC, podemos utilizar a classe Date para devolver uma data formatada para nós passando o ano, o mes e o dia. Lembrando que o mês na classe Date começa no 0, então 1 é fevereiro, 2 março e etc.
    
    ```jsx
    document.cookie = `
    name=itallo; expires=${new Date(9999, 0, 1).toUTCString()}`
    
    document.cookie = `
    sobrenome=vidal; expires=${new Date(9999, 0, 1).toUTCString()}`
    
    document.cookie // name=itallo; obrenome=vidal
    ```
    
    Outra coisa a se salientar é que ao capturar os cookies, eles vêm juntos, então para mostrá-los ou manipulá-los devemos separar a string devolvida.
    
    Como podemos ver, mexer com cookies são mais trabalhosos e não tão intuitivos. É sempre aconselhável usar session e local storage, a menos que tenhamos que mandar algo específico para o servidor com os cookies, o que é razoavelmente difícil.

[[Javascript]]