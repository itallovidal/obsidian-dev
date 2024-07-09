## Join

Os comandos `join` servem para unir colunas de diferentes tabelas. Existem alguns tipos de `join` → `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`.

### Inner Join

O comando `inner join` é responsável por retornar somente as informações que as tabelas tem em comum.

```sql
#SINTAXE
SELECT <select_list> // colunas que quer selecionar
FROM Tabela A // a tabela aonde vai pegar
INNER JOIN Tabela B // a outra tabela aonde tamebem vai pegar
ON A.Key = B.Key // a coluna que faza a ligação entre as duas
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/da45f784-ef3c-4085-a80a-425e5d558dcf/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/58a15130-5de3-495a-8094-6bbc2cbd7ae8/Untitled.png)

```sql
#EXEMPLO
SELECT nome, num // nome de paciente e numero de fonep
FROM paciente // tabela paciente
INNER JOIN fonep // tabela fonep
ON fonep.idpac = paciente.idpac; // pega os dados aonde 
//as linhas tiverem o valor de idpac igual
```

Então esse exemplo retornará o nome e numero dos pacientes que possuem números e números e possuem algum paciente. Dessa maneira, não retorna linha com valor igual a `null`

### Left Join

O comando `left join` é responsável por retornar todas as linhas de uma tabela A, mais as linhas de uma tabela B que tenha dados na tabela A

```sql
#SINTAXE
SELECT <select_list> // colunas que quer selecionar
FROM Tabela A // a tabela aonde vai pegar
LEFT JOIN Tabela B // a outra tabela aonde tamebem vai pegar
ON A.Key = B.Key // a coluna que faza a ligação entre as duas
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/bc7f8201-5324-4206-966f-d89f9966ca7b/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/f2e1edfc-df17-413c-bfda-3d2eab34db7a/Untitled.png)

```sql
#EXEMPLO
SELECT nome, num // nome de paciente e numero de fonep
FROM paciente // tabela paciente
LEFT JOIN fonep // tabela fonep
ON fonep.idpac = paciente.idpac; // pega os dados aonde 
//as linhas tiverem o valor de idpac igual
```

Então esse exemplo retornará todos os nomes da tabela paciente, independente se possui numero ou não. Porém, os números só serão retornados se possuírem um nome na tabela paciente

### Right Join

O comando `right join` é responsável por retornar todas as linhas de uma tabela B, mais as linhas de uma tabela A que tenha dados na tabela B

```sql
#SINTAXE
SELECT <select_list> // colunas que quer selecionar
FROM Tabela A // a tabela aonde vai pegar
RIGHT JOIN Tabela B // a outra tabela aonde tamebem vai pegar
ON A.Key = B.Key // a coluna que faza a ligação entre as duas
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/5522d8ef-9ec0-4dbf-bd22-b97e5a38809e/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/05164f00-e11f-4420-afa4-bb286ce20d32/Untitled.png)

```sql
#EXEMPLO
SELECT nome, num // nome de paciente e numero de fonep
FROM paciente // tabela paciente
RIGHT JOIN fonep // tabela fonep
ON fonep.idpac = paciente.idpac; // pega os dados aonde 
//as linhas tiverem o valor de idpac igual
```

Então esse exemplo retornará todos os números da tabela fonep, independente se possui nome ou não. Porém, os nomes só serão retornados se possuírem um número na tabela fonep.

node: [[SQL]]