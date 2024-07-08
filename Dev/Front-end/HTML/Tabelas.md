As tabelas são uma parte bem importante da web. Antigamente as páginas eram organizadas em formato de tabela porque era mais fácil de disponibilizar o conteúdo. Elas faziam o papel do display Grid de hoje em dia. Ainda hoje os emails são estruturados em formas de tabelas. Agora nós vamos ver a estrutura delas:

Você pode ver que temos uma tag table que engloba toda a tabela. A lógica da tabela é que teremos linhas e dentro dessas linhas iremos ter as informações. Uma tabela pode ser lateralizada - quando os títulos aparecem ao lado das informações - ou podem ser verticais - quando os títulos aparecem no topo da tabela. Depende muito de como você quer dispor a tabela, então veremos das duas formas. Vamos fazer a tabela lateral por enquanto:

```html
<table>
				<tr>
	        <th>Meus horários</th>
				</tr>
        <tr>
            <th> Manhã </th>
            <td> HTML </td>
            <td> CSS </td>
            <td> JS </td>
        </tr>
        <tr>
            <th> Tarde</th>
            <td> exercicios HTML </td>
            <td> exercicios CSS </td>
            <td> exercicios JS </td>
        </tr>
        <tr>
            <th> Noite </th>
            <td> Descansar </td>
        </tr>
        <tr>
            <td> Madrugada </td>
        </tr>
    </table>
```

Podemos ver que o Th seria Table Header - ou cabecalho da tabela - e ele está dentro de um Tr, que seria Table Row - Linha da Tabela. Além disso, temos nossas informações dentro da tag Td, que seria table data.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d00612fe-d770-4715-965f-b5d96d9caeef/Untitled.png)

Está um pouco feinho justamente pela falta de estilo. Vamos aplicar um estilo básico só para que possamos ver melhor nossa estrutura. Lembrando que o foco agora não é CSS.

```html
<style>
        table{
						width: 60%;
            background-color: rgb(81, 81, 81);
            padding: 2%;
            color: white;
            text-align: center;
        }

        th{
            background-color: black;
            padding: 1.5%;
        }

        td{
            background-color: white;
            color: black;
            padding: 1.5%;
        }
    </style>
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c455f1e0-947f-4059-8c34-402664c84c30/Untitled.png)

Esse pequeno código já faz com que consigamos entender melhor cada parte da tabela. Podemos ver que as informações estão com fundo branco, os títulos estão pretos e o fundo da tabela está cinza. Aqui temos um problema fácil de solucionar. Podemos ver que o título “meus horários” deveriam cobrir a tabela toda, assim como a parte de “descansar” deveria se extender da noite até a madrugada. Isso ocorre porque a tabela está com 4 células dentro da linha e por padrão, uma informação preenche apenas 1 espaço.

Podemos alterar esse comportamento usando colspan e rowspan, que informa quantas células determinada informação irá preecher:

```html
<table>
        <tr>
						<!-- preencher 4 celulas -->
            <th colspan="4">Meus horários</th>
        </tr>

        <tr>
            <th> Manhã </th>
            <td> HTML </td>
            <td> CSS </td>
            <td> JS </td>
        </tr>
        <tr>
            <th> Tarde </th>
            <td> exercicios HTML </td>
            <td> exercicios CSS </td>
            <td> exercicios JS </td>
        </tr>
        <tr>
            <th> Noite </th>
						<!-- preencher 4 celulas e duas linhas-->
            <td colspan="4" rowspan="2"> Descansar </td>
        </tr>
        <tr>
            <th> Madrugada </th>
        </tr>
    </table>
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7dc9ded3-9c0b-4c11-be25-e38e70c7a7c5/Untitled.png)

Pronto, temos nossa tabela funcionando! Agora vamos fazer com que ela fique vertical. Teremos que naturalmente reorganizar a nossa tabela.

```html
<table>
        <tr>
            <th colspan="4">Meus horários</th>
        </tr>
        <tr>
            <th> Manhã </th>
            <th> Tarde </th>
            <th> Noite </th>
            <th> Madrugada </th>
        </tr>

        <tr>
            <td> HTML </td>
            <td>Exercício de HTML</td>
            <td colspan="2" rowspan="3"> Descansar </td>
        </tr>
        <tr>
            <td> CSS </td> 
            <td>Exercício de CSS</td>           
        </tr>
        <tr>
            <td> JS </td>
            <td>Exercício de JS</td>
        </tr>
    </table>
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d439104f-d629-42ba-b801-5b236ebfaeeb/Untitled.png)

Note que sempre temos uma linha sozinha de horários, fazendo papel de legenda para essa tabela. Pensando nisso, podemos trocar essas duas tags **<tr><th> legenda </th> </tr>** por uma tag caption que serve justamente para definir uma legenda para uma tabela.

Além disso, podemos também acrescentar uma tag Thead e Tbody para delimitar onde é o cabecalho e onde é o corpo da tabela. Toda essa semântica nos ajuda a estilizar sem que precisemos ficar adicionando vários id`s e classes nos elementos já que cada elemento que cumpre uma função específica detém uma tag referente.

```html
<style>
        table{
            width: 60%;
            background-color: rgb(81, 81, 81);
            padding: 2%;
            color: white;
            text-align: center;
        }

        caption{
            background-color: rgb(180, 176, 185);
            padding-block: 3%;
            font-size: 2rem;
            color: black;
            font-weight: bold
        }

        thead{
            background-color: black;
        }

        tbody{
            background-color: white;
            color: black;
        }

        td{
            padding: 1.5%;
        }
    </style>

    <table>
        <caption>Meus horários</caption>
        <thead>
            <tr>
                <th> Manhã </th>
                <th> Tarde </th>
                <th> Noite </th>
                <th> Madrugada </th>
            </tr>
        </thead>

        <tbody>
            <tr>
                <td> HTML </td>
                <td>Exercício de HTML</td>
                <td colspan="2" rowspan="3"> Descansar </td>
            </tr>
            <tr>
                <td> CSS </td> 
                <td>Exercício de CSS</td>           
            </tr>
            <tr>
                <td> JS </td>
                <td>Exercício de JS</td>
            </tr>
        </tbody>
    </table>
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/68d63a60-7866-482f-8d60-79f6d38b171a/Untitled.png)

Tópico: [[HTML]]