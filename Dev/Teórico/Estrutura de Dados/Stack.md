Pilha é uma estrutura de dados que consiste em guardar elementos um em cima do outro, como o nome sugere. É uma estrutura conhecida por ser do tipo `*LIFO*`, onde o último elemento a entrar é o primeiro a sair.

Nesta estrutura temos alguns métodos comuns:

- `*push*`:
    - utilizado para adicionar elementos
- `*pop*`:
    - utilizado para remover e mostrar o último elemento
- `*peek*`:
    - utilizado para ver o último elemento
- `*size*`:
    - utilizado para mostrar a quantidade de elementos
- `*isEmpty*` :
    - utilizado para verificar se a pilha está vazia

Implementação da classe `*Stack`* sem comentários

```tsx
class Stack{
    private items: number[] = []
    private counter = -1

    push(value: number){
        console.log(`Elemento ${value} adicionado à posição ${this.counter +1} da pilha.`)

        this.counter++
        this.items[this.counter] = value
    }

    pop(){
        if(this.counter === -1 ) {
            console.log(`Sem mais elementos para retirar.`)
            return undefined
        }

        const lastElement = this.items[this.counter]

        console.log(`Elemento retirado -> ${lastElement}.`)

        this.items = this.items.filter((v, i)=> {
            if(i !== this.counter){
                return v
            }
        })

        this.counter--

        return lastElement
    }

    peek(){
        console.log(`O ultimo elemento -> ${this.items[this.counter]}.`)

        return this.items[this.counter]
    }

    size(){
        console.log(this.counter + 1)

        return this.counter + 1
    }

    isEmpty(){
        console.log(`Está vazia -> ${!(!!(this.counter + 1))}`)
        return !(!!(this.counter + 1))
    }

    show(){
        // console.log(this.counter)
        for (let i = 0; i <= this.counter; i++) {
            console.log(this.items[i])
        }
    }
}
```

# Código Comentado

A classe `*Stack*`

```tsx
class Stack{

		// variável que iremos utilizar para guardar
		// os items da pilha
    private items: number[] = []
    
    // contador responsável por direcionar
    // o valor X à posição Y do vetor.
    
    // com o vetor vazio, esse contador irá 
    // começar com -1
    private counter = -1
```

Quanto ao método de adição:

```tsx
    push(value: number){
        // ao adicionar um valor, 
        // logo, incrementa-se uma unidade
        this.counter++
        
        // isso fará com que o primeiro valor
        // seja adicionado na posição 0 do vetor
        this.items[this.counter] = value
    }
```

Para que possamos ler o último elemento sem retirá-lo usaremos o método `*peek*` :

```tsx
    peek(){
        // para retornar o último elemento
        // basta utilizar a posicao do contador
        return this.items[this.counter]
    }
```

Para que possamos saber a quantidade de elementos, utilizamos `*size` :*

```tsx
size(){
	      // como nosso counter comeca em 0
	      // é importante que incrementemos 
	      // uma unidade para sabermos a real
	      // quantidade armazenada
        return this.counter + 1
    }
```

Criaremos um método para verificar se ele está vazio:

```tsx
   isEmpty(){
        // pegamos a quantidade armazenada
        // e transformamos em um booleano.
        
        // só que é importante dizer que 
        // como estamos validando se está vazio 
        // ou não, temos que inverter o sinal
        
        // isso porque 0 em booleano vai dar false
        // e no caso se for vazio de fato, a funcão deve
        // retornar verdadeiro
        return !(!!(this.counter + 1))
    }
```

Para mostrar o conteúdo da `*stack*`:

```tsx
    show(){
        // estrutura for básica
        for (let i = 0; i <= this.counter; i++) {
            console.log(this.items[i])
        }
    }
```

Para retirar o último elemento, utilizaremos a funcão `*pop` :*

```tsx
pop(){
        // antes devemos verificar se o contador
        // é -1, pois caso seja não existe elemento no vetor
        if(this.counter === -1 ) {
            return undefined
        }

				// aqui pegamos o último elemento do vetor
        const lastElement = this.items[this.counter]

        // e aqui fazemos um filtro retirando o último elemento
        // a lógica é pegar todos os elementos
        // que não seja o último.
        
        // pode ser feito com um vetor de apoio
        // também, o intuito é retirar o ultimo elemento
        this.items = this.items.filter((v, i)=> {
            if(i !== this.counter){
                return v
            }
        })

				// como retiramos um elemento, devemos
				// decrementar nosso contador.
        this.counter--
	
	
				// retornando o último elemento para
				// caso precise usar
        return lastElement
    }
```

<aside> 💡 Um ponto importante, é que determinadas implementações de pilha, apenas decrementam a quantidade do contador, fazendo com que o próximo `*push`* substitua o elemento antigo. Cuidado.

</aside>

node: [[Estrutura de Dados]]