O react query é uma biblioteca para facilitar a comunicação do front-end com o back-end. Ele ajuda a lidar com erros, cacheamento de informações, sincronização de estado e atualização. Ele possui uma série de hooks que serão facilitadores em todos os processos.

Com ele você pode manipular como que essa requisição será feita quando o usuário estiver sem internet, ou quando a resposta está lenta, ou quem sabe quantas tentativas deverão ser realizadas, o tempo entre elas,  podemos ter noção também de como está o estado da requisição: se ela está pendente, pausada, se deu erro,  quantas vezes deu erro, e etc.

# Instalação

```bash
npm i @tanstack/react-query
```

# useMutation

É considerada mutação qualquer ação de criação, deleção e alteração/atualização.