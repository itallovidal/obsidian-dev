Todo programa escrito por humanos precisa ser convertido para uma linguagem que a máquina entenda. Porém, diferentes linguagens fazem essa operação de diferentes formas.

## Compilação

Por exemplo, em linguagens como `*C*/*C++`,* `Haskell` _,_ `Rust` _, `Go` ,_ o código escrito passa por um processo chamado de _Compilação,_ onde é convertido diretamente para código de máquina - que é binário - para que o processador possa executar. O código é executado de uma vez só.

Isso faz com que sua execução seja mais mais rápida e mais eficiente, aumentando a performance. Elas fornecem ao desenvolvedor controle de hardware como gerenciamento de memória e uso da CPU, por exemplo.

Toda alteração gera uma `*build` ,* ou seja, ao compilar sofre um processo de “montagem“ que fará com que o processador consiga executar. Toda vez que algo no código for mudado, uma nova `*build*` terá de ser gerada para execução.

## Interpretação

Já a linguagem interpretada é executada linha por linha, tendo um interpretador no meio do caminho realizando o processo de conversão para a linguagem de máquina.

Hoje é muito famoso o conceito de JIT - Just in Time - onde a linguagem é compilada de forma modularizada, ou seja, compila de forma dinâmica o código necessário. Exemplos que utilizam esse modelo é `*Javascript*`, e `*Phyton*` .

# WORA

`*Write Once, Run Anywhere*` é um termo utilizado em `*JAVA*` para caracterizar que seu código pode ser escrito uma única vez e rodar em diversos sistemas. A linguagem é tanto interpretada quanto compilada.

Seu código é compilado para `*bytecode` através do `JavaC`_, e depois interpretado com um interpretador chamado `*JVM`_ que utiliza do modelo `*JIT*` para traduzir para o ambiente desejado, seja Windows, Mac, Linux e etc..

## Linguagens Transpiladas

Temos também algumas linguagens que são transpiladas. `*Elm*` e `*Typescript*` são exemplos, onde uma determinada linguagem compila seu código para uma outra linguagem alvo. Ou seja, o código `*Typescript*` gera um código `*javascript`* através de um `*Transpiler`.*

> Para saber mais: [terminologia - Qual a diferença entre linguagem compilada para linguagem interpretada? - Stack Overflow em Português](https://pt.stackoverflow.com/questions/77070/qual-a-diferen%C3%A7a-entre-linguagem-compilada-para-linguagem-interpretada)

# Bundlers `*todo*`

node: [[Arquitetura de Software]]