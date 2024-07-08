# O que é?

O Docker é um ****software de código aberto usado para implantar aplicativos dentro de **`*containers virtuais.*`** A conteinerização permite que vários aplicativos funcionem em diferentes ambientes complexos.

Cada container Docker possui um pacote com as dependências necessárias para a execução de um aplicativo especifico, configurações essas que são ditadas pela `*imagem*`. Dessa maneira, por conta dessa conteinerização é possível, por exemplo, possuir varias aplicações com as configurações em versões diferentes, sem que uma afete a outra.

`*Uma imagem*` é um script de configuração para criar um container, sempre que um usuário a executa, um novo container é criado. Podemos ver uma lista de imagens no site [DockerHub](https://hub.docker.com/).

# **Docker _vs_ Máquina Virtual**

Uma máquina virtual é a emulação de um novo computador através de um computador já existente. Uma máquina virtual serve para que as configurações necessárias para rodar aquela aplicação fique isolada apenas dentro desta máquina emulada.

Já um container Docker é um _pacote de software com todas as dependências necessárias para executar um aplicativo específico._ Todas as configurações e instruções para iniciar ou parar containers são ditadas pela imagem do Docker.

Dessa maneira, por mais que Docker e as máquinas virtuais possuam propósitos semelhantes, o Docker possui o diferencial de não precisar instalar todo um sistema operacional, pois ele reutiliza o sistema utilizado pelo host, o que melhora o desempenho em relação as maquinas virtuais.

Usar containers do Docker poupa aos usuários o incômodo de solucionar possíveis problemas de compatibilidade entre sistemas. Isso porque, com o Docker, um software é executado da mesma forma em todos os ambientes.

# Exemplo de imagem → bitnami/postgresql

O `*bitnami/postgreesql*` é uma imagem para a criação de um docker de um banco de dados `*postgresql*`. Para inicializar uma imagem pela primeira vez é preciso informar ao docker algumas especificidades.

Abaixo veremos o comando e depois uma explicação de cada informação.

## **Comando:**

```jsx
// SINTAXE
docker run --name "app name" -e POSTGRESQL_USERNAME="nome" 
-e POSTGRESQL_PASSWORD="senha" -e POSTGRESQL_DATABASE="nome do banco" 
-p "porta":"porta" "nome da imagem"
```

## Explicação**:**

```jsx
docker run // cria um container a partir de uma imagem
--name "app name" // nome do container
-e POSTGRESQL_USERNAME="nome" //configuração de conexão com  banco
-e POSTGRESQL_PASSWORD="senha" //configuração de conexão com  banco
-e POSTGRESQL_DATABASE="nome do banco" //configuração de conexão com  banco
-p "porta":"porta"
"nome da imagem"
```

## Exemplo**:**

```jsx
docker run
--name api-solid-pg
-e POSTGRESQL_USERNAME=docker
-e POSTGRESQL_PASSWORD=docker
-e POSTGRESQL_DATABASE=apisolid
-p 5432:5432
bitnami/postgresql
```

Pronto! Container, banco e usuário criados a partir da imagem da `*bitnami*`.

<aside> 💡 Sobre a porta `-p` → os containers por padrão rodam na porta `*5432`,* porém, essa porta é aberta apenas no container e não no localhost.

Para tornar possível acessar esse container pelo `*localhost*` é preciso inserir o comando `-p 5432:5432` que serve para dizer que o que for aberto na porta _5432_ do container também será aberto na porta _5432_ do `*localhost*`

</aside>

Após executar esse comando, será gerado no arquivo `.env` uma variável ambiente `DATABASE_URL` com a url de conexão com o banco. Ela vem com valores default, e por isso será necessário alterar para as configurações do banco que foi criado.

_**Default**_

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/6d4b2e3e-b098-4f36-9c45-beeb869f9f96/Untitled.png)

_**Configurado**_

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/308a615e-7c85-4a40-aeb4-5a8c30aa0581/Untitled.png)

# Docker composer

O `*Docker Composer*` serve para automatizar a criação de um ou vários containers. Isso adianta o processo de criação e também registra tudo o que foi usado para o desenvolvimento de uma determinada aplicação. É um arquivo que contém todas as informações, como nome do serviço, a imagem utilizada, variáveis de ambiente, configurações de porta e outras gerais.

Exemplo da diferença de gerar o container pelo `*cli*` e pelo `*composer` .*

> CLI

```jsx
docker run
--name api-solid-pg
-e POSTGRESQL_USERNAME=docker
-e POSTGRESQL_PASSWORD=docker
-e POSTGRESQL_DATABASE=apisolid
-p 5432:5432
bitnami/postgresql
```

> docker-compose.yaml

```
services:
  api-solid-pg:
    image: bitnami/postgresql
    ports:
	      - 5432:5432
    environment:
      - POSTGRESQL_USERNAME=docker
      - POSTGRESQL_PASSWORD=docker
      - POSTGRESQL_DATABASE=apisolid
```

Após criar o arquivo, basta rodar ele usando o seguinte código

```jsx
docker compose up -d
```

Esse comando vai subir todos os containers que foram configurados no arquivo `*docker-compose.yml.` *****

<aside> 💡 O `-d` serve apenas para dizer que os logs não devem ser mostrados.

</aside>

Para parar o container basta rodar o seguinte comando

```jsx
docker compose stop
```

<aside> 💡 Uma coisa muito legal que podemos fazer é salvar o banco no nosso próprio sistema, pois caso tenhamos que apagar o docker, ainda teremos uma cópia de todas as informações armazenadas.

</aside>

```
services:
  api-solid-pg:
    image: bitnami/postgresql
    ports:
      - 5432:5432
    environment:
      - POSTGRESQL_USERNAME=docker
      - POSTGRESQL_PASSWORD=docker
      - POSTGRESQL_DATABASE=apisolid
			- PGDATA: /data/postgres
		volumes:
			- ./data/pg:/data/postgres
```

## Comandos CLI

### Lista os Dockers

Para verificar os containers que existem na maquina, basta rodar o seguinte comando.

```jsx
docker ps -a
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/c7612e84-646f-484a-8107-44c081600bfb/Untitled.png)

### Starta um Docker

Para colocar um container no ar, basta rodar o seguinte comando.

```jsx
// SINTAXE
docker start "nome ou id do container"
```

```jsx
// EXEMPLO
docker start api-solid-pg
```

### Stop em um Docker

Para colocar parar o container, basta rodar o seguinte comando

```jsx
// SINTAXE
docker stop "nome ou id do container"
```

```jsx
// EXEMPLO
docker stop api-solid-pg
```

### Remove um Docker

Para excluir um container, basta rodar o seguinte comando.

```jsx
// SINTAXE
docker rm "nome ou id do container"
```

```jsx
// EXEMPLO
docker rm api-solid-pg
```

### Logs de um Docker

Para ver os logs de um container, basta rodar o seguinte comando

```jsx
// SINTAXE
docker logs "nome ou id do container"
```

```jsx
// EXEMPLO
docker logs api-solid-pg
```

node: [[Backend]]