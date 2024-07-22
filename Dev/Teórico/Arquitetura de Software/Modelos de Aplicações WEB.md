Ao desenvolver sites, devemos levar em consideração qual modelo iremos aplicar em nosso desenvolvimento. Os modelos atuais mais comuns são:

- MPA - Multi Page App
    - Aplicações WEB onde dado uma requisição WEB, o servidor irá manipular os dados e devolver uma página relacionada. Tudo acontece na parte do servidor.
- SPA - Single Page App
    - Aplicações WEB onde possuem um HTML base e seus trechos onde possuem interação com o usuário são carregados dinamicamente.
- PWA - Progressive Web App
    - São aplicações que buscam levar a WEB para o campo mobile, fornecendo a possibilidade de rodá-los em seu próprio webview.

# MVC Pattern

O padrão MVC é um padrão que visa segmentar a aplicação para tornar mais simples o desenvolvimento de aplicações mais complexas. O intuito é ter três segmentos:

- Model
- View
- Controller

## Controllers

Os controladores são responsáveis por receber uma determinada requisição HTTP. Eles lidam com a requisição informando o resto do servidor os próximos passos do que fazer com aquela requisição. Geralmente não possui muito código, servindo apenas como intermédio entre os outros dois segmentos.

## Model

Os modelos são responsáveis por lidar com toda a lógica e dados de um determinado recurso. Depois que a requisição chega ao controller, ele chama o Modelo adequado para lidar com aquela solicitação. Podem fazer validações, administrar dados, conexões com banco, etc etc..

> O modelo não deve se preocupar em lidar com a requisição em si, o que fazer ao dar erro ou tudo dar certo. A única coisa que ele deve fazer é aplicar a lógica para administrar determinado recurso.

O controlador não deve se preocupar em lidar com a lógica da requisição, em manipular os dados nem nada do tipo, isso deve ser feito pelo modelo. Ao receber a resposta do modelo, ele deve mandar ao View aquela informação e como apresentar.

## View

A view vai pegar aquele dado do controller, vai montar a apresentação - ou seja, o trecho HTML com os dados, estrutura correta e etc.. - e vai devolver para o controller para que ele possa dar a resposta da requisição.

Ou seja, na prática, é feito uma requisição para API, o Controller recebe essa requisição, utiliza do Model para manipular esses dados, e dependendo da solicitação devolve uma View - página da WEB - com todas as informações necessárias ou equivalentes àquela requisição.

# Aplicação WEB

Com SpringBoot conseguimos desenvolver tanto APIs REST quanto Aplicações WEB MPA.

Uma delas é que a página só é carregada após todo o processo desejado pela requisição for feito. Por isso que alguns sites que utilizam desse padrão de aplicação WEB, demoram a carregar dependendo da solicitação realizada. Por conta disso, não é possível carregar a página dinamicamente.

# REST API

**Representational State Transfer**, é uma arquitetura conhecida por ser simples, padronizada, escalável e stateless entre cliente e servidor. O fato de ser stateless significa que ela não guarda nenhum tipo de dado ou informação entre as requisições. Como sua execução é cacheável, torna-se muito performática.

Cada elemento a ser solicitado à API é chamado de recurso. Então uma listagem de produtos são recursos, um produto específico é um recurso, e assim por diante. Toda solicitação enviada à API chamamos de `*request*` , e toda devolução da API é chamado de `*response*` .

## Request

É muito comum que uma requisição tenha:

- Seu método HTTP
    - POST, GET, DELETE, PUT, PATCH, UPDATE etc..
- EndPoint
    - Rotas que identificam um recurso
- Parâmetros
    - Valores relacionados à alguma chave que acrescentam informações sobre qual recurso buscar
- Body Request - Corpo
    - Informações adicionais, geralmente utilizadas quando queremos adicionar, alterar ou atualizar um recurso
- Headers
    - Informações adicionais sobre a requisição em si, como chaves de autenticação, como deseja que o recurso seja retornado, tipo de cachê, como a solicitação está enviando os dados e etc..

Leitura Recomendada:

> [Diferença entre @RestController e @Controller Annotation no Spring MVC e REST | by Gilberto | Medium](https://medium.com/@gcbrandao/diferen%C3%A7a-entre-restcontroller-e-controller-annotation-no-spring-mvc-e-rest-8533998a93eb)

node: [[Arquitetura de Software]]