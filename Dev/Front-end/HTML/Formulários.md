Vamos dar uma olhada na estrutura base de um formulário e em como ele se comporta. Um formulário é uma estrutura que recebe informações e as envia para algum lugar. Pode ser para outra página, pode ser para um banco de dados, um email e etc..

Em sua estrutura veremos tags inputs, tags labels e tags de botão. Os inputs servem para capturar os dados. Esses dados podem ser texto, número, data, pode ser uma lista com opcões, pode ser email, podem ser vários tipos de dados diferentes.

Para que o usuário saiba que tipo de dado ele deve colocar, temos a etiqueta: label. Ela servirá de título para nossos inputs. Temos no fim, um botão. Ele pode ser com um input do tipo botão, ou um botão do tipo submit.

```html
<form action="form.php" method="get">

    <label for="nome">Digite seu nome</label>
    <input id="nome" name="nomeUsuario" type="text">

    <button type="submit">Enviar</button>
</form>
```

“Submit” quer dizer submeter, nesse caso, enviar. Toda vez que um form tem todas as suas informações validadas, ele tem seu “submit”. Por padrão, ele envia os dados coletados atualizando a página. Esse envio pode ser feito por GET ou POST, dependendo do valor atribuído ao atributo method. O atributo action indica para onde essas informações devem ser enviadas.

Basicamente o método GET envia os dados pela URL da página, de forma visível, e é indicado para envio de poucas informações. Já o método POST encapsula os dados de forma básica e nos dá a possibilidade de enviar mais informações, como imagensm, por exemplo.

É normal que na tag label tenha o atributo For, ele indica para qual input aquela etiqueta serve, informando ao navegador que ao clicar na informação, determinada input deve ter foco. Isso serve principalmente para termos de acessibilidade.

Vemos também o atributo name, responsável por vincular a informação recebida a um determinado nome, para que ao enviar os dados possamos capturá-los por esse nome. Outro atributo muito importante é o atributo type.

Com ele podemos informar qual tipo de dado aquele input vai receber, se é uma string, se é um número, uma string com formatação de email, uma data, e etc.. Suas verificações são básicas, então é importante que nós façamos uma checagem mais cuidadosa com JS e depois PHP.

```html
<select name="escolaridadeUsuario" id="escolaridade">
    <option value="fundamental">ensino fundamental</option>
    <option value="meido">ensino medio</option>
    <option value="facul">faculdade</option>
</select>
```

Uma estrutura muito interessante é a lista com o select. Com ele podemos fornecer uma série de opções para o usuário prontas para que ele possa selecionar. Basta usar o valor de cada opção no value da tag.

Tópico: [[HTML]]