Antes de começarmos a fazer nossa API REST em JAVA, é preciso saber a diferença entre uma API REST e uma Aplicação WEB. Abaixo podemos ver as leituras indicadas.

> [Padrões de Arquitetura Software](https://www.notion.so/Padr-es-de-Arquitetura-Software-f24aed8f90cb44e0a8138c4a005a28ca?pvs=21)

> [Aplicação WEB](https://www.notion.so/Aplica-o-WEB-0af0b40229724ad69cde70fde49b6794?pvs=21)

Nesse primeiro momento veremos sobre API REST em `*JAVA*`. Ao iniciar um projeto, veremos uma `*annotation*` chamada `*@SpringBootApplication`* e uma classe `*main*`. Ao lado, algumas pastas do maven, pastas para testes automatizados, algumas pastas para recursos como imagens e outros arquivos HTML, JS, JSON e etc..

## Annotations

`*Annotations*` são um tipo de metadados que fornecem informações que são processadas pelo compilador ou em tempo de execução. Alguns recebem parâmetros com informações adicionais e outros bastam por si só. São utilizados geralmente acima do código que você está anotando, porém podem ser utilizadas na mesma linha também.

As anotações sempre possuem a estrutura de: `*@anotação.*`

A primeira _annotation_ que vemos é a `*@SpringBootApplication` ,* como dito anteriormente. Ela é responsável por informar ao Spring que essa é a classe principal da API, com isso o spring vai habilitar auto configurações.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/c094e3ff-9267-4b72-8a9c-a4e1cd5b857b/Untitled.png)

Vamos criar um _package_ (pasta) para armazenar nosso primeiro `*controller*`.

Abaixo podemos ver duas anotações: `*@RestController*` e `*@RequestMapping`.* A primeira informa que aquela classe faz parte de uma API Rest. A segunda mapeia essa classe para ser um `*controller*` de uma rota específica: `*/hello*`

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/3d8de56b-660a-4d66-aedf-824560e32225/Untitled.png)

Agora iremos criar um método JAVA e mapear este método para ser disparado quando tivermos dentro da requisição`*/hello*` um método `*HTTP GET*`.

```java

@RequestMapping("/hello")
@RestController()
public class helloController {

    @GetMapping()
    public String helloWorld(){
        return "hello world!";
    }
}
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/3683fb27-de9b-4b4c-8252-1cb7f2255768/Untitled.png)

Teremos uma anotação para cada _método http_, e devemos anotar acima da função para que o `*spring*` saiba qual função deve ser chamada para cada requisição. No exemplo acima a função `*helloWorld*` é chamada quando a rota `*/hello*` + `*GET*` é chamada. Abaixo podemos ver algumas outras anotações.

- `*@GetMapping*`
- `*@PostMapping*`
- `*@DeleteMapping*`
- `*@UpdateMapping*`

# Manipulando Corpo e Parâmetros

É muito comum em requisições que peguemos informações pelos parâmetros ou pelo _body_. Vamos ver como podemos fazer para capturar e lidar com esses momentos.

## Path Params

Conhecidos como parâmetros de caminho, são subrotas que identificam um recurso. Por exemplo, vamos supor que queremos pegar o produto de `*id*` X. Esse parâmetro é dinâmico, pode ser 1, 2, 500, 1230, etc.. Para isso vamos utilizar a seguinte estrutura:

```java
// url
localhost:8080/produtos/1
```

```java
@RestController()
@RequestMapping("/produtos")
public class produtosController {

    @GetMapping("/{id}")
    public String getProduct(@PathVariable String id){
        return "O produto foi com o ID de "+ id;
    }
}
```

Toda rota dinâmica utilizaremos `*chaves` + `seu nome` .* Depois disso apenas capturamos esse valor na assinatura da função utilizando a _annotation `@PathVariable`_ com o seu tipo e seu nome.

## Query Params

São valores atribuídos a uma chave que ajudam na pesquisa de algum recurso. Vamos supor que queremos o produto com o `*id*` X mas que seja azul.

```java
// url
localhost:8080/produtos/1?cor=azul
```

```java
@RestController()
@RequestMapping("/produtos")
public class produtosController {

    @GetMapping("/{id}")
    public String getSpecificProduct(@PathVariable String id, @RequestParam String cor){
        return "O produto foi com o ID de "+ id + " cor de "+ cor;
    }
}
```

Agora nós utilizamos o `*@RequestParam*` para capturar o valor de `*cor*` que está na nossa `*URL` .* Em casos onde temos um parâmetro apenas é ok utilizar desta forma mas em casos onde temos mais de um parâmetro pode deixar nossa assinatura de método muito grande ter que especificar cada elemento. Nesses casos é melhor utilizarmos um Map para guardarmos os valores.

```java
// url
localhost:8080/produtos/1?cor=azul&tamanho=pequeno
```

```java
@RestController()
@RequestMapping("/produtos")
public class produtosController {

    @GetMapping("/{id}")
    public String getSpecificProduct(@PathVariable String id, @RequestParam Map<String, String> params){
        return "O produto possui ID "+ id + ", cor "+ params.get("cor") + ", tamanho " + params.get("tamanho");
    }
}
```

## Headers

Podemos fazer a mesma coisa com os headers enviados:

```java
@RestController()
@RequestMapping("/produtos")
public class produtosController {

    @PostMapping
    public String postHeader(@RequestHeader Map<String, String> headers){
        return "Os Headers enviados são " + headers.entrySet();
    }
}
```

> O método `*entrySet*` mostra o objeto em formato de string.

## Body Params

Agora pensando em um cenário em que tenhamos que cadastrar um produto, temos que mudar o método e enviar um `*json*` com as informações a serem cadastradas. Vamos ver como podemos fazer esse processo:

```json
// json enviado
{
	"nome": "jujuba",
	"preco": 1.99
}
```

```java
@RestController()
@RequestMapping("/produtos")
public class produtosController {

    @PostMapping
    public String postProduct(@RequestBody String body){
        System.out.println(body);
        return "produto cadastrado com sucesso.";
    }
}
```

Acima podemos ver o uso de uma anotação `*@RequestBody` .* Ela indica para o `*spring*` que aquela variável receberá o corpo da requisição. No momento, nós estamos tipando esse `*body*` como uma `*String` ,* mostrando ele no console e retornando uma mensagem para sabermos se a requisição funcionou.

Como podemos ver, recebemos o objeto da forma correta, mas estamos com uma versão em `*string literal`* e não um objeto manipulável.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/688d52a2-c224-4667-aca7-aff741a65c27/Untitled.png)

> _Console_

Para isso poderíamos fazer todo um parse de string para objetos, mas esse processo é muito cansativo e nada produtivo. Para isso, iremos ver mais sobre o que são DTOs e como os `*Java Records*` nos ajudam na sua manipulação.

## DTOs: o que são?

> _**Data Transfer Object**_ (DTO) ou simplesmente _**Transfer Object**_ é um padrão de projetos bastante usado em Java para o transporte de dados entre diferentes componentes de um sistema, diferentes instâncias ou processos de um sistema distribuído ou diferentes sistemas via serialização.

A ideia consiste basicamente em agrupar um conjunto de atributos numa classe simples de forma a otimizar a comunicação.Numa chamada remota, seria ineficiente passar cada atributo individualmente. Da mesma forma seria ineficiente ou até causaria erros passar uma entidade mais complexa.

> [java - O que é um DTO? - Stack Overflow em Português](https://pt.stackoverflow.com/questions/31362/o-que-%C3%A9-um-dto)

Ou seja, basicamente são classes simplificadas que representam e estruturam um determinado tipo de dado. No nosso exemplo podemos criar uma classe Pessoa, com nome e idade como propriedades, fornecendo seus tipos e estruturas.

## Java Records

Records é uma funcionalidade relativamente nova em JAVA. Ela foi implementada para diminuir a quantidade de código necessário para criações de classes como as DTOs, que tem como intuito serem classes sem complexidade apenas para transportar informações.

Então ao invés de criarmos uma classe e termos que fazer manualmente a criação da propriedade, configurar como privado, criar construtor, criar métodos getters e etc., o que pode dar um trabalho imenso principalmente se estivermos manipulando um objeto complexo, com Records esse processo é muito simples:

```java
// criando um record de produto
public record DTOProduto(String nome, int preco) {}
```

Bem simples e direto. Algumas observações importantes:

- Os records criam propriedades privadas.
- Essas propriedades são finais - ou seja, imutáveis
- Records geram automaticamente método Getters
- Geram automaticamente métodos Equals e Hashcode

Voltando para nosso exemplo, ele já mostra no console de maneira característica de objeto: com o tipo dele e seus valores.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/e998e19c-3c8f-4f71-9143-710e245d621e/Untitled.png)

> _Console_

```java
@RestController()
@RequestMapping("/produtos")
public class produtosController {

    @PostMapping()
    public String postProduct(@RequestBody DTOProduto body){
        System.out.println(body);
        return "O produto foi " + body.nome() + " com o preco de " + body.preco();
    }
}
```

# Response Entity

Sempre é bom retornarmos informações adicionais na requisição. Com isso podemos utilizar uma classe especial de resposta chamada `*ResponseEntity*`, aceitando `*status codes*`, `*body*` e `*headers` .* Um ponto importante é que essa classe recebe um `*generic*` que representa o que ela vai retornar. Uma `*String*`, um `*Object*`, um `*Resource*` e etc..

Algo interessante que podemos fazer é dizer que ele retorna um Object - que é o `*wrapper class*` mais genérico que temos - e montar nossa resposta com que quisermos, como `*status*`, `*body*`, os `*headers*` e depois chamar o método `*build()*` .

```java
@RestController()
@RequestMapping("/produtos")
public class produtosController {

    @PostMapping()
    public ResponseEntity<Object> postProduct(@RequestBody DTOProduto body){
        System.out.println(body);
        return ResponseEntity.status(HttpStatus.CREATED)
                             .header("teste", "valor1")
                             .build();
    }
}
```

> Obs.: Podemos utilizar a classe `*HttpStatus`* para acessar todos os status code ou podemos apenas passar um `*int*` com o status equivalente, fica à seu critério.

# Validação e Tratativa de Exceções

Ao lidar com dados que são fornecidos pelo cliente, em muitos casos é necessário que façamos uma série de validações para que possamos manipular os dados corretamente. Com as annotations de validação que o próprio spring fornece esse processo fica bem simples.

## Adicionando Dependência

```java
<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

## Definindo Validações

Continuando com os exemplos relacionados à produtos, vamos supor que queremos cadastrar um produto novo. Podemos criar uma entidade produto com todos os campos necessários e suas validações:

```java
@Data
public class Product {

    @Pattern(regexp = "\\\\S+", message = "O campo (name) não deve conter espaços.")
    private String name;
    
    @Length(min = 10, max = 100, message = "A descrição deve conter pelo menos 10 caracteres.")
    private String description;

		@Positive
    private int price;
}
```

Em nosso exemplo, A entidade produto possui três campos. Nome, descrição e preço. Acima deles temos sua respectiva annotation de validação. Algumas possuem valores a serem especificados como é o caso do `*@Pattern*`, que recebe uma `*regex*`, e outras bastam por si só como a `*@Positive*` que valida se a entrada é positiva.

## Annotations de verificação

@NotNull

@NotEmpty

@NotBlank

@Positive / @Negative

@Size

@Min / @Max

@Future / @Past

@Email

> Para a lista completa: [Java Bean Validation Basics | Baeldung](https://www.baeldung.com/java-validation)

## @Data

A annotation `*@data*` que aparece anotada na entidade define automaticamente:

- Métodos Getters
- Métodos Setters
- Método Equals
- Método toString
- Construtor para todos campos `*final*`

## Estruturando Controller

Para que possamos aplicar essa validação, precisamos utilizar a annotation `*@Valid*`. Caso passe nos testes de validação, o fluxo de código continuará normalmente, caso contrário o spring irá lançar uma exceção `*MethodArgumentNotValidException` .*

```java
@RestController()
@RequestMapping("/produtos")
public class produtosController {

    @PostMapping()
    public ResponseEntity<Object> postProduct(@Valid @RequestBody Product body){
        System.out.println(body);

        return ResponseEntity.status(HttpStatus.CREATED).build();
    }
}
```

## Tratando Exceção

Agora com a validação ativa, devemos tratar o erro jogado. Para isso, iremos criar uma classe que irá administrar nossos erros e tratar as exceções.

```java
@ControllerAdvice
public class ExceptionHandlerController {

    @ExceptionHandler(MethodArgumentNotValidException.class)
    public void handleMethodArgumentNotValidException(MethodArgumentNotValidException e){

    }
}
```

## Criando uma validação Customizada.

## @controllerAdvice e @ExceptionHandler

Para que tenhamos uma classe que centraliza o controle das nossas exceções, podemos utilizar a annotation `*@controllerAdvice` .* Ela irá interceptar as exceções de forma global antes do retorno da resposta ao cliente.

> Outro Exemplo:

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/1a90837a-f8f1-456c-b4a3-134240066ead/Untitled.png)

Depois de interceptada, precisamos de uma segunda annotation chamada `*@ExceptionHandler` .* Com ela poderemos especificar qual tipo de erro iremos tratar naquele método especificamente.

## Objeto de Erro

Ao lançar a exceção, o objeto de erro possui diversos métodos e propriedades que não nos interessam. Vamos criar um objeto de erro com o nome do campo que deu problema e sua mensagem:

```java
@Data
@AllArgsConstructor
public class ErrorMessageDTO {
    private String message;
    private String field;
}
```

> `*@AllArgsConstructor`* é **responsável por criar um construtor que recebe como parâmetros todos os atributos da classe.

```java
@ControllerAdvice
public class ExceptionHandlerController {
    private MessageSource messageSource;

		// responsável por capturar a mensagem personalizada definida
		// na annotation
    public ExceptionHandlerController(MessageSource message){
        this.messageSource = message;
    }

    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<ArrayList<ErrorMessageDTO>> handleMethodArgumentNotValidException(MethodArgumentNotValidException e){
        // criando uma lista de erros
				ArrayList<ErrorMessageDTO> errors = new ArrayList<>();

				// fazendo um looping por todos os campos que deram erro
        e.getBindingResult().getFieldErrors().forEach(err ->{

						// extraindo a mensagem 
            String message = messageSource.getMessage(err, LocaleContextHolder.getLocale());
						
						// instanciando o objeto mais simples que criamos
            ErrorMessageDTO erro = new ErrorMessageDTO(message, err.getField());

						// adicionando na lista de erros
            errors.add(erro);
        });

				// retornando um vetor de erros
        return ResponseEntity.status(400).body(errors);
    }
}
```

node: [[SpringBoot]]