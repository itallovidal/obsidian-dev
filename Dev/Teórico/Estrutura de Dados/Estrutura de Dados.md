
# Big O Notation

Serve para descrever tanto a complexidade espacial quanto a complexidade temporal de um determinado algoritmo. Existem algumas classificações que devemos saber, sendo elas:

## O(1) - Tempo Constante.

Essa é classificada como a mais rápida, tendo menor complexidade. Independente da quantidade de Inputs, nosso algoritmo será executado na mesma quantidade de tempo.

#### Exemplo: 
Recuperar o primeiro elemento em uma lista. Sempre terá o mesmo tempo de execução, independente da lista de elementos ter 1 ou 100 itens.

## O(Log n) - Tempo Logarítmico

Neste cenário, o tempo de execução aumenta em Log n, e a quantidade de elementos aumenta em N. Ou seja, o input cresce muito mais rápido do que o tempo de execução.

Podemos ver no gráfico abaixo o algoritmo de Busca Binária - Binary Search - onde consiste em dividir a quantidade de elementos até achar o elemento desejado. 

#### Exemplo: 
- Elemento a ser encontrado: 3
- Vetor: [1, 2, 3, 4, 5, 6, 7, 8, 9 , 10 ]
Começaremos na divisão do vetor, no elemento 4, verificando se ele é igual, maior ou menor do que o elemento a ser encontrado. Neste caso, 5 é maior do que 2, então todos os elementos acima do 5 são descartados. Esse processo se repete até o 2 ser encontrado. 

![[Pasted image 20241030190756.png]]

# O(n) - Tempo Linear

Conforme a quantidade de inputs aumenta, o tempo aumenta proporcionalmente. Se eu demoro X para percorrer 10 elementos, eu vou demorar 2x para percorrer 20 elementos.

#### Exemplo: 
Um cenário onde temos que percorrer um vetor em um for loop.

# O(n log n) - Tempo Linearítmico

Teremos O(n log n) quando tivermos a junção do tempo logarítmico com o linear. Podemos dar como exemplo o Merge Sorting. 

#### Exemplo:
- [3,7, 8, 5,4,2,6,1]
Em um vetor sortido de 1 a 8, o objetivo é reorganizar o vetor de maneira crescente. Para isso, esse vetor vai ser quebrado em vetores menores, dividido recursivamente, até que todos os elementos estejam separados. 

![[Pasted image 20241030205641.png]]

 O próximo passo é montar o vetor novamente, colocando cada elemento de volta no vetor original reorganizando - os.
 
![[Pasted image 20241030205626.png]]

# O($n^2$) - Tempo Quadrático

Quando um temos um for dentro de outro for temos como resultado um tempo quadrático. É considerada também como tempo polinomial. 

#### Exemplo

Caso queiramos pegar todas as duplas de um determinado vetor.
- [1,2,3]
Para isso temos que fazer um looping dentro de outro para assim verificar quais duplas são possíveis.
- 11, 12, 13
- 21, 22, 23
- 31,32,33
Nesse cenário, caso o input cresça de 3 para 6, ele não demoraria duas vezes mais, e sim 36 vezes. 

# O($2^2$) - Tempo exponencial

Como podemos inferir pelo nome, a complexidade destes algoritmos cresce de maneira muito rápida em relação ao input, tornando impraticável para valores muito grandes.

#### Exemplo

Vamos supor que temos um vetor [1, 2, 3].  O objetivo é gerar todos os subconjuntos possíveis. 
- Então temos a possibilidade de estar presente ou ausente.
- N é 3, pois temos 3 elementos
No fim temos $2^3$ de possibilidades que se resultam em:
- []
- [1]
- [2]
- [3]
- [1,2]
- [1,3]
- [2,3]
- [1,2,3]

Para termos de comparação:
- Quando n for 5 teremos  32 possibilidades
- Quando n for 10 teremos  1024 ...
- Quando n for 20 teremos  1.048.576 ...