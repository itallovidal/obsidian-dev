## Iniciando um Projeto

Através do [Spring Initializr](https://start.spring.io/) , podemos configurar nosso projeto com qual ferramenta de administração de dependências iremos utilizar, qual linguagem iremos desenvolver, a versão do `*spring*` e informações gerais do projeto. Além disso, podemos adicionar as dependências de uma maneira simples apenas com alguns cliques. O `*Spring Initializr*` serve como uma interface guia para adiantar nosso desenvolvimento.

Ou seja, não criamos o projeto diretamente na IDE, mas sim em um site externo. Poderíamos até criar o projeto diretamente na IDE, porém através do initializr esse processo é mais simples e rápido. Depois de configurar tudo, podemos simplesmente baixar o zip.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/3097bea9-73c9-4b79-a7a6-60bc7dfc044e/Untitled.png)

## Configurando a IDE:

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/9f772b34-2d51-4fb7-be35-d707ae913665/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/8c3de7fc-80ac-4cc2-8860-c8e359f1056f/Untitled.png)

## Entendendo as Configurações: O que é Maven?

A primeira configuração é para qual linguagem iremos desenvolver. Já que iremos desenvolver nossa API em `*JAVA*`, iremos utilizar a opção `*Maven*`. Ele é um administrador de pacotes para `*JAVA*`.

> “*É muito comum encontrar projetos que fazem o uso de outras bibliotecas ou frameworks, para usá-los é necessário acessá-los através da dependências. As dependências em Java são arquivos comprimidos e armazenados com a extensão `.jar`.

Alguns dessas dependências possuem uma ou mais subdependências e algumas delas possuem uma ou mais subsubdependências, e por aí vai. Ao invés de quando você precisar de uma dependência você ir em busca dela no Google, baixá-la, adicionar no seu projeto e descobrir que ela precisa de X novas subdependências e ficar num ciclo gigante à caça de dependências, você pode automatizar esse processo ~~chato e~~ cansativo, e focar no desenvolvimento que é o que realmente dá valor ao seu projeto. O Maven automatiza isso para você! “*

> **
> 
> _Ao pesquisar por uma dependência para ser acessada através do Maven você obterá um trecho XML que serve para configurar o `pom.xml` do seu projeto e indicar que você estará fazendo uso dessa dependência em seu projeto. Ao adicionar esse trecho, o Maven faz o download dela e armazena em um repositório local no seu computador, se você possuir mais de um projeto fazendo uso da mesma dependência você só terá um único arquivo no seu computador, no seu repositório local organizado pelo Maven._
> 
> - **[java - Para que serve o Maven? - Stack Overflow em Português](https://pt.stackoverflow.com/questions/59240/para-que-serve-o-maven)

Depois disso, escolhemos uma versão estável e recente do springBoot e configuramos algumas informações gerais do projeto como nome, descrição e etc., além da seleção da versão do `*JAVA`.*

## .JAR vs .WAR: Quais diferenças?

Essas são duas opções que temos para a escolha de formatos de arquivos usados no desenvolvimento de uma aplicação com Spring. Ao seleção de .JAR é um formato de arquivo que é usado para distribuir classes em `*JAVA*`, associar metadados e recursos. Geralmente utilizado em aplicações onde são `*stand-alone*`. Veremos isso em breve.

A seleção .WAR é um tipo de arquivo .JAR mas que serve para empacotar aplicações WEB, contendo arquivos HTML, imagens, e arquivos JS. Para ele rodar precisa também de estar em um servidor. Nosso objeto é criar uma API responsável por manipular determinados recursos, não sendo uma aplicação web com arquivos HTML, imagens e etc. sendo uma aplicação `*stand-alone`.*

## Dependências

Para ajudar no nosso desenvolvimento marcamos algumas dependências interessantes. O Spring Web nós dá o suporte para desenvolver APIs RESTFul, configurando o TOMCAT - servidor - para que possamos subir nossa API e utilizando o padrão MVC em sua implementação.

O Lombok é uma biblioteca que utiliza de Anotações para configurar/representar/adiantar determinadas funções para que o nosso desenvolvimento seja mais dinâmico. E a última, mas não menos importante é o Dev tools que nos possibilita live reload e faz com que nossa aplicação restarte com as configurações atualizadas mais rapidamente.