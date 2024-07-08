### Listas Ordenadas e Não Ordenadas

As listas são muito úteis para quando queremos mostrar um conjunto de itens relacionados. Seja ela ordenada - com números, por exemplo- ou sem ordenação - com bolinhas - agora veremos sua estrutura básica.

```html
<h3>O que já estudei</h3>
<ul>
    <li> <s> Html básico </s> </li>
    <li>Html intermediario</li>
    <li>Html avançado</li>
</ul>

<h3>Minhas linguagens preferidas</h3>
<ol>
    <li>CSS</li>
    <li>JS</li>
    <li>C#</li>
</ol>
```

Podemos ver que tanto na lista ordenada quanto na lista não ordenada temos a tag li, que indica o nome do item da lista - list item. A única diferença é a tag externa que define se é uma lista ordenada ou uma lista não ordenada - Ordered List ou Unordered List.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/23dc2244-4b35-4d55-97eb-7bf1bd885306/Untitled.png)

Obs.: Estamos usando uma tag <s> que indica que o texto deve ser riscado.

### Listas Descritivas

As listas descritivas são responsáveis por, como o nome sugere, descrever determinado termo. Com elas teremos um termo - data term - e uma descrição - data description. Por padrão elas possuem essa estrutura e esse padrão de estilo:

```html
<h3>Tipos de Linguagem</h3>
<dl>
    <dt>HTML</dt>
    <dd>Linguagem de marcação de texto.</dd>

    <dt>CSS</dt>
    <dd>Linguagem de estilização em cascata.</dd>

    <dt>JS</dt>
    <dd>Linguagem de programação.</dd>
</dl>
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a57ab2ba-23e7-4b4f-ba4a-7fe0422175ae/Untitled.png)

Tópico: [[HTML]]