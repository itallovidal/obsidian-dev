## Fazendo a Conexão

Para fazer a conexão entre o código e o banco de dados, precisamos criar duas variáveis de ambiente capazes de armazenar tanto a URL do banco quanto a chave capaz de se conectar com ele. Utilizando o `*vite*`, podemos criar um arquivo `*.env`* que servirá para guardar variáveis globais de ambiente.

```tsx
// note que usamos o prefixo VITE para que o vite reconheça as variáveis
// esse prefixo pode mudar de acordo com o ambiente e o servidor.
VITE_SUPABASE_URL="url do banco"
VITE_ANON_KEY="chave para conectar no banco"
```

Instalamos o pacote do supabase no nosso ambiente de desenvolvimento:

> OBS.: essa instalação dependerá da sua linguagem utilizada. Veja a [documentação](https://supabase.com/docs) para mais informações de `*getting started*`

```tsx
npm i @supabase/supabase-js
```

Feito isso, configuramos o objeto responsável por executar as tarefas relacionadas ao `*supabase*`.

```tsx
import { createClient } from '@supabase/supabase-js'
						
										// note que para importar corretamente utilizando o vite
										// precisamos utilizar "import.meta" ao invés de "process"
const supabaseUrl = import.meta.env.VITE_SUPABASE_URL
const supabaseKey = import.meta.env.VITE_ANON_KEY

// criando e exportando o objeto supabase utilizando a url e a chave.
export const supabase = createClient(supabaseUrl, supabaseKey)
```

## Supabase e as Querys

A estrutura das `*querys`* é ligeiramente diferente de como fazemos com `*SQL`* diretamente. Abaixo, veremos como fazemos utilizando no código o objeto `*supabase*` e logo depois o seu equivalente utilizando apenas `*SQL.*`

> OBS.: O supabase permite que façamos teste de querys através do campo SQL Editor. Nele podemos testar e verificar seu retorno antes de implementarmos no código.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/44bc9484-d615-454a-8e65-4a4b4a582375/825dac63-e0c9-4c1c-bf51-3173f26badef/Untitled.png)

## SELECT

O `*select*` é um comando utilizado para selecionar tudo ou uma determinada parte da tabela.

```sql
// selecione tudo da tabela usuários
SELECT * from users
```

```sql
// selecione tudo da tabela usuários		
const {data, error } = await supabase.from('users').select()
```

Note que o objeto que executa a `query` ****retorna dois outros objetos.

1. Um objeto de data - que são as informações que nós solicitamos
2. Um objeto de `*error*`, que indica o erro caso ele tenha acontecido.

O método `*select*` recebe uma string com o nome do campo a ser selecionado.

## SELECT com filtro (WHERE)

Para fazer filtragem é um pouquinho diferente. Enquanto utilizamos WHERE no SQL diretamente, com o objeto do `supabase` utilizaremos o método `*eq()*` . Este método recebe o nome do campo, e o valor a ser procurado.

```sql
// selecione o nome de users onde o nome é igual a juquinha
SELECT name from users WHERE name = 'juquinha'
```

```sql
// selecione o nome de users onde o nome é igual a juquinha
const {data, error} = await supabase.from('users').select('name').eq('name', 'juquinha')
```

Desta forma irá retornar um vetor de objetos - caso ele encontre registros - mesmo se o retorno tiver um único usuário. Para casos que sabemos que irá retornar apenas um registro podemos utilizar o método `*single()*` para que ele não retorne como vetor e sim o objeto direto.

```sql
// selecione o nome de users onde o nome é igual a juquinha
const {data, error} = await supabase.from('users').select('name').eq('name', 'juquinha')
```

**// completar com where múltiplo**

## INSERT INTO

Para inserir dados na tabela é muito simples:

```sql
// insere dentro de users (nos campos) os valores (x, y, z)
INSERT INTO users(name, hobbie, password) VALUES ('itallo', 'gaming', '12345')
```

```sql
const { error } = await supabase
										.from("users")
										.insert([{ nome: 'itallo', hobbie: 'gaming', password: '12345' }]);
```

O comando `insert` recebe um vetor de objetos. Cada objeto representa uma `*row` .* Ou seja, podemos inserir mais de uma linha no `insert`, basta passarmos vários objetos. Importante tomar cuidado para não inserir campos que o próprio banco pode gerar.

> OBS.: Vale a pena salientar que comando de `*insert*` não devolvem nenhuma `*row*` por padrão. Esse comportamento pode ser sobrescrito no supabase utilizando um `*select*` no final da query.

## UPDATE

O comando update serve para atualizar os valores. Ele possui algumas diferenças na abordagem.

```sql
// atualiza a tabela users, substitui o valor de hobbie para ler onde o nome for itallo.
UPDATE users SET hobbie = 'ler' where name = 'itallo'
```

```sql
const { data, error } = await supabase
												  .from('users')
												  .update({ hobbie: 'ler' })
												  .eq('name', 'itallo')
```

Caso passemos uma variável para o update - que é a maioria dos casos - e essa variável tiver o mesmo nome do campo, podemos omiti-lo e deixara sintaxe mais curta.

```sql
const hobbie = 'ler'

const { data, error } = await supabase
												  .from('users')
												  .update({ hobbie })
												  .eq('name', 'itallo')
```

## DELETE

Para deletar é bem direto:

```sql
// deleta de users onde o campo x é igual ao valor x
DELETE FROM users WHERE name = 'itallo'
```

```sql

const { data, error } = await supabase
												  .from('users')
												  .delete()
												  .eq('name', 'itallo')
```

## ORDER BY

Para ordenar a os dados de acordo com os valores de um campo.

```sql
 // ordena as informacoes de forma decrescente de acordo com o campo created_at 
SELECT * FROM users ORDER BY created_at DESC
```

```sql

const { data, error } = await supabase
													.from('users')
													.select()
													.order('created_at', {ascending: false})

```

O método `*order()*` recebe dois valores, o campo que quer ordenar e um objeto de configuração onde podemos especificar se os valores serão retornados de forma ascendente ou descendente.

node: [[SQL]]