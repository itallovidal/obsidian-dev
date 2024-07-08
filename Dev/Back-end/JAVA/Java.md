# JRE e JDK

_**Java Runtime Enviroment**_ é um software que é responsável por fazer com que programas feitos em JAVA sejam executados adequadamente. Ele pega o código executável e compila para a plataforma desejada. É um conjunto de bibliotecas, e configurações, além da JVM, que possibilitam esse processo.

_**Java Developer Kit**_ é uma coleção de ferramentas que um desenvolvedor precisa para que seja desenvolvido uma aplicação em `*JAVA*`. Consiste em tudo que o JRE fornece mais `*JavaTools*`, o `*Java Compiler*`, `*debbugger*` e outras ferramentas voltadas ao desenvolvimento.

# Estrutura de dados

Abaixo iremos ver algumas estruturas de dados interessantes que podemos utilizar durante nosso desenvolvimento como listas, hasmaps, vetores e algumas coisas estruturas.

## Arrays

Vetores em java possuem um tamanho fixo, são estruturas que recebem um conjunto de dados predefinido. Não são muito flexíveis.

```java
String[] nomes = {"itallo", "thaissa", "manu"};
```

## ArrayList

Listas são vetores dinâmicos, ou seja, não possuem quantidade de elementos especificada, possuindo tamanho variável.

Para instanciar uma ArrayList com valores podemos abrir chaves, e passar um objeto com método `*add*`e seus valores.

```java
ArrayList<String> cadastros = new ArrayList<String>(){
			{
				add("itallo");
				add("thaissa");
				add("manu");

			}
		};
```

## Métodos interessantes

- indexOf
    
- equals
    
- contains
    
- add
    
- removeIf
    
- get
    
- remove
    
- isEmpty
    

## Maps: HashMap

Conhecido também como Coleções, são conjuntos de dados que possuem uma chave associada com um valor. Por exemplo, um `*hasmap*` com `*String*` e `*int`* para citar notas de alunos:

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/c01cc751-ac10-4bab-b7ee-84ac03ebb10c/Untitled.png)

Podemos notar que o java não aceita tipos primitivos na assinatura do Map. Para resolver esse problema podemos utilizar uma `*Wrapper Class` .* São classes que nos permite utilizar tipos primitivos como tipo de referência, onde possuem métodos úteis e podem ser usadas em coleções. **

```java
Map<String, Integer> notas = new HashMap<>(){
			{
				put("itallo", 10);
				put("thaissa", 8);
				put("manu", 9);
			}
	};
```

## Métodos interessantes

- clear
    
- put
    
- forEach
    
- equals
    
- get
    
- merge
    
- remove
    
- isEmpty
    

## Maps: HashSet

Muito parecido com o `*hashMap*`, o `*hashmap*` também é uma categoria das coleções, e possui como característica guardar elementos únicos. Ele não trabalha com chave-valor, e sim apenas o valor.

> OBS.: Hashset não possuem ordem definidas.

Ele não repete os elementos, se tentarmos adicionar um valor igual a um já existente, ele não irá adicionar no `*hashMap`.*

## Streams e Lambda

Uma stream é uma coleção de objetos, como hashmap ou setMap. Com a introdução do Java 8, é possível utilizar uma forma mais declarativa, funcional e curta para lidar com coleções.

Podemos utilizar métodos como filter, map, reduce, find e etc., métodos muito utilizados em linguagens como javascript que possui um viés mais declarativo.

Para utilizar esses métodos, devemos usar lambdas, outra feature nova que veio com o java8. Muito parecida com as arrow functions do JS, sua estrutura é composta com o `valor do laço` + `operador de seta` + `o que deve ser executado` .

```java
ArrayList<String> cadastros = *new* ArrayList<String>(){   
 {       
		add("itallo"); 
    add("thaissa");
    add("manu");
 }};

// printa todos os nomes
cadastros.forEach(nome -> System.***out***.println(nome));
```

# Exceções: Verificadas e não Verificadas

As exceções verificadas são excecões que o compilador vai exigir que você as trate, processos que podemos prever que vai dar problema. Já as não verificadas são excecoes onde só conseguimos verificar no momento da excecucão do código.

## Try/Catch

Uma das melhores formas de lidar com exceções verificadas é utilizando `*try/catch` ,* assim podemos “tentar” realizar determinada tarefa, caso tenhamos algum problema nesse processo podemos “lançar” o erro e “pegar” esse erro para fazer alguma tratativa.

Vamos ver o exemplo abaixo. Temos um método estático com nome de “calc” que calcula um determinado valor + 5. A questão é que ele só pode fazer essa conta caso o número fornecido for maior que 0.

Então fazemos uma verificação para ver se o número é menor que zero e caso ele seja, jogamos uma exceção do tipo mais básico: `*Exeception*` . Você deve notar que na assinatura do método está `*throws Exeception*` .

Isso acontece porque em caso onde temos Exceções Verificadas dentro de métodos, devemos informar em sua assinatura o qual tipo de exceção ele pode vir a retornar.

```java
public class Main {

    public static int calc(int a) throws Exception {
            if(a <0){
                throw new Exception("'a' não pode ser menor que zero.");
            }

            return a + 5;
    }
}
```

Agora podemos utilizar de um `*try/catch*` para tentar realizar o nosso processo, e caso algo dê errado, irá cair no bloco catch logo abaixo.

```java
public class Main {

    public static int calc(int a) throws Exception {
            if(a <0){
                throw new Exception("'a' não pode ser menor que zero.");
            }

            return a + 5;
    }

    public static void main(String[] args) {
        try{
            int result = calc(3);
            System.out.println(result);

        }catch (Exception e){
            System.out.println(e.getMessage());
        }
    }
}
```

node: [[Backend]]